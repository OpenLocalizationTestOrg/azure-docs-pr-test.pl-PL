---
title: Aplikacja systemu Windows platformy Uniwersalnej tooyour authentication aaaAdd | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse Azure App Service Mobile Apps tooauthenticate użytkowników aplikacji systemu Windows platformy Uniwersalnej przy użyciu różnych dostawców tożsamości, obejmującej: usługi AAD, Google, Facebook, Twitter i firmy Microsoft."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: ad4477e9509f1c40c33e71818e268f6857fe1e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-windows-app"></a><span data-ttu-id="a70ea-103">Dodawanie aplikacji dla systemu Windows tooyour uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="a70ea-103">Add authentication tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="a70ea-104">W tym temacie opisano sposób tooadd aplikacji mobilnej tooyour uwierzytelniania opartego na chmurze.</span><span class="sxs-lookup"><span data-stu-id="a70ea-104">This topic shows you how tooadd cloud-based authentication tooyour mobile app.</span></span> <span data-ttu-id="a70ea-105">W tym samouczku możesz dodać projekt szybkiego startu Windows platformy Uniwersalnej toohello uwierzytelniania aplikacji mobilnej przy użyciu dostawcy tożsamości, która jest obsługiwana przez usługę Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a70ea-105">In this tutorial, you add authentication toohello Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="a70ea-106">Po pomyślnym są uwierzytelnieni i upoważnieni przez zaplecza aplikacji mobilnej, wartość Identyfikatora użytkownika hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="a70ea-106">After being successfully authenticated and authorized by your Mobile App backend, hello user ID value is displayed.</span></span>

<span data-ttu-id="a70ea-107">W tym samouczku jest oparta na powitania Mobile Apps — Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="a70ea-107">This tutorial is based on hello Mobile Apps quickstart.</span></span> <span data-ttu-id="a70ea-108">Najpierw musisz zakończyć samouczek hello [Rozpoczynanie pracy z usługą Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a70ea-108">You must first complete hello tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="a70ea-109"><a name="register"></a>Zarejestrować aplikację do uwierzytelniania i skonfigurować hello usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="a70ea-109"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="a70ea-110"><a name="redirecturl"></a>Dodaj adresy URL przekierowania zewnętrznych dozwolone Twojej aplikacji toohello</span><span class="sxs-lookup"><span data-stu-id="a70ea-110"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="a70ea-111">Bezpieczne uwierzytelnianie wymaga Zdefiniuj nowy schemat adresu URL dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a70ea-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="a70ea-112">Po zakończeniu procesu uwierzytelniania hello dzięki temu hello uwierzytelniania systemu tooredirect wstecz tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a70ea-112">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="a70ea-113">W tym samouczku używamy schemat adresu URL hello _appname_ w ciągu.</span><span class="sxs-lookup"><span data-stu-id="a70ea-113">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="a70ea-114">Można jednak użyć dowolnego wybranego schematu URL.</span><span class="sxs-lookup"><span data-stu-id="a70ea-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="a70ea-115">Powinna być unikatowa tooyour aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="a70ea-115">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="a70ea-116">Przekierowanie hello tooenable na powitania po stronie serwera:</span><span class="sxs-lookup"><span data-stu-id="a70ea-116">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="a70ea-117">W hello [portalu Azure] wybierz usługę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a70ea-117">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="a70ea-118">Kliknij przycisk hello **uwierzytelniania / autoryzacji** opcji menu.</span><span class="sxs-lookup"><span data-stu-id="a70ea-118">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="a70ea-119">W hello **dozwolone zewnętrznych adresów URL przekierowań**, wprowadź `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="a70ea-119">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="a70ea-120">Witaj **url_scheme_of_your_app** w tym ciągu jest hello schemat adresu URL aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="a70ea-120">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="a70ea-121">Musi on być zgodny normalne Specyfikacja adresu URL dla protokołu (Użyj litery i tylko cyfry i rozpoczyna się od litery).</span><span class="sxs-lookup"><span data-stu-id="a70ea-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="a70ea-122">Należy zanotuj ciąg hello, który możesz wybrać, ponieważ będzie potrzebny tooadjust kodu aplikacji mobilnej przy użyciu hello schemat adresu URL w kilku miejscach.</span><span class="sxs-lookup"><span data-stu-id="a70ea-122">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="a70ea-123">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a70ea-123">Click **OK**.</span></span>

5. <span data-ttu-id="a70ea-124">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a70ea-124">Click **Save**.</span></span>

## <span data-ttu-id="a70ea-125"><a name="permissions"></a>Ogranicz uprawnienia tooauthenticated użytkowników</span><span class="sxs-lookup"><span data-stu-id="a70ea-125"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="a70ea-126">Teraz możesz sprawdzić, czy ten dostęp anonimowy tooyour wewnętrznej bazy danych została wyłączona.</span><span class="sxs-lookup"><span data-stu-id="a70ea-126">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="a70ea-127">Ustaw jako projekt uruchamiania hello projektu aplikacji platformy uniwersalnej systemu Windows hello wdrażanie i uruchamianie aplikacji hello; Upewnij się, że wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a70ea-127">With hello UWP app project set as hello start-up project, deploy and run hello app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="a70ea-128">Dzieje się tak, ponieważ aplikacja hello prób tooaccess kodu aplikacji mobilnej jako nieuwierzytelniony użytkownik, ale hello *TodoItem* tabeli teraz wymaga uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a70ea-128">This happens because hello app attempts tooaccess your Mobile App Code as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="a70ea-129">Następnie zaktualizuje użytkownicy tooauthenticate aplikacji hello przed wysłaniem żądania zasobów z usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a70ea-129">Next, you will update hello app tooauthenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="a70ea-130"><a name="add-authentication"></a>Dodaj aplikację toohello uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="a70ea-130"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="a70ea-131">W projekcie aplikacji platformy uniwersalnej systemu Windows hello pliku MainPage.xaml.cs i Dodaj hello następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="a70ea-131">In hello UWP app project file MainPage.xaml.cs and add hello following code snippet:</span></span>
   
        // Define a member variable for storing hello signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs hello authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' toohello name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    <span data-ttu-id="a70ea-132">Ten kod uwierzytelnia użytkownika hello za pomocą nazwy logowania usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="a70ea-132">This code authenticates hello user with a Facebook login.</span></span> <span data-ttu-id="a70ea-133">Jeśli używasz dostawcy tożsamości innego niż usługi Facebook, zmień wartość hello **MobileServiceAuthenticationProvider** większa niż wartość toohello przez dostawcę.</span><span class="sxs-lookup"><span data-stu-id="a70ea-133">If you are using an identity provider other than Facebook, change hello value of **MobileServiceAuthenticationProvider** above toohello value for your provider.</span></span>
2. <span data-ttu-id="a70ea-134">Zastąp hello **OnNavigatedTo()** metody w MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="a70ea-134">Replace hello **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="a70ea-135">Następnie należy dodać **Zaloguj** przycisk toohello aplikacji, które wyzwala uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a70ea-135">Next, you will add a **Sign in** button toohello app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="a70ea-136">Dodaj następujące toohello fragment kodu MainPage.xaml.cs hello:</span><span class="sxs-lookup"><span data-stu-id="a70ea-136">Add hello following code snippet toohello MainPage.xaml.cs:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login hello user and then load data from hello mobile app.
            if (await AuthenticateAsync())
            {
                // Switch hello buttons and load items from hello mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="a70ea-137">Otwórz plik projektu MainPage.xaml hello, zlokalizować hello elementu, który definiuje hello **zapisać** przycisk i zastąp go hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="a70ea-137">Open hello MainPage.xaml project file, locate hello element that defines hello **Save** button and replace it with hello following code:</span></span>
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. <span data-ttu-id="a70ea-138">Dodaj następujące toohello fragment kodu App.xaml.cs hello:</span><span class="sxs-lookup"><span data-stu-id="a70ea-138">Add hello following code snippet toohello App.xaml.cs:</span></span>

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. <span data-ttu-id="a70ea-139">Otwórz plik Package.appxmanifest, przejdź do zbyt**deklaracje**w **dostępne deklaracje** listy rozwijanej wybierz **protokołu** i kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a70ea-139">Open Package.appxmanifest file, navigate too**Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="a70ea-140">Teraz skonfigurować hello **właściwości** z hello **protokołu** deklaracji.</span><span class="sxs-lookup"><span data-stu-id="a70ea-140">Now configure hello **Properties** of hello **Protocol** declaration.</span></span> <span data-ttu-id="a70ea-141">W **Nazwa wyświetlana**, Dodaj nazwę hello mają toousers toodisplay aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a70ea-141">In **Display name**, add hello name you wish toodisplay toousers of your application.</span></span> <span data-ttu-id="a70ea-142">W **nazwa**, Dodaj użytkownika {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="a70ea-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="a70ea-143">Naciśnij klawisz hello F5 klucza toorun hello aplikacji, kliknij przycisk hello **Zaloguj** przycisk i zaloguj się do aplikacji hello u dostawcy tożsamości wybrany.</span><span class="sxs-lookup"><span data-stu-id="a70ea-143">Press hello F5 key toorun hello app, click hello **Sign in** button, and sign into hello app with your chosen identity provider.</span></span> <span data-ttu-id="a70ea-144">Po logowanie zakończy się pomyślnie, aplikacja hello jest uruchamiana bez błędów i możesz są możliwe tooquery z wewnętrzną bazą danych i toodata aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="a70ea-144">After your sign-in is successful, hello app runs without errors and you are able tooquery your backend and make updates toodata.</span></span>

## <span data-ttu-id="a70ea-145"><a name="tokens"></a>Token uwierzytelniania hello magazynu na powitania klienta</span><span class="sxs-lookup"><span data-stu-id="a70ea-145"><a name="tokens"></a>Store hello authentication token on hello client</span></span>
<span data-ttu-id="a70ea-146">Hello w poprzednim przykładzie pokazano standardowe logowania, która wymaga powitania klienta toocontact zarówno hello dostawcy tożsamości i hello App Service w każdym uruchomieniu danej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a70ea-146">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello App Service every time that hello app starts.</span></span> <span data-ttu-id="a70ea-147">Nie tylko jest nieefektywne, można uruchomić tej metody do użycia — odnosi się problemy z wielu klientów Wypróbuj toostart aplikacji na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="a70ea-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try toostart you app at hello same time.</span></span> <span data-ttu-id="a70ea-148">Lepszym rozwiązaniem jest token autoryzacji hello toocache zwracane w aplikacji usługi, a następnie spróbuj toouse to najpierw przed przy użyciu opartych na dostawcy logowania.</span><span class="sxs-lookup"><span data-stu-id="a70ea-148">A better approach is toocache hello authorization token returned by your App Service and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="a70ea-149">Może buforować hello token wystawiony przez usługi aplikacji niezależnie od tego, czy używasz zarządzanych przez klienta lub zarządzane przez usługę uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a70ea-149">You can cache hello token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="a70ea-150">W tym samouczku korzysta z zarządzanymi przez usługę uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a70ea-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="a70ea-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a70ea-151">Next steps</span></span>
<span data-ttu-id="a70ea-152">Teraz, aby ukończyć w tym samouczku uwierzytelnianie podstawowe, należy wziąć pod uwagę kontynuować tooone hello następujące samouczki:</span><span class="sxs-lookup"><span data-stu-id="a70ea-152">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="a70ea-153">Dodaj aplikację tooyour powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="a70ea-153">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="a70ea-154">Dowiedz się, jak powiadomień wypychanych tooadd obsługują tooyour aplikacji i Konfigurowanie powiadomień wypychanych toosend usługi Azure Notification Hubs toouse aplikacji mobilnej wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a70ea-154">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="a70ea-155">Włączanie synchronizacji w trybie offline dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="a70ea-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="a70ea-156">Dowiedz się, jak w trybie offline tooadd obsługują aplikację przy użyciu zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="a70ea-156">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="a70ea-157">Synchronizacja w trybie offline umożliwia użytkownikom końcowym toointeract z aplikacją mobilną&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.</span><span class="sxs-lookup"><span data-stu-id="a70ea-157">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
