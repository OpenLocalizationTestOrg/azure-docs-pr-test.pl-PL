---
title: "v2.0 usługi Active Directory aaaAzure natywnych aplikacji .NET | Dokumentacja firmy Microsoft"
description: "Jak toobuild natywnych aplikacji .NET który loguje się użytkowników z obu Account firmy Microsoft i konta firmowego lub szkolnego."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 46d81e09-bad0-44ce-9026-881805976e72
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/30/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 9418eeba02b800feee5cb00219574eb16506f0a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-desktop-app"></a>Dodaj tooa logowania w aplikacji Windows Desktop
Z punktem końcowym v2.0 hello hello można szybko dodać uwierzytelniania aplikacji klasycznych tooyour o obsługę zarówno osobistego konta Microsoft i konta służbowego.  On również umożliwia toosecurely Twojej aplikacji komunikować się z wewnętrznej bazy danych w sieci web interfejsu api, a także [hello Microsoft Graph](https://graph.microsoft.io) i kilka hello [Office 365 Unified API](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).

> [!NOTE]
> Nie wszystkie scenariusze Azure Active Directory (AD) i funkcji obsługiwanych przez hello punktu końcowego v2.0.  toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
> 
> 

Aby uzyskać [natywnych aplikacji .NET, na urządzeniu z systemem](active-directory-v2-flows.md#mobile-and-native-apps), usługa Azure AD zapewnia hello biblioteki uwierzytelniania tożsamości firmy Microsoft lub MSAL.  Jedynym celem MSAL jego życia jest toomake ułatwiają dla twojej aplikacji tooget tokeny wywoływania usługi sieci web.  toodemonstrate Ci, jak łatwo jest, w tym miejscu będzie budujemy aplikację listy zadań do wykonania WPF .NET który:

* Pobiera dostęp do tokenów przy użyciu hello & znaki hello użytkownika w [protokół uwierzytelniania OAuth 2.0](active-directory-v2-protocols.md).
* Bezpieczne wywołania wewnętrznej bazy danych usługi sieci web listy zadań do wykonania, która jest również chroniony przez OAuth 2.0.
* Znaki hello użytkownika.

## <a name="download-sample-code"></a>Pobierz przykładowy kod
Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).  toofollow wzdłuż, możesz [pobrać szkielet aplikacji hello jako .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) lub klonowania hello szkielet:

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

ukończyć powitalnych aplikacji znajduje się na końcu hello również w tym samouczku.

## <a name="register-an-app"></a>Rejestracja aplikacji
Utwórz nową aplikację na [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj następujące [szczegółowe kroki](active-directory-v2-app-registration.md).  Upewnij się, że:

* Skopiuj hello **identyfikator aplikacji** przypisany tooyour aplikacji, będzie on potrzebny wkrótce.
* Dodaj hello **Mobile** platformy aplikacji.

## <a name="install--configure-msal"></a>Instalowanie i konfigurowanie MSAL
Teraz, gdy masz aplikację w zarejestrowany z firmą Microsoft, można zainstalować MSAL i wpisz swój kod dotyczące tożsamości.  Aby dla punktu końcowego v2.0 hello MSAL toobe toocommunicate stanie, należy tooprovide go niektóre informacje o rejestracji aplikacji.

* Rozpocznij, dodając projektu TodoListClient toohello MSAL przy użyciu konsoli Menedżera pakietów hello.

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* W projekcie TodoListClient hello Otwórz `app.config`.  Zastąp wartości hello elementów hello na powitania `<appSettings>` hello tooreflect sekcji wartości danych wejściowych do portalu rejestracji aplikacji hello.  Kod będzie odwoływać tych wartości, przy każdym użyciu MSAL.
  
  * Witaj `ida:ClientId` jest hello **identyfikator aplikacji** skopiowany z portalu hello aplikacji.
* W projekcie hello listy zadań usługi, otwórz `web.config` w katalogu głównym hello hello projektu.  
  
  * Zastąp hello `ida:Audience` wartości z hello sam **identyfikator aplikacji** hello portalu.

## <a name="use-msal-tooget-tokens"></a>Używaj tokenów tooget MSAL
Witaj podstawową zasadą za MSAL jest zawsze, gdy Twoja aplikacja powinna tokenu dostępu, po prostu telefoniczne skontaktowanie się z `app.AcquireToken(...)`, i MSAL hello rest.  

* W hello `TodoListClient` otwarciu projektu `MainWindow.xaml.cs` i Znajdź hello `OnInitialized(...)` metody.  pierwszym krokiem Hello jest tooinitialize aplikacji `PublicClientApplication` -MSAL dla klasy podstawowej reprezentujący natywnych aplikacji.  Jest to, gdy przekazujesz MSAL hello współrzędne musi toocommunicate z usługą Azure AD i poinformuj go jak toocache tokenów.

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* Po uruchomieniu aplikacji hello, firma Microsoft ma toocheck i zobacz, jeśli użytkownik hello jest już zalogowany do aplikacji hello.  Jednak nie chcemy jeszcze tooinvoke interfejsu użytkownika logowania — wybierzemy hello użytkownika, kliknij przycisk "Zaloguj" toodo tak.  Również w hello `OnInitialized(...)` metody:

```C#
// As hello app starts, we want toocheck toosee if hello user is already signed in.
// You can do so by trying tooget a token from MSAL, using hello method
// AcquireTokenSilent.  This forces MSAL toothrow an exception if it cannot
// get a token for hello user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in hello cache - or MSAL was able tooget a new oen via refresh token.
    // Proceed toofetch hello user's tasks from hello TodoListService via hello GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, hello app should take no action,
        // and simply show hello user hello sign in button.
    }
    else
    {
        // Here, we catch all other MsalExceptions
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
}

```

* Jeśli hello użytkownik nie jest zalogowany i kliknięciu przycisku "Zaloguj" hello, firma Microsoft ma tooinvoke logowania interfejsu użytkownika i użytkownik hello wprowadzić swoje poświadczenia.  Implementowanie obsługi przycisk hello logowania:

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign hello user out if they clicked hello "Clear Cache" button

// If hello user clicked hello 'Sign-In' button, force
// MSAL tooprompt hello user for credentials by using
// AcquireTokenAsync, a method that is guaranteed tooshow a prompt toohello user.
// MSAL will get a token for hello TodoListService and cache it for you.

AuthenticationResult result = null;
try
{
    result = await app.AcquireTokenAsync(new string[] { clientId });
    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    // If MSAL cannot get a token, it will throw an exception.
    // If hello user canceled hello login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by hello user");
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }

        MessageBox.Show(message);
    }

    return;
}


}
```

* Jeśli hello pomyślnym zalogowaniu się użytkownika, MSAL będą odbierać i pamięci podręcznej tokenu i można kontynuować toocall hello `GetTodoList()` metody bez obaw.  Opuścił tooget zadań użytkownika jest tooimplement hello `GetTodoList()` metody.

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try tooget an access token toocall hello TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL toothrow an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show hello user a message
    // and let them click hello Sign-In button.

    if (ex.ErrorCode == "user_interaction_required")
    {
        MessageBox.Show("Please sign in first");
        SignInButton.Content = "Sign In";
    }
    else
    {
        // In any other case, an unexpected error occurred.

        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }

    return;
}

// Once hello token has been returned by MSAL,
// add it toohello http authorization header,
// before making hello call tooaccess hello tooDo list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When hello user is done managing their To-Do List, they may finally sign out of hello app by clicking hello "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If hello user clicked hello 'clear cache' button,
        // clear hello MSAL token cache and show hello user as signed out.
        // It's also necessary tooclear hello cookies from hello browser
        // control so hello next user has a chance toosign in.

        if (SignInButton.Content.ToString() == "Clear Cache")
        {
                TodoList.ItemsSource = string.Empty;
                app.UserTokenCache.Clear(app.ClientId);
                ClearCookies();
                SignInButton.Content = "Sign In";
                return;
        }

        ...
```

## <a name="run"></a>Uruchom polecenie
Gratulacje! Teraz mieć również działający w aplikacji .NET WPF, który ma hello możliwości tooauthenticate użytkowników i bezpiecznie wywoływać interfejsy API sieci Web przy użyciu protokołu OAuth 2.0.  Uruchom oba projekty i zaloguj się za pomocą osobistego konta Microsoft lub konta służbowego.  Dodawanie listy zadań do wykonania zadania toothat użytkownika.  Wyloguj się i zaloguj się ponownie jako inny użytkownik tooview ich listy zadań do wykonania.  Aplikacja hello Zamknij i uruchom je ponownie.  Zwróć uwagę, jak hello sesja pozostanie niezmieniona — to aplikacja hello buforuje tokenów w pliku lokalnym.

MSAL umożliwia łatwe tooincorporate wspólne funkcje tożsamości w aplikacji, za pomocą konta osobiste oraz firmowe.  Zapewnia obsługę wszystkich hello dirty pracy dla Ciebie — Zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający hello użytkownika za pomocą interfejsu użytkownika, odświeżanie wygaśnięcia tokenów i inne nazwy logowania.  Naprawdę tooknow wystarczy jednego wywołania interfejsu API, `app.AcquireTokenAsync(...)`.

Odwołania, hello ukończone próbka (bez wartości konfiguracji) [jest dostarczane jako zip w tym miejscu](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), lub można ją sklonować z serwisu GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a>Następne kroki
Możesz teraz przejść do bardziej zaawansowanych tematów.  Można tootry:

* [Zabezpieczanie hello TodoListService interfejsu API sieci Web z punktem końcowym v2.0 hello](active-directory-v2-devquickstarts-dotnet-api.md)

Aby uzyskać dodatkowe zasoby Zobacz:  

* [Przewodnik dewelopera v2.0 Hello >>](active-directory-appmodel-v2-overview.md)
* [Tag "msal" StackOverflow >>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a>Pobierz aktualizacje zabezpieczeń naszych produktów
Firma Microsoft zachęca tooget powiadomień o występujących incydentach zabezpieczeń poprzez wizytę [tę stronę](https://technet.microsoft.com/security/dd252948) i subskrypcji tooSecurity doradczych alertów.

