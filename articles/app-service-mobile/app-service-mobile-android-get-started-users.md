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
# <a name="add-authentication-tooyour-android-app"></a><span data-ttu-id="8b691-103">Dodawanie aplikacji dla systemu Android tooyour uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="8b691-103">Add authentication tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="8b691-104">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="8b691-104">Summary</span></span>
<span data-ttu-id="8b691-105">W tym samouczku można dodać projekt szybkiego startu todolist toohello uwierzytelniania w systemie Android przy użyciu dostawcy tożsamości obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="8b691-105">In this tutorial, you add authentication toohello todolist quickstart project on Android by using a supported identity provider.</span></span> <span data-ttu-id="8b691-106">W tym samouczku jest oparta na powitania [Rozpoczynanie pracy z usługą Mobile Apps] — samouczek, należy najpierw wykonać.</span><span class="sxs-lookup"><span data-stu-id="8b691-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="8b691-107"><a name="register"></a>Zarejestrować aplikację do uwierzytelniania i konfigurowanie usługi Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8b691-107"><a name="register"></a>Register your app for authentication and configure Azure App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="8b691-108"><a name="redirecturl"></a>Dodaj adresy URL przekierowania zewnętrznych dozwolone Twojej aplikacji toohello</span><span class="sxs-lookup"><span data-stu-id="8b691-108"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="8b691-109">Bezpieczne uwierzytelnianie wymaga Zdefiniuj nowy schemat adresu URL dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8b691-109">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="8b691-110">Po zakończeniu procesu uwierzytelniania hello dzięki temu hello uwierzytelniania systemu tooredirect wstecz tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8b691-110">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="8b691-111">W tym samouczku używamy schemat adresu URL hello _appname_ w ciągu.</span><span class="sxs-lookup"><span data-stu-id="8b691-111">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="8b691-112">Można jednak użyć dowolnego wybranego schematu URL.</span><span class="sxs-lookup"><span data-stu-id="8b691-112">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="8b691-113">Powinna być unikatowa tooyour aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="8b691-113">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="8b691-114">Przekierowanie hello tooenable na powitania po stronie serwera:</span><span class="sxs-lookup"><span data-stu-id="8b691-114">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="8b691-115">W hello [portalu Azure] wybierz usługę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8b691-115">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="8b691-116">Kliknij przycisk hello **uwierzytelniania / autoryzacji** opcji menu.</span><span class="sxs-lookup"><span data-stu-id="8b691-116">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="8b691-117">W hello **dozwolone zewnętrznych adresów URL przekierowań**, wprowadź `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="8b691-117">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="8b691-118">Witaj _appname_ ten ciąg jest hello schemat adresu URL aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="8b691-118">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="8b691-119">Musi on być zgodny normalne Specyfikacja adresu URL dla protokołu (Użyj litery i tylko cyfry i rozpoczyna się od litery).</span><span class="sxs-lookup"><span data-stu-id="8b691-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="8b691-120">Należy zanotuj ciąg hello, który możesz wybrać, ponieważ będzie potrzebny tooadjust kodu aplikacji mobilnej przy użyciu hello schemat adresu URL w kilku miejscach.</span><span class="sxs-lookup"><span data-stu-id="8b691-120">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="8b691-121">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8b691-121">Click **OK**.</span></span>

5. <span data-ttu-id="8b691-122">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8b691-122">Click **Save**.</span></span>

## <span data-ttu-id="8b691-123"><a name="permissions"></a>Ogranicz uprawnienia tooauthenticated użytkowników</span><span class="sxs-lookup"><span data-stu-id="8b691-123"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* <span data-ttu-id="8b691-124">W programie Android Studio Otwórz projekt hello Ukończono z samouczka hello [Rozpoczynanie pracy z usługą Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="8b691-124">In Android Studio, open hello project you completed with hello tutorial [Get started with Mobile Apps].</span></span> <span data-ttu-id="8b691-125">Z hello **Uruchom** menu, kliknij przycisk **uruchamianie aplikacji**i sprawdź, czy wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8b691-125">From hello **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span>

     <span data-ttu-id="8b691-126">Ten wyjątek spowodowany prób aplikacji hello tooaccess Witaj ponownie kończyć się jako użytkownik nieuwierzytelniony, ale hello *TodoItem* tabeli teraz wymaga uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="8b691-126">This exception happens because hello app attempts tooaccess hello back end as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="8b691-127">Następnie zaktualizuj użytkownicy tooauthenticate aplikacji hello przed wysłaniem żądania zasobów z hello kończyć Mobile Apps ponownie.</span><span class="sxs-lookup"><span data-stu-id="8b691-127">Next, you update hello app tooauthenticate users before requesting resources from hello Mobile Apps back end.</span></span> 

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="8b691-128">Dodaj aplikację toohello uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="8b691-128">Add authentication toohello app</span></span>
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <span data-ttu-id="8b691-129"><a name="cache-tokens"></a>Tokeny uwierzytelniania pamięci podręcznej na powitania klienta</span><span class="sxs-lookup"><span data-stu-id="8b691-129"><a name="cache-tokens"></a>Cache authentication tokens on hello client</span></span>
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="8b691-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8b691-130">Next steps</span></span>
<span data-ttu-id="8b691-131">Teraz, aby ukończyć w tym samouczku uwierzytelnianie podstawowe, należy wziąć pod uwagę kontynuować tooone hello następujące samouczki:</span><span class="sxs-lookup"><span data-stu-id="8b691-131">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="8b691-132">[Dodawanie aplikacji dla systemu Android tooyour powiadomień wypychanych](app-service-mobile-android-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="8b691-132">[Add push notifications tooyour Android app](app-service-mobile-android-get-started-push.md).</span></span>
  <span data-ttu-id="8b691-133">Dowiedz się, jak tooconfigure aplikacji mobilnych z powrotem kończyć powiadomień wypychanych toosend toouse Azure notification hubs.</span><span class="sxs-lookup"><span data-stu-id="8b691-133">Learn how tooconfigure your Mobile Apps back end toouse Azure notification hubs toosend push notifications.</span></span>
* <span data-ttu-id="8b691-134">[Włączanie synchronizacji w trybie offline dla aplikacji systemu Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="8b691-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="8b691-135">Dowiedz się, jak w trybie offline tooadd obsługują tooyour aplikacji przy użyciu zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="8b691-135">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="8b691-136">Z synchronizacji w trybie offline, użytkownicy mogą korzystać z aplikacji mobilnej&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.</span><span class="sxs-lookup"><span data-stu-id="8b691-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[Rozpoczynanie pracy z usługą Mobile Apps]: app-service-mobile-android-get-started.md
