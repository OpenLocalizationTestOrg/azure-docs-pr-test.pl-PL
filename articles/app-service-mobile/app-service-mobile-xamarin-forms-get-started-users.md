---
title: aaaGet uruchomiono z uwierzytelniania dla aplikacji mobilnej w aplikacji platformy Xamarin Forms | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse Mobile Apps tooauthenticate użytkowników aplikacji platformy Xamarin Forms za pomocą różnych dostawców tożsamości, obejmującej AAD, Google, Facebook, Twitter i firmy Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: panarasi
manager: syntaxc4
editor: 
ms.assetid: 9c55e192-c761-4ff2-8d88-72260e9f6179
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: panarasi
ms.openlocfilehash: 7f6716619f33d9cc4f866c41effba8f048dc49fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarin-forms-app"></a>Dodaj aplikację platformy Xamarin Forms tooyour uwierzytelniania
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a>Omówienie
W tym temacie opisano sposób tooauthenticate użytkowników aplikację usługi Mobile aplikacji z poziomu aplikacji klienta. W tym samouczku Dodawanie uwierzytelniania do projektu szybkiego startu Xamarin Forms hello przy użyciu dostawcy tożsamości, która jest obsługiwana przez usługę App Service. Po pomyślnie trwa uwierzytelnieniu i autoryzacji w aplikacji mobilnej, jest wyświetlana wartość Identyfikatora użytkownika hello i będą mogli tooaccess ograniczone tabeli danych.

## <a name="prerequisites"></a>Wymagania wstępne
Witaj najlepszych wyników z tego samouczka, zaleca się wykonanie hello [tworzenie aplikacji platformy Xamarin Forms] [ 1] samouczka. Po ukończeniu tego samouczka, konieczne będzie projektu Xamarin Forms aplikacji TodoList wielu platform.

Jeśli nie używasz hello pobrany Projekt serwera szybki start, należy dodać projekt tooyour hello uwierzytelniania rozszerzenie pakietu. Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps][2].

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>Zarejestrować aplikację do uwierzytelniania i konfigurowanie usługi aplikacji
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Dodaj adresy URL przekierowania zewnętrznych dozwolone Twojej aplikacji toohello

Bezpieczne uwierzytelnianie wymaga Zdefiniuj nowy schemat adresu URL dla aplikacji. Po zakończeniu procesu uwierzytelniania hello dzięki temu hello uwierzytelniania systemu tooredirect wstecz tooyour aplikacji. W tym samouczku używamy schemat adresu URL hello _appname_ w ciągu. Można jednak użyć dowolnego wybranego schematu URL. Powinna być unikatowa tooyour aplikacji mobilnej. Przekierowanie hello tooenable na powitania po stronie serwera:

1. W hello [portalu Azure] wybierz usługę aplikacji.

2. Kliknij przycisk hello **uwierzytelniania / autoryzacji** opcji menu.

3. W hello **dozwolone zewnętrznych adresów URL przekierowań**, wprowadź `url_scheme_of_your_app://easyauth.callback`.  Witaj **url_scheme_of_your_app** w tym ciągu jest hello schemat adresu URL aplikacji mobilnej.  Musi on być zgodny normalne Specyfikacja adresu URL dla protokołu (Użyj litery i tylko cyfry i rozpoczyna się od litery).  Należy zanotuj ciąg hello, który możesz wybrać, ponieważ będzie potrzebny tooadjust kodu aplikacji mobilnej przy użyciu hello schemat adresu URL w kilku miejscach.

4. Kliknij przycisk **OK**.

5. Kliknij pozycję **Zapisz**.

## <a name="restrict-permissions-tooauthenticated-users"></a>Ogranicz uprawnienia tooauthenticated użytkowników
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a>Dodawanie biblioteki klas przenośnych toohello uwierzytelniania
Aplikacje mobilne używa hello [LoginAsync] [ 3] — metoda rozszerzenia na powitania [MobileServiceClient] [ 4] toosign użytkownika z usługi aplikacji uwierzytelnianie. W przykładzie użyto przepływ uwierzytelniania serwer zarządzany, który wyświetla dostawcy hello w interfejsie logowania w aplikacji hello. Aby uzyskać więcej informacji, zobacz [serwer zarządzany uwierzytelniania][5]. Aby zapewnić lepsze środowisko użytkownika w aplikacji produkcyjnej, należy rozważyć zamiast za pomocą [zarządzanych przez klienta uwierzytelniania][6].

Zdefiniuj tooauthenticate z projektem Xamarin Forms **IAuthenticate** interfejsu w hello przenośnej biblioteki klas dla aplikacji hello. Następnie dodaj **logowania** interfejsu użytkownika toohello przycisk zdefiniowane w hello przenośną bibliotekę klas, którego kliknięcie toostart uwierzytelniania. Dane są ładowane z zaplecza aplikacji mobilnej powitania po pomyślnym uwierzytelnieniu.

Implementowanie hello **IAuthenticate** interfejs dla każdej platformy obsługiwane przez aplikację.

1. W programie Visual Studio lub Xamarin Studio Otwórz App.cs z projektu hello z **przenośne** w polu Nazwa hello jest projektu biblioteki przenośnej klasy, a następnie dodaj następujące hello `using` instrukcji:

        using System.Threading.Tasks;
2. W App.cs, Dodaj następujące hello `IAuthenticate` definicji bezpośrednio przed hello interfejsu `App` definicji klasy.

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. Interfejs hello tooinitialize z implementacją specyficzne dla platformy, Dodaj powitania po toohello statyczne elementy członkowskie **aplikacji** klasy.

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. Otwórz TodoList.xaml z projektu biblioteki klas przenośnych hello, Dodaj następujące hello **przycisk** element hello *buttonsPanel* elementu układu po istniejącego przycisku hello:

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    Ten przycisk wyzwala serwer zarządzany uwierzytelniania za pomocą zaplecza aplikacji mobilnej.
5. Otwórz TodoList.xaml.cs z projektu biblioteki klas przenośnych hello, a następnie dodaj następujące pola toohello hello `TodoList` klasy:

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. Zastąp hello **OnAppearing** metody z hello następującego kodu:

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems tootrue in order toosynchronize hello data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide hello Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    Ten kod upewnia się, że tylko odświeżania danych z usługi powitania po Cię uwierzytelniono.
7. Dodaj powitania po obsługę hello **kliknięto element** toohello zdarzeń **TodoList** klasy:

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. Zapisz zmiany i skompiluj ponownie projektu biblioteki klas przenośnych hello weryfikowanie żadne błędy.

## <a name="add-authentication-toohello-android-app"></a>Dodawanie aplikacji dla systemu Android toohello uwierzytelniania
W tej sekcji przedstawiono sposób tooimplement hello **IAuthenticate** interfejs w projekcie aplikacji systemu Android hello. Pomiń tę sekcję, jeśli urządzenia z systemem Android nie są obsługiwane.

1. W programie Visual Studio lub Xamarin Studio kliknij prawym przyciskiem myszy hello **droid** projektu, następnie **Ustaw jako projekt startowy**.
2. Naciśnij klawisz F5 toostart hello projektu w debugerze hello, a następnie sprawdź, czy wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji. Kod 401 Hello jest generowany, ponieważ dostęp hello wewnętrznej bazy danych jest tylko użytkownicy tooauthorized ograniczone.
3. Otwórz MainActivity.cs w hello projekt systemu Android i dodaj następujące hello `using` instrukcji:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. Aktualizacja hello **MainActivity** hello tooimplement klasy **IAuthenticate** interfejsu, w następujący sposób:

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. Aktualizacja hello **MainActivity** klasy, dodając **MobileServiceUser** pola i **Uwierzytelnij** metodę, która jest wymagana przez hello **IAuthenticate ** interfejsu, w następujący sposób:

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                user = await TodoItemManager.DefaultManager.CurrentClient.LoginAsync(this, 
                    MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                if (user != null)
                {
                    message = string.Format("you are now signed-in as {0}.",
                        user.UserId);
                    success = true;
                }
            }
            catch (Exception ex)
            {
                message = ex.Message;
            }

            // Display hello success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    Jeśli używasz dostawcy tożsamości innego niż usługi Facebook, wybierz inną wartość dla [MobileServiceAuthenticationProvider][7].

6. Dodaj następujące kodu wewnątrz hello <application> węzła AndroidManifest.xml:

```xml
    <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
      <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
      </intent-filter>
    </activity>
```

1. Dodaj hello następującego kodu toohello **OnCreate** metody hello **MainActivity** klasy przed wywołaniem hello zbyt`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    Ten kod gwarantuje, że wystawca uwierzytelnienia hello jest inicjowana przed obciążeń aplikacji hello.
2. Odbuduj aplikacji hello, uruchom go, a następnie zaloguj się przy użyciu dostawcy uwierzytelniania hello wybranego i sprawdź, czy są możliwe tooaccess danych jako użytkownik uwierzytelniony.

## <a name="add-authentication-toohello-ios-app"></a>Dodawanie aplikacji dla systemu iOS toohello uwierzytelniania
W tej sekcji przedstawiono sposób tooimplement hello **IAuthenticate** interfejs w projekcie aplikacji systemu iOS hello. Pomiń tę sekcję, jeśli urządzenia z systemem iOS nie są obsługiwane.

1. W programie Visual Studio lub Xamarin Studio kliknij prawym przyciskiem myszy hello **iOS** projektu, następnie **Ustaw jako projekt startowy**.
2. Naciśnij klawisz F5 toostart hello projektu w debugerze hello, a następnie sprawdź, czy wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji hello. odpowiedzi 401 Hello jest generowany, ponieważ dostęp hello wewnętrznej bazy danych jest tylko użytkownicy tooauthorized ograniczone.
3. Otwórz AppDelegate.cs w projekcie systemu iOS hello i dodaj następujące hello `using` instrukcji:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. Aktualizacja hello **AppDelegate** hello tooimplement klasy **IAuthenticate** interfejsu, w następujący sposób:

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. Aktualizacja hello **AppDelegate** klasy, dodając **MobileServiceUser** pola i **Uwierzytelnij** metodę, która jest wymagana przez hello **IAuthenticate ** interfejsu, w następujący sposób:

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(UIApplication.SharedApplication.KeyWindow.RootViewController,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                        success = true;
                    }
                }
            }
            catch (Exception ex)
            {
               message = ex.Message;
            }

            // Display hello success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    Jeśli używasz dostawcy tożsamości innego niż usługi Facebook, wybierz inną wartość dla [MobileServiceAuthenticationProvider].

6. Aktualizacja klasy AppDelegate hello przez dodanie przeciążenie metody OpenUrl (Opcje NSDictionary aplikacji, nsurl oczekiwanego adresu url, UIApplication)

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. Dodaj powitania po wierszu kodu toohello **FinishedLaunching** za wywołanie metody przed hello`LoadApplication()`:

        App.Init(this);

    Ten kod gwarantuje, że wystawca uwierzytelnienia hello jest zainicjowany przed załadowaniem aplikacji hello.

6. Dodaj **{url_scheme_of_your_app}** tooURL programów w pliku Info.plist.

7. Odbuduj aplikacji hello, uruchom go, a następnie zaloguj się przy użyciu dostawcy uwierzytelniania hello wybranego i sprawdź, czy są możliwe tooaccess danych jako użytkownik uwierzytelniony.

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a>Dodawanie uwierzytelniania tooWindows 10 (takie jak telefon) projekty aplikacji
W tej sekcji przedstawiono sposób tooimplement hello **IAuthenticate** interfejsu w projektach aplikacji hello systemu Windows 10. Zastosuj te same czynności dla projektów uniwersalnych platformy systemu Windows (UWP), ale przy użyciu hello Hello **platformy uniwersalnej systemu Windows** projektu (ze zmianami dostrzeżone). Pomiń tę sekcję, jeśli urządzenia z systemem Windows nie są obsługiwane.

1. "W programie Visual Studio, kliknij prawym przyciskiem myszy albo hello **UWP** projektu, następnie **Ustaw jako projekt startowy**.
2. Naciśnij klawisz F5 toostart hello projektu w debugerze hello, a następnie sprawdź, czy wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji hello. odpowiedzi 401 Hello odbywa się, ponieważ dostęp hello wewnętrznej bazy danych jest ograniczone tooauthorized tylko użytkownicy.
3. Otwórz MainPage.xaml.cs dla projektu aplikacji Windows hello i dodaj następujące hello `using` instrukcji:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    Zastąp `<your_Portable_Class_Library_namespace>` z przestrzenią nazw hello biblioteki klas przenośnych.
4. Aktualizacja hello **MainPage** hello tooimplement klasy **IAuthenticate** interfejsu, w następujący sposób:

        public sealed partial class MainPage : IAuthenticate
5. Aktualizacja hello **MainPage** klasy, dodając **MobileServiceUser** pola i **Uwierzytelnij** metodę, która jest wymagana przez hello **IAuthenticate** interfejsu, w następujący sposób:

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            string message = string.Empty;
            var success = false;

            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        success = true;
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                    }
                }

            }
            catch (Exception ex)
            {
                message = string.Format("Authentication Failed: {0}", ex.Message);
            }

            // Display hello success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    Jeśli używasz dostawcy tożsamości innego niż usługi Facebook, wybierz inną wartość dla [MobileServiceAuthenticationProvider].

1. Dodaj następującego wiersza kodu w Konstruktorze hello hello hello **MainPage** klasy przed wywołaniem hello zbyt`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    Zastąp `<your_Portable_Class_Library_namespace>` z przestrzenią nazw hello biblioteki klas przenośnych.

3. Jeśli używasz **platformy uniwersalnej systemu Windows**, Dodaj następujące hello **OnActivated** metoda przesłania toohello **aplikacji** klasy:

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   Zastąpienie metody hello już istnieje, należy dodać kodu warunkowego hello z hello poprzedzających fragment.  Ten kod nie jest wymagane dla projektów uniwersalnych systemu Windows.

3. Dodaj **{url_scheme_of_your_app}** w Package.appxmanifest. 

4. Odbuduj aplikacji hello, uruchom go, a następnie zaloguj się przy użyciu dostawcy uwierzytelniania hello wybranego i sprawdź, czy są możliwe tooaccess danych jako użytkownik uwierzytelniony.

## <a name="next-steps"></a>Następne kroki
Teraz, aby ukończyć w tym samouczku uwierzytelnianie podstawowe, należy wziąć pod uwagę kontynuować tooone hello następujące samouczki:

* [Dodaj aplikację tooyour powiadomień wypychanych](app-service-mobile-xamarin-forms-get-started-push.md)

  Dowiedz się, jak powiadomień wypychanych tooadd obsługują tooyour aplikacji i Konfigurowanie powiadomień wypychanych toosend usługi Azure Notification Hubs toouse aplikacji mobilnej wewnętrznej bazy danych.
* [Włączanie synchronizacji w trybie offline dla aplikacji](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  Dowiedz się, jak w trybie offline tooadd obsługują aplikację przy użyciu zaplecza aplikacji mobilnej. Synchronizacja w trybie offline umożliwia toointeract użytkowników końcowych z aplikacji mobilnej — przeglądanie, dodawanie lub modyfikowanie danych — nawet wtedy, gdy istnieje połączenie sieciowe.

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
