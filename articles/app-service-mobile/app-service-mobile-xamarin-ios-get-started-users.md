---
title: Wprowadzenie do uwierzytelniania dla aplikacji mobilnych w systemu Xamarin iOS
description: "Dowiedz się, jak używać Mobile Apps do uwierzytelniania użytkowników aplikacji platformy Xamarin iOS za pomocą różnych dostawców tożsamości, obejmującej AAD, Google, Facebook, Twitter i Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 180cc61b-19c5-48bf-a16c-7181aef3eacc
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: glenga
ms.openlocfilehash: 454b2df5a9bf8cfba93befea54370957ab044d95
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-xamarinios-app"></a><span data-ttu-id="db586-103">Dodawanie uwierzytelniania do aplikacji platformy Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="db586-103">Add authentication to your Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="db586-104">W tym temacie przedstawiono, jak uwierzytelniać użytkowników aplikacji usługi Mobile aplikacji z poziomu aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="db586-104">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="db586-105">W tym samouczku Dodawanie uwierzytelniania do projektu szybkiego startu platformy Xamarin.iOS przy użyciu dostawcy tożsamości, która jest obsługiwana przez usługę App Service.</span><span class="sxs-lookup"><span data-stu-id="db586-105">In this tutorial, you add authentication to the Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="db586-106">Po pomyślnie trwa uwierzytelnieniu i autoryzacji w aplikacji mobilnej, jest wyświetlana wartość Identyfikatora użytkownika i będzie można uzyskać dostęp do danych tabeli ograniczone.</span><span class="sxs-lookup"><span data-stu-id="db586-106">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed and you will be able to access restricted table data.</span></span>

<span data-ttu-id="db586-107">Najpierw musisz zakończyć samouczka [tworzenie aplikacji platformy Xamarin.iOS].</span><span class="sxs-lookup"><span data-stu-id="db586-107">You must first complete the tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="db586-108">Jeśli nie używasz szybki start pobrany Projekt serwera, należy dodać pakietu rozszerzenia uwierzytelniania do projektu.</span><span class="sxs-lookup"><span data-stu-id="db586-108">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="db586-109">Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="db586-109">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="db586-110">Zarejestrować aplikację do uwierzytelniania i konfigurowanie usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="db586-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-to-the-allowed-external-redirect-urls"></a><span data-ttu-id="db586-111">Dodaj aplikację do dozwolonych przekierowania zewnętrzne adresy URL</span><span class="sxs-lookup"><span data-stu-id="db586-111">Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="db586-112">Bezpieczne uwierzytelnianie wymaga Zdefiniuj nowy schemat adresu URL dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="db586-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="db586-113">Dzięki temu system uwierzytelniania przekierować z powrotem do aplikacji po zakończeniu procesu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="db586-113">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="db586-114">W tym samouczku używamy schemat adresu URL _appname_ w ciągu.</span><span class="sxs-lookup"><span data-stu-id="db586-114">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="db586-115">Można jednak użyć dowolnego wybranego schematu URL.</span><span class="sxs-lookup"><span data-stu-id="db586-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="db586-116">Powinien być unikatowy w aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="db586-116">It should be unique to your mobile application.</span></span> <span data-ttu-id="db586-117">Aby włączyć przekierowywanie po stronie serwera:</span><span class="sxs-lookup"><span data-stu-id="db586-117">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="db586-118">W [portalu Azure] wybierz usługę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="db586-118">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="db586-119">Kliknij przycisk **uwierzytelniania / autoryzacji** opcji menu.</span><span class="sxs-lookup"><span data-stu-id="db586-119">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="db586-120">W **dozwolone zewnętrznych adresów URL przekierowań**, wprowadź `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="db586-120">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="db586-121">**Url_scheme_of_your_app** w tym ciągu jest schemat adresu URL dla aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="db586-121">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="db586-122">Musi on być zgodny normalne Specyfikacja adresu URL dla protokołu (Użyj litery i tylko cyfry i rozpoczyna się od litery).</span><span class="sxs-lookup"><span data-stu-id="db586-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="db586-123">Należy zanotuj ciąg, który wybrany jako trzeba będzie dostosować kodu aplikacji mobilnej przy użyciu schemat adresu URL w kilku miejscach.</span><span class="sxs-lookup"><span data-stu-id="db586-123">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="db586-124">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="db586-124">Click **OK**.</span></span>

5. <span data-ttu-id="db586-125">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="db586-125">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="db586-126">Ogranicz uprawnienia dla uwierzytelnionych użytkowników</span><span class="sxs-lookup"><span data-stu-id="db586-126">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="db586-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="db586-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="db586-128">W programie Visual Studio lub Xamarin Studio uruchamianie projektu klienta na urządzenia lub emulatora.</span><span class="sxs-lookup"><span data-stu-id="db586-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="db586-129">Upewnij się, że wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="db586-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="db586-130">Niepowodzenie jest rejestrowane w konsoli debugera.</span><span class="sxs-lookup"><span data-stu-id="db586-130">The failure is logged to the console of the debugger.</span></span> <span data-ttu-id="db586-131">Dlatego w programie Visual Studio powinna zostać wyświetlona awarii w oknie danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="db586-131">So in Visual Studio, you should see the failure in the output window.</span></span>

<span data-ttu-id="db586-132">&nbsp;&nbsp;Tego błędu nieautoryzowanego odbywa się, ponieważ aplikacja próbuje uzyskać dostęp jako użytkownik nieuwierzytelniony zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="db586-132">&nbsp;&nbsp;This unauthorized failure happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="db586-133">*TodoItem* tabeli teraz wymaga uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="db586-133">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="db586-134">Następnie możesz zaktualizuje aplikacji klienckiej żądania zasobów z zaplecza aplikacji mobilnej z uwierzytelnionego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="db586-134">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="db586-135">Dodawanie uwierzytelniania do aplikacji</span><span class="sxs-lookup"><span data-stu-id="db586-135">Add authentication to the app</span></span>
<span data-ttu-id="db586-136">W tej sekcji należy zmodyfikować aplikację, aby wyświetlić ekran logowania przed wyświetleniem danych.</span><span class="sxs-lookup"><span data-stu-id="db586-136">In this section, you will modify the app to display a login screen before displaying data.</span></span> <span data-ttu-id="db586-137">Po uruchomieniu aplikacji, nie nie łączy się z usługą aplikacji i nie zawiera żadnych danych.</span><span class="sxs-lookup"><span data-stu-id="db586-137">When the app starts, it will not not connect to your App Service and will not display any data.</span></span> <span data-ttu-id="db586-138">Po raz pierwszy użytkownik wykonuje gestu odświeżania, pojawi się ekran logowania. Po pomyślnym logowaniu pojawi się lista zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="db586-138">After the first time that the user performs the refresh gesture, the login screen will appear; after successful login the list of todo items will be displayed.</span></span>

1. <span data-ttu-id="db586-139">W projekcie klienta, otwórz plik **QSTodoService.cs** i dodaj następującą instrukcję using i `MobileServiceUser` z metody dostępu do klasy QSTodoService:</span><span class="sxs-lookup"><span data-stu-id="db586-139">In the client project, open the file **QSTodoService.cs** and add the following using statement and `MobileServiceUser` with accessor to the QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="db586-140">Dodaj nową metodę o nazwie **Uwierzytelnij** do **QSTodoService** z następującej definicji:</span><span class="sxs-lookup"><span data-stu-id="db586-140">Add new method named **Authenticate** to **QSTodoService** with the following definition:</span></span>

        public async Task Authenticate(UIViewController view)
        {
            try
            {
                AppDelegate.ResumeWithURL = url => url.Scheme == "zumoe2etestapp" && client.ResumeWithURL(url);
                user = await client.LoginAsync(view, MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine (@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
            }
        }

    >[AZURE.NOTE] <span data-ttu-id="db586-141">Jeśli używasz dostawcy tożsamości innych niż Facebook, zmień wartość przekazana do **LoginAsync** powyżej do jednej z następujących czynności: _MicrosoftAccount_, _Twitter_, _Google_, lub _WindowsAzureActiveDirectory_.</span><span class="sxs-lookup"><span data-stu-id="db586-141">If you are using an identity provider other than a Facebook, change the value passed to **LoginAsync** above to one of the following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="db586-142">Otwórz **QSTodoListViewController.cs**.</span><span class="sxs-lookup"><span data-stu-id="db586-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="db586-143">Zmodyfikować definicję metody **ViewDidLoad** usuwanie wywołanie **RefreshAsync()** w pobliżu elementu end:</span><span class="sxs-lookup"><span data-stu-id="db586-143">Modify the method definition of **ViewDidLoad** removing the call to **RefreshAsync()** near the end:</span></span>
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out the call to RefreshAsync
            // await RefreshAsync();
        }
4. <span data-ttu-id="db586-144">Zmodyfikuj metodę **RefreshAsync** uwierzytelniać **użytkownika** właściwość ma wartość null.</span><span class="sxs-lookup"><span data-stu-id="db586-144">Modify the method **RefreshAsync** to authenticate if the **User** property is null.</span></span> <span data-ttu-id="db586-145">Dodaj następujący kod w górnej części definicja metody:</span><span class="sxs-lookup"><span data-stu-id="db586-145">Add the following code at the top of the method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="db586-146">Otwórz **AppDelegate.cs**, dodaj następującą metodę:</span><span class="sxs-lookup"><span data-stu-id="db586-146">Open **AppDelegate.cs**, add the following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="db586-147">Otwórz **Info.plist** pliku, przejdź do **typy adresu URL** w **zaawansowane** sekcji.</span><span class="sxs-lookup"><span data-stu-id="db586-147">Open **Info.plist** file, navigate to **URL Types** in the **Advanced** section.</span></span> <span data-ttu-id="db586-148">Teraz skonfigurować **identyfikator** i **Schematy adresów URL** typ adresu URL i kliknij przycisk **Dodawanie adresu URL typu**.</span><span class="sxs-lookup"><span data-stu-id="db586-148">Now configure the **Identifier** and the **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="db586-149">**Schematy adresów URL** powinna być taka sama jak Twoje {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="db586-149">**URL Schemes** should be the same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="db586-150">W programie Visual Studio lub Xamarin Studio połączony z hostem Xamarin kompilacji na komputerze Mac, uruchamianie projektu klienta przeznaczonych dla określonego urządzenia lub emulatora.</span><span class="sxs-lookup"><span data-stu-id="db586-150">In Visual Studio or Xamarin Studio connected to your Xamarin Build Host on your Mac, run the client project targeting a device or emulator.</span></span> <span data-ttu-id="db586-151">Sprawdź, czy aplikacja nie wyświetla żadnych danych.</span><span class="sxs-lookup"><span data-stu-id="db586-151">Verify that the app displays no data.</span></span>
   
    <span data-ttu-id="db586-152">Wykonuje gestu odświeżania ściąganie w dół listę elementów, co spowoduje wyświetlenie ekranu logowania.</span><span class="sxs-lookup"><span data-stu-id="db586-152">Perform the refresh gesture by pulling down the list of items, which will cause the login screen to appear.</span></span> <span data-ttu-id="db586-153">Po pomyślnie zostały wprowadzone prawidłowe poświadczenia, aplikacja będzie wyświetlana lista zadań do wykonania i mogą wysyłać aktualizacje do danych.</span><span class="sxs-lookup"><span data-stu-id="db586-153">Once you have successfully entered valid credentials, the app will display the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
<span data-ttu-id="db586-154">[tworzenie aplikacji platformy Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="db586-154">[Create a Xamarin.iOS app]: app-service-mobile-xamarin-ios-get-started.md</span></span>