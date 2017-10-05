---
title: "Dodawanie powiadomień wypychanych do aplikacji systemu Android z usługą Mobile Apps | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak korzystać z aplikacji mobilnej do wysyłania powiadomień wypychanych do aplikacji systemu Android."
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
ms.openlocfilehash: b89e9af55342d5d7473d848956996f846250b4b5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-android-app"></a><span data-ttu-id="e5fd7-103">Dodawanie powiadomień wypychanych do aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="e5fd7-103">Add push notifications to your Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="e5fd7-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e5fd7-104">Overview</span></span>
<span data-ttu-id="e5fd7-105">W tym samouczku, dodawanie powiadomień wypychanych do [Android szybki start] projektu, aby powiadomienia wypychane są wysyłane do urządzenia, za każdym razem, gdy wstawieniu rekordu.</span><span class="sxs-lookup"><span data-stu-id="e5fd7-105">In this tutorial, you add push notifications to the [Android quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="e5fd7-106">Szybki start pobrany Projekt serwera nie jest używany, należy najpierw pakiet rozszerzenia powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="e5fd7-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="e5fd7-107">Aby uzyskać więcej informacji, zobacz [pracować z serwera wewnętrznej bazy danych .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="e5fd7-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5fd7-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e5fd7-108">Prerequisites</span></span>
<span data-ttu-id="e5fd7-109">Potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e5fd7-109">You need the following:</span></span>

* <span data-ttu-id="e5fd7-110">IDE, w zależności od projektu zaplecza:</span><span class="sxs-lookup"><span data-stu-id="e5fd7-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="e5fd7-111">[Android Studio](https://developer.android.com/sdk/index.html) Jeśli ta aplikacja ma zaplecza Node.js.</span><span class="sxs-lookup"><span data-stu-id="e5fd7-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="e5fd7-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) lub nowszym, jeśli ta aplikacja ma zaplecze .NET firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e5fd7-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="e5fd7-113">Android 2.3 i nowszy, poprawki repozytorium Google 27 lub nowszym i usług Google Play 9.0.2 lub nowszy Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="e5fd7-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="e5fd7-114">Zakończenie [Android szybki start].</span><span class="sxs-lookup"><span data-stu-id="e5fd7-114">Complete the [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="e5fd7-115">Tworzenie projektu obsługującego usługę Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="e5fd7-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="e5fd7-116">Konfigurowanie Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="e5fd7-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="e5fd7-117">Konfigurowanie usługi Azure do wysyłania powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="e5fd7-117">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-the-server-project"></a><span data-ttu-id="e5fd7-118">Włącz powiadomienia wypychane dla server project</span><span class="sxs-lookup"><span data-stu-id="e5fd7-118">Enable push notifications for the server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="e5fd7-119">Dodawanie powiadomień wypychanych do aplikacji</span><span class="sxs-lookup"><span data-stu-id="e5fd7-119">Add push notifications to your app</span></span>
<span data-ttu-id="e5fd7-120">W tej sekcji należy zaktualizować klienta aplikacji systemu Android do obsługi powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="e5fd7-120">In this section, you update your client Android app to handle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="e5fd7-121">Sprawdź wersję zestawu SDK systemu Android</span><span class="sxs-lookup"><span data-stu-id="e5fd7-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="e5fd7-122">Następnym krokiem jest Zainstaluj usługi Google Play.</span><span class="sxs-lookup"><span data-stu-id="e5fd7-122">Your next step is to install Google Play services.</span></span> <span data-ttu-id="e5fd7-123">Google Cloud Messaging ma niektóre minimalne interfejsu API poziomu wymagania dotyczące projektowania i testowania, który **minSdkVersion** musi odpowiadać właściwości w manifeście.</span><span class="sxs-lookup"><span data-stu-id="e5fd7-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which the **minSdkVersion** property in the manifest must conform to.</span></span>

<span data-ttu-id="e5fd7-124">Jeśli testujesz starsze urządzenia, należy skontaktować się [ustawić się Google Play zestaw SDK usług] ustalenie, jak niska można ustawić tej wartości i odpowiednio ją ustawić.</span><span class="sxs-lookup"><span data-stu-id="e5fd7-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] to determine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="e5fd7-125">Dodawanie usług Google Play do projektu</span><span class="sxs-lookup"><span data-stu-id="e5fd7-125">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="e5fd7-126">Dodawanie kodu</span><span class="sxs-lookup"><span data-stu-id="e5fd7-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-the-app-against-the-published-mobile-service"></a><span data-ttu-id="e5fd7-127">Testowanie aplikacji opublikowanych usługi mobilnej</span><span class="sxs-lookup"><span data-stu-id="e5fd7-127">Test the app against the published mobile service</span></span>
<span data-ttu-id="e5fd7-128">Można przetestować aplikację, dołączając bezpośrednio telefonie z systemem Android za pomocą kabla USB lub za pomocą urządzenia wirtualnego w emulatorze.</span><span class="sxs-lookup"><span data-stu-id="e5fd7-128">You can test the app by directly attaching an Android phone with a USB cable, or by using a virtual device in the emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5fd7-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e5fd7-129">Next steps</span></span>
<span data-ttu-id="e5fd7-130">Po ukończeniu tego samouczka, rozważ kontynuowanie na jedno z następujących samouczków:</span><span class="sxs-lookup"><span data-stu-id="e5fd7-130">Now that you completed this tutorial, consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="e5fd7-131">[Dodawanie uwierzytelniania do aplikacji systemu Android](app-service-mobile-android-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="e5fd7-131">[Add authentication to your Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="e5fd7-132">Dowiedz się, jak dodawanie uwierzytelniania do listy zadań projektu szybkiego startu w programie Android przy użyciu dostawcy tożsamości obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="e5fd7-132">Learn how to add authentication to the todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="e5fd7-133">[Włączanie synchronizacji w trybie offline dla aplikacji systemu Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="e5fd7-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="e5fd7-134">Dowiedz się, jak dodać obsługę w trybie offline do aplikacji przy użyciu zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="e5fd7-134">Learn how to add offline support to your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="e5fd7-135">Z synchronizacji w trybie offline, użytkownicy mogą korzystać z aplikacji mobilnej&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.</span><span class="sxs-lookup"><span data-stu-id="e5fd7-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
<span data-ttu-id="e5fd7-136">[Android szybki start]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="e5fd7-136">[Android quick start]: app-service-mobile-android-get-started.md</span></span>

<span data-ttu-id="e5fd7-137">[ustawić się Google Play zestaw SDK usług]:https://developers.google.com/android/guides/setup</span><span class="sxs-lookup"><span data-stu-id="e5fd7-137">[Set Up Google Play Services SDK]:https://developers.google.com/android/guides/setup</span></span>
