---
title: "aaaGet uruchomiony przy użyciu uwierzytelniania dla aplikacji mobilnych w systemu Xamarin iOS"
description: "Dowiedz się, jak toouse Mobile Apps tooauthenticate użytkowników aplikacji platformy Xamarin iOS za pomocą różnych dostawców tożsamości, obejmującej AAD, Google, Facebook, Twitter i firmy Microsoft."
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
ms.openlocfilehash: 6458e9651b03df61c86b88b11953792e04bfa5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinios-app"></a><span data-ttu-id="454d8-103">Dodaj aplikację platformy Xamarin.iOS tooyour uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="454d8-103">Add authentication tooyour Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="454d8-104">W tym temacie opisano sposób tooauthenticate użytkowników aplikację usługi Mobile aplikacji z poziomu aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="454d8-104">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="454d8-105">W tym samouczku możesz dodać uwierzytelniania toohello Xamarin.iOS projekt szybkiego startu przy użyciu dostawcy tożsamości, która jest obsługiwana przez usługę App Service.</span><span class="sxs-lookup"><span data-stu-id="454d8-105">In this tutorial, you add authentication toohello Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="454d8-106">Po pomyślnie trwa uwierzytelnieniu i autoryzacji w aplikacji mobilnej, jest wyświetlana wartość Identyfikatora użytkownika hello i będą mogli tooaccess ograniczone tabeli danych.</span><span class="sxs-lookup"><span data-stu-id="454d8-106">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed and you will be able tooaccess restricted table data.</span></span>

<span data-ttu-id="454d8-107">Najpierw musisz zakończyć samouczek hello [tworzenie aplikacji platformy Xamarin.iOS].</span><span class="sxs-lookup"><span data-stu-id="454d8-107">You must first complete hello tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="454d8-108">Jeśli nie używasz hello pobrany Projekt serwera szybki start, należy dodać projekt tooyour hello uwierzytelniania rozszerzenie pakietu.</span><span class="sxs-lookup"><span data-stu-id="454d8-108">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="454d8-109">Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="454d8-109">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="454d8-110">Zarejestrować aplikację do uwierzytelniania i konfigurowanie usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="454d8-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a><span data-ttu-id="454d8-111">Dodaj adresy URL przekierowania zewnętrznych dozwolone Twojej aplikacji toohello</span><span class="sxs-lookup"><span data-stu-id="454d8-111">Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="454d8-112">Bezpieczne uwierzytelnianie wymaga Zdefiniuj nowy schemat adresu URL dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="454d8-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="454d8-113">Po zakończeniu procesu uwierzytelniania hello dzięki temu hello uwierzytelniania systemu tooredirect wstecz tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="454d8-113">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="454d8-114">W tym samouczku używamy schemat adresu URL hello _appname_ w ciągu.</span><span class="sxs-lookup"><span data-stu-id="454d8-114">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="454d8-115">Można jednak użyć dowolnego wybranego schematu URL.</span><span class="sxs-lookup"><span data-stu-id="454d8-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="454d8-116">Powinna być unikatowa tooyour aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="454d8-116">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="454d8-117">Przekierowanie hello tooenable na powitania po stronie serwera:</span><span class="sxs-lookup"><span data-stu-id="454d8-117">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="454d8-118">W hello [portalu Azure] wybierz usługę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="454d8-118">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="454d8-119">Kliknij przycisk hello **uwierzytelniania / autoryzacji** opcji menu.</span><span class="sxs-lookup"><span data-stu-id="454d8-119">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="454d8-120">W hello **dozwolone zewnętrznych adresów URL przekierowań**, wprowadź `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="454d8-120">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="454d8-121">Witaj **url_scheme_of_your_app** w tym ciągu jest hello schemat adresu URL aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="454d8-121">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="454d8-122">Musi on być zgodny normalne Specyfikacja adresu URL dla protokołu (Użyj litery i tylko cyfry i rozpoczyna się od litery).</span><span class="sxs-lookup"><span data-stu-id="454d8-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="454d8-123">Należy zanotuj ciąg hello, który możesz wybrać, ponieważ będzie potrzebny tooadjust kodu aplikacji mobilnej przy użyciu hello schemat adresu URL w kilku miejscach.</span><span class="sxs-lookup"><span data-stu-id="454d8-123">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="454d8-124">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="454d8-124">Click **OK**.</span></span>

5. <span data-ttu-id="454d8-125">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="454d8-125">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="454d8-126">Ogranicz uprawnienia tooauthenticated użytkowników</span><span class="sxs-lookup"><span data-stu-id="454d8-126">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="454d8-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="454d8-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="454d8-128">W programie Visual Studio lub Xamarin Studio Uruchom projekt klienta hello na urządzenia lub emulatora.</span><span class="sxs-lookup"><span data-stu-id="454d8-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="454d8-129">Upewnij się, że wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="454d8-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="454d8-130">Błąd Hello jest rejestrowane toohello konsoli hello debugera.</span><span class="sxs-lookup"><span data-stu-id="454d8-130">hello failure is logged toohello console of hello debugger.</span></span> <span data-ttu-id="454d8-131">Dlatego w programie Visual Studio hello awarii w oknie danych wyjściowych hello powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="454d8-131">So in Visual Studio, you should see hello failure in hello output window.</span></span>

<span data-ttu-id="454d8-132">&nbsp;&nbsp;Ten błąd nieautoryzowanego wynika z faktu, aplikacja hello prób tooaccess zaplecza aplikacji mobilnej jako nieuwierzytelniony użytkownik.</span><span class="sxs-lookup"><span data-stu-id="454d8-132">&nbsp;&nbsp;This unauthorized failure happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="454d8-133">Witaj *TodoItem* tabeli teraz wymaga uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="454d8-133">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="454d8-134">Następnie zaktualizuje powitania klienta aplikacji toorequest zasobów z zaplecza aplikacji mobilnej hello z uwierzytelnionego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="454d8-134">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="454d8-135">Dodaj aplikację toohello uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="454d8-135">Add authentication toohello app</span></span>
<span data-ttu-id="454d8-136">W tej sekcji należy zmodyfikować przed wyświetleniem danych toodisplay aplikacji hello ekran logowania.</span><span class="sxs-lookup"><span data-stu-id="454d8-136">In this section, you will modify hello app toodisplay a login screen before displaying data.</span></span> <span data-ttu-id="454d8-137">Po uruchomieniu aplikacji hello nie nie będą łączyć się tooyour usługi aplikacji i nie zawiera żadnych danych.</span><span class="sxs-lookup"><span data-stu-id="454d8-137">When hello app starts, it will not not connect tooyour App Service and will not display any data.</span></span> <span data-ttu-id="454d8-138">Po powitania po raz pierwszy użytkownik hello wykonuje hello gestu odświeżania, zostanie wyświetlony ekran logowania hello; Po pojawi się lista zadań do wykonania w hello pomyślnego logowania.</span><span class="sxs-lookup"><span data-stu-id="454d8-138">After hello first time that hello user performs hello refresh gesture, hello login screen will appear; after successful login hello list of todo items will be displayed.</span></span>

1. <span data-ttu-id="454d8-139">W hello projektu klienta, otwórz plik hello **QSTodoService.cs** i dodaj następujące hello za pomocą instrukcji i `MobileServiceUser` z toohello akcesor QSTodoService klasy:</span><span class="sxs-lookup"><span data-stu-id="454d8-139">In hello client project, open hello file **QSTodoService.cs** and add hello following using statement and `MobileServiceUser` with accessor toohello QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="454d8-140">Dodaj nową metodę o nazwie **Uwierzytelnij** za**QSTodoService** z powitania po definicji:</span><span class="sxs-lookup"><span data-stu-id="454d8-140">Add new method named **Authenticate** too**QSTodoService** with hello following definition:</span></span>

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

    >[AZURE.NOTE] <span data-ttu-id="454d8-141">Jeśli używasz dostawcy tożsamości innych niż Facebook, zmień wartość hello przekazano zbyt**LoginAsync** powyżej tooone następującego hello: _MicrosoftAccount_, _Twitter_, _Google_, lub _WindowsAzureActiveDirectory_.</span><span class="sxs-lookup"><span data-stu-id="454d8-141">If you are using an identity provider other than a Facebook, change hello value passed too**LoginAsync** above tooone of hello following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="454d8-142">Otwórz **QSTodoListViewController.cs**.</span><span class="sxs-lookup"><span data-stu-id="454d8-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="454d8-143">Zmodyfikuj definicję metody hello **ViewDidLoad** usuwanie hello wywołanie za**RefreshAsync()** niemal zakończenia hello:</span><span class="sxs-lookup"><span data-stu-id="454d8-143">Modify hello method definition of **ViewDidLoad** removing hello call too**RefreshAsync()** near hello end:</span></span>
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out hello call tooRefreshAsync
            // await RefreshAsync();
        }
4. <span data-ttu-id="454d8-144">Zmodyfikuj metodę hello **RefreshAsync** tooauthenticate Jeśli hello **użytkownika** właściwość ma wartość null.</span><span class="sxs-lookup"><span data-stu-id="454d8-144">Modify hello method **RefreshAsync** tooauthenticate if hello **User** property is null.</span></span> <span data-ttu-id="454d8-145">Dodaj następującego kodu u góry hello definicję metody hello hello:</span><span class="sxs-lookup"><span data-stu-id="454d8-145">Add hello following code at hello top of hello method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="454d8-146">Otwórz **AppDelegate.cs**, Dodaj hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="454d8-146">Open **AppDelegate.cs**, add hello following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="454d8-147">Otwórz **Info.plist** pliku, przejdź do zbyt**typy adresu URL** w hello **zaawansowane** sekcji.</span><span class="sxs-lookup"><span data-stu-id="454d8-147">Open **Info.plist** file, navigate too**URL Types** in hello **Advanced** section.</span></span> <span data-ttu-id="454d8-148">Teraz skonfigurować hello **identyfikator** i hello **Schematy adresów URL** typ adresu URL i kliknij przycisk **Dodawanie adresu URL typu**.</span><span class="sxs-lookup"><span data-stu-id="454d8-148">Now configure hello **Identifier** and hello **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="454d8-149">**Schematy adresów URL** powinny być takie same hello jako Twoje {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="454d8-149">**URL Schemes** should be hello same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="454d8-150">W programie Visual Studio lub Xamarin Studio połączone tooyour Xamarin hosta kompilacji na komputerze Mac Uruchom projekt klienta hello przeznaczonych dla określonego urządzenia lub emulatora.</span><span class="sxs-lookup"><span data-stu-id="454d8-150">In Visual Studio or Xamarin Studio connected tooyour Xamarin Build Host on your Mac, run hello client project targeting a device or emulator.</span></span> <span data-ttu-id="454d8-151">Sprawdź, czy, aplikacja hello nie wyświetla żadnych danych.</span><span class="sxs-lookup"><span data-stu-id="454d8-151">Verify that hello app displays no data.</span></span>
   
    <span data-ttu-id="454d8-152">Wykonaj hello odświeżania gestu przez ściąganie hello listę elementów, które spowoduje, że tooappear ekranu logowania hello w dół.</span><span class="sxs-lookup"><span data-stu-id="454d8-152">Perform hello refresh gesture by pulling down hello list of items, which will cause hello login screen tooappear.</span></span> <span data-ttu-id="454d8-153">Po pomyślnie zostały wprowadzone prawidłowe poświadczenia, aplikacji hello zostaną wyświetlone powitalne Lista zadań do wykonania i można udostępnić dane toohello aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="454d8-153">Once you have successfully entered valid credentials, hello app will display hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[tworzenie aplikacji platformy Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md