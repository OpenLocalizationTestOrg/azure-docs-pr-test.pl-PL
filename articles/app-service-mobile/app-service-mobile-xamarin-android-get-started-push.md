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
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a><span data-ttu-id="e2e50-103">Dodawanie aplikacji platformy Xamarin.Android tooyour powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="e2e50-103">Add push notifications tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="e2e50-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e2e50-104">Overview</span></span>
<span data-ttu-id="e2e50-105">W tym samouczku, możesz dodać toohello powiadomień wypychanych [Xamarin.Android szybki start](app-service-mobile-windows-store-dotnet-get-started.md) projektu, aby powiadomienie wypychane zostanie wysłane toohello urządzenia, za każdym razem, gdy wstawieniu rekordu.</span><span class="sxs-lookup"><span data-stu-id="e2e50-105">In this tutorial, you add push notifications toohello [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="e2e50-106">Jeśli nie używasz hello pobrany Projekt serwera szybki start, muszą hello pakiet rozszerzenia powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="e2e50-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="e2e50-107">Zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="e2e50-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2e50-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e2e50-108">Prerequisites</span></span>
<span data-ttu-id="e2e50-109">Ten samouczek wymaga następujących hello:</span><span class="sxs-lookup"><span data-stu-id="e2e50-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="e2e50-110">Aktywne konto Google.</span><span class="sxs-lookup"><span data-stu-id="e2e50-110">An active Google account.</span></span> <span data-ttu-id="e2e50-111">Można założyć konto Google na [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="e2e50-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="e2e50-112">[Usługa Google Cloud Messaging składnik klienta](http://components.xamarin.com/view/GCMClient/).</span><span class="sxs-lookup"><span data-stu-id="e2e50-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="e2e50-113"><a name="configure-hub"></a>Konfigurowanie Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="e2e50-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="e2e50-114"><a id="register"></a>Włącz Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="e2e50-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a><span data-ttu-id="e2e50-115">Skonfiguruj żądań wypychania Azure toosend</span><span class="sxs-lookup"><span data-stu-id="e2e50-115">Configure Azure toosend push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="e2e50-116"><a id="update-server"></a>Zaktualizuj powiadomień wypychanych toosend powitania serwera projektu</span><span class="sxs-lookup"><span data-stu-id="e2e50-116"><a id="update-server"></a>Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="e2e50-117"><a id="configure-app"></a>Konfigurowanie powitania klienta projektu powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="e2e50-117"><a id="configure-app"></a>Configure hello client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="e2e50-118"><a id="add-push"></a>Dodaj aplikację tooyour kodu powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="e2e50-118"><a id="add-push"></a>Add push notifications code tooyour app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="e2e50-119"><a name="test"></a>Testowych powiadomień wypychanych w aplikacji</span><span class="sxs-lookup"><span data-stu-id="e2e50-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="e2e50-120">Aplikacja hello można testować przy użyciu urządzenia wirtualnego w emulatorze hello.</span><span class="sxs-lookup"><span data-stu-id="e2e50-120">You can test hello app by using a virtual device in hello emulator.</span></span> <span data-ttu-id="e2e50-121">Brak dodatkowych czynności konfiguracyjnych wymaganych podczas uruchamiania emulatora.</span><span class="sxs-lookup"><span data-stu-id="e2e50-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="e2e50-122">Upewnij się, że jest wdrażany tooor debugowania na urządzeniu wirtualnym z interfejsów API Google, ustawić jako cel hello, jak pokazano poniżej w hello Android Virtual Device (AVD) manager.</span><span class="sxs-lookup"><span data-stu-id="e2e50-122">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="e2e50-123">Dodanie urządzenia Android toohello konto Google, klikając **aplikacje** > **ustawienia** > **Dodaj konto**, następnie postępuj zgodnie z monitami hello.</span><span class="sxs-lookup"><span data-stu-id="e2e50-123">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="e2e50-124">Uruchamianie aplikacji todolist hello jako przed i Wstaw nowe zadanie do wykonania.</span><span class="sxs-lookup"><span data-stu-id="e2e50-124">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="e2e50-125">Teraz, w obszarze powiadomień hello jest wyświetlana ikona powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="e2e50-125">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="e2e50-126">Można także otworzyć hello powiadomień szuflady tooview hello pełny tekst hello powiadomień.</span><span class="sxs-lookup"><span data-stu-id="e2e50-126">You can open hello notification drawer tooview hello full text of hello notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
