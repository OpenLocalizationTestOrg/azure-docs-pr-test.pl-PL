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
# <a name="add-push-notifications-tooyour-android-app"></a><span data-ttu-id="42696-103">Dodawanie aplikacji dla systemu Android tooyour powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="42696-103">Add push notifications tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="42696-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="42696-104">Overview</span></span>
<span data-ttu-id="42696-105">W tym samouczku, możesz dodać toohello powiadomień wypychanych [Android szybki start] projektu, aby powiadomienie wypychane zostanie wysłane toohello urządzenia, za każdym razem, gdy wstawieniu rekordu.</span><span class="sxs-lookup"><span data-stu-id="42696-105">In this tutorial, you add push notifications toohello [Android quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="42696-106">Jeśli nie używasz hello pobrany Projekt serwera szybki start, muszą hello pakiet rozszerzenia powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="42696-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="42696-107">Aby uzyskać więcej informacji, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="42696-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42696-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="42696-108">Prerequisites</span></span>
<span data-ttu-id="42696-109">Potrzebne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="42696-109">You need hello following:</span></span>

* <span data-ttu-id="42696-110">IDE, w zależności od projektu zaplecza:</span><span class="sxs-lookup"><span data-stu-id="42696-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="42696-111">[Android Studio](https://developer.android.com/sdk/index.html) Jeśli ta aplikacja ma zaplecza Node.js.</span><span class="sxs-lookup"><span data-stu-id="42696-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="42696-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) lub nowszym, jeśli ta aplikacja ma zaplecze .NET firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="42696-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="42696-113">Android 2.3 i nowszy, poprawki repozytorium Google 27 lub nowszym i usług Google Play 9.0.2 lub nowszy Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="42696-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="42696-114">Zakończenie hello [Android szybki start].</span><span class="sxs-lookup"><span data-stu-id="42696-114">Complete hello [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="42696-115">Tworzenie projektu obsługującego usługę Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="42696-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="42696-116">Konfigurowanie Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="42696-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="42696-117">Konfigurowanie powiadomień wypychanych Azure toosend</span><span class="sxs-lookup"><span data-stu-id="42696-117">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a><span data-ttu-id="42696-118">Włącz powiadomienia wypychane na powitania serwera projektu</span><span class="sxs-lookup"><span data-stu-id="42696-118">Enable push notifications for hello server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="42696-119">Dodaj aplikację tooyour powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="42696-119">Add push notifications tooyour app</span></span>
<span data-ttu-id="42696-120">W tej sekcji należy zaktualizować klienta powiadomień wypychanych toohandle aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="42696-120">In this section, you update your client Android app toohandle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="42696-121">Sprawdź wersję zestawu SDK systemu Android</span><span class="sxs-lookup"><span data-stu-id="42696-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="42696-122">Następnym krokiem jest tooinstall usług Google Play.</span><span class="sxs-lookup"><span data-stu-id="42696-122">Your next step is tooinstall Google Play services.</span></span> <span data-ttu-id="42696-123">Google Cloud Messaging ma niektóre minimalne interfejsu API poziomu wymagania dotyczące projektowania i testowania, które hello **minSdkVersion** właściwości w manifeście hello muszą być zgodne.</span><span class="sxs-lookup"><span data-stu-id="42696-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which hello **minSdkVersion** property in hello manifest must conform to.</span></span>

<span data-ttu-id="42696-124">Jeśli testujesz starsze urządzenia, należy skontaktować się [ustawić się Google Play zestaw SDK usług] toodetermine jak niska, ustaw tę wartość i odpowiednio ją ustawić.</span><span class="sxs-lookup"><span data-stu-id="42696-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] toodetermine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="42696-125">Dodaj projekt toohello usług Google Play</span><span class="sxs-lookup"><span data-stu-id="42696-125">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="42696-126">Dodawanie kodu</span><span class="sxs-lookup"><span data-stu-id="42696-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a><span data-ttu-id="42696-127">Test aplikacji hello hello opublikowane usługi mobilnej</span><span class="sxs-lookup"><span data-stu-id="42696-127">Test hello app against hello published mobile service</span></span>
<span data-ttu-id="42696-128">Można przetestować aplikacji hello, dołączając bezpośrednio telefonie z systemem Android za pomocą kabla USB lub za pomocą urządzenia wirtualnego w emulatorze hello.</span><span class="sxs-lookup"><span data-stu-id="42696-128">You can test hello app by directly attaching an Android phone with a USB cable, or by using a virtual device in hello emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42696-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="42696-129">Next steps</span></span>
<span data-ttu-id="42696-130">Po ukończeniu tego samouczka, rozważ kontynuować tooone hello następujące samouczki:</span><span class="sxs-lookup"><span data-stu-id="42696-130">Now that you completed this tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="42696-131">[Dodawanie aplikacji dla systemu Android tooyour uwierzytelniania](app-service-mobile-android-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="42696-131">[Add authentication tooyour Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="42696-132">Dowiedz się, jak projektu tooadd uwierzytelniania toohello todolist — Szybki Start w systemie Android przy użyciu dostawcy tożsamości obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="42696-132">Learn how tooadd authentication toohello todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="42696-133">[Włączanie synchronizacji w trybie offline dla aplikacji systemu Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="42696-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="42696-134">Dowiedz się, jak w trybie offline tooadd obsługują tooyour aplikacji przy użyciu zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="42696-134">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="42696-135">Z synchronizacji w trybie offline, użytkownicy mogą korzystać z aplikacji mobilnej&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.</span><span class="sxs-lookup"><span data-stu-id="42696-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
[Android szybki start]: app-service-mobile-android-get-started.md

[ustawić się Google Play zestaw SDK usług]:https://developers.google.com/android/guides/setup
