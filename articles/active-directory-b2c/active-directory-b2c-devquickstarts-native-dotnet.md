---
title: aaaAzure Active Directory B2C | Dokumentacja firmy Microsoft
description: "Jak toobuild aplikacji pulpitu systemu Windows który obejmuje logowania, rejestracji i profilu zarządzania przy użyciu usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: f22b0299ff74bfba2f3fea88f006da609859dda5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a>Usługa Azure AD B2C: Tworzenie aplikacji klasycznej systemu Windows
Za pomocą usługi Azure Active Directory (Azure AD) B2C, można dodawać tożsamości samoobsługi zaawansowane funkcje tooyour pulpitu aplikacji do zarządzania w kilku krótkich krokach. W tym artykule opisano, jak toocreate aplikacji .NET systemu Windows Presentation Foundation (WPF) "Lista zadań do wykonania", który zawiera użytkownika rejestrację, logowanie i zarządzanie profilami. Aplikacja Hello obejmuje obsługę rejestracji i logowania przy użyciu nazwy użytkownika lub adres e-mail. Zawiera również obsługę rejestracji i logowania przy użyciu kont społecznościowych, takich jak Facebook i Google.

## <a name="get-an-azure-ad-b2c-directory"></a>Tworzenie katalogu usługi Azure AD B2C
Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę.  Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i innych elementów. Jeśli jeszcze go nie masz, [utwórz katalog usługi B2C](active-directory-b2c-get-started.md), zanim przejdziesz dalej.

## <a name="create-an-application"></a>Tworzenie aplikacji
Następnie należy toocreate aplikację w katalogu usługi B2C. Dzięki temu informacje usługi Azure AD, czy go wymaga toosecurely komunikować się z aplikacją. toocreate usługi aplikacji, wykonaj [tych instrukcji](active-directory-b2c-app-registration.md).  Należy pamiętać o wykonaniu następujących czynności:

* Obejmują **klientami** w aplikacji hello.
* Kopiuj hello **identyfikator URI przekierowania** `urn:ietf:wg:oauth:2.0:oob`. Jest hello domyślny adres URL dla tego przykładu kodu.
* Kopiuj hello **identyfikator aplikacji** czyli przypisanej tooyour aplikacji. Będzie potrzebny później.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Tworzenie zasad
W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md). Ten przykładowy kod obejmuje trzy środowiska tożsamości: Zarejestruj się, zaloguj się i edytowanie profilu. Należy dla każdego typu toocreate zasady zgodnie z opisem w [artykule o zasadach](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Podczas tworzenia hello trzech zbiorów zasad należy koniecznie:

* Wybierz **identyfikator użytkownika rejestracji** lub **tworzenia konta E-mail** w bloku dostawców tożsamości hello.
* Wybrać wartość **Nazwa wyświetlana** i inne atrybuty tworzenia konta w zasadach tworzenia konta.
* Wybrać oświadczenia **Nazwa wyświetlana** i **Identyfikator obiektu** jako oświadczenia aplikacji dla wszystkich zasad. Można również wybrać inne oświadczenia.
* Kopiuj hello **nazwa** poszczególnych zasad po jego utworzeniu. Powinien on mieć prefiks hello `b2c_1_`.  Te nazwy zasad będą potrzebne później.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Po pomyślnym utworzeniu hello trzy zasady, wszystko jest gotowe toobuild aplikacji.

## <a name="download-hello-code"></a>Pobierz kod hello
Witaj kodu w tym samouczku [jest przechowywany w serwisie GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet). Przykładowe hello toobuild podczas przejść, możesz [pobrać szkielet projektu jako plik .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip). Można również sklonować szkielet hello:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

Aplikacja Hello ukończone jest również [dostępny jako plik zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) lub na powitania `complete` gałęzi hello tego samego repozytorium.

Po pobraniu hello przykładowy kod tooget plik SLN programu Visual Studio Otwórz hello jest uruchomiona. Witaj `TaskClient` projekt jest hello WPF aplikacja komputerowa, która hello użytkownik wchodzi w interakcję z. Do celów tego samouczka hello wywołuje zadań zaplecza interfejsu API sieci web, hostowana na platformie Azure, która przechowuje listy zadań do wykonania poszczególnych użytkowników.  Nie trzeba interfejsu API sieci web hello toobuild, mamy już będzie działać dla Ciebie.

toolearn jak bezpiecznie interfejsu API sieci web uwierzytelnia żądania przy użyciu usługi Azure AD B2C, zapoznaj się z [interfejsu API sieci web wprowadzenie artykułu](active-directory-b2c-devquickstarts-api-dotnet.md).

## <a name="execute-policies"></a>Zasady wykonywania
Aplikacja komunikuje się z usługi Azure AD B2C przez wysyłanie komunikatów uwierzytelniania, określających zasady hello mają tooexecute jako część żądania hello HTTP. Aplikacje .NET, można użyć hello Podgląd komunikatów uwierzytelniania OAuth 2.0 toosend biblioteki uwierzytelniania firmy Microsoft (MSAL), wykonaj zasad i uzyskiwać tokeny tego wywołania interfejsów API sieci web.

### <a name="install-msal"></a>Zainstaluj MSAL
Dodaj MSAL toohello `TaskClient` projektu przy użyciu hello Konsola Menedżera pakietów programu Visual Studio.

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a>Wprowadzanie szczegółów B2C
Witaj Otwórz plik `Globals.cs` i Zastąp wartości właściwości hello własne. Ta klasa jest używana w całym `TaskClient` tooreference najczęściej używanych wartości.

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-hello-publicclientapplication"></a>Utwórz hello PublicClientApplication
podstawowy klasa MSAL Hello jest `PublicClientApplication`. Ta klasa reprezentuje aplikacji w systemie hello Azure AD B2C. Gdy hello initalizes aplikacji, Utwórz wystąpienie `PublicClientApplication` w `MainWindow.xaml.cs`. Można to w całym hello okna.

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens toopersist when hello user closes hello app,
        // we've extended hello MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a>Inicjowanie przepływu rejestracji
Gdy użytkownik zażąda toosigns w górę, ma tooinitiate rejestracji przepływ, który korzysta z utworzonymi zasadami hello rejestracji. Za pomocą MSAL, możesz po prostu Wywołaj `pca.AcquireTokenAsync(...)`. Witaj parametry przekazywane za`AcquireTokenAsync(...)` ustalić, które token zostanie wyświetlony, używane w hello żądań uwierzytelnienia i inne zasady hello.

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use hello app's clientId here as hello scope parameter, indicating that
        // you want a token toohello your app's backend web API (represented by
        // hello cloud hosted task API).  Use hello UiOptions.ForceLogin flag to
        // indicate tooMSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in hello app that hello user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When hello request completes successfully, you can get user
        // information from hello AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After hello sign up successfully completes, display hello user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of hello policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
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

### <a name="initiate-a-sign-in-flow"></a>Inicjowanie przepływu logowania
Możesz zainicjować przepływ logowania w hello taki sam sposób, że zainicjować przepływ rejestracji. Gdy użytkownik się zaloguje, upewnij się, hello same wywołać tooMSAL, teraz za pomocą zasad logowania:

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a>Zainicjować przepływ edycji profilu
Ponownie, możesz wykonać zasad edycji profilu w hello sam sposób:

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

We wszystkich tych przypadkach MSAL albo zwraca token w `AuthenticationResult` lub zgłasza wyjątek. Zawsze uzyskać token z MSAL, można użyć hello `AuthenticationResult.User` obiekt tooupdate hello użytkownika danych w aplikacji hello, takie jak hello interfejsu użytkownika. ADAL również pamięci podręcznych hello token do użycia w innych częściach aplikacji hello.

### <a name="check-for-tokens-on-app-start"></a>Sprawdź, czy tokeny przy uruchamianiu aplikacji
Umożliwia także śledzenie tookeep MSAL hello użytkownika logowania stanu.  W tej aplikacji chcemy hello tooremain użytkownik zalogowany nawet po aplikacji hello Zamknij i otwórz go ponownie.  Ponownie wewnątrz hello `OnInitialized` zastąpienia, należy użyć w MSAL `AcquireTokenSilent` toocheck — metoda pamięci podręcznej tokenów:

```C#
AuthenticationResult result = null;
try
{
    // If hello user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in hello cache.  Proceed without calling hello tooDo list service.
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
```

## <a name="call-hello-task-api"></a>Wywołanie interfejsu API zadań hello
Teraz używanych MSAL tooexecute zasad i uzyskać tokeny.  Toouse jednego interfejsu API te tokeny toocall hello zadań, należy ponownie można użyć w MSAL `AcquireTokenSilent` toocheck — metoda pamięci podręcznej tokenów:

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want toocheck for a cached token, independent of whatever policy was used tooacquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent tooindicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch hello exception and show hello user a message.
    catch (MsalException ex)
    {
        // There is no access token in hello cache, so prompt hello user toosign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
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
    ...
```

Gdy hello wywołanie za`AcquireTokenSilentAsync(...)` zakończy się pomyślnie i token znajduje się w pamięci podręcznej hello, możesz dodać hello token toohello `Authorization` nagłówka żądania hello HTTP. Hello interfejsu API sieci web zadania będą korzystać z listy zadań do wykonania tego nagłówka tooauthenticate hello żądania tooread hello użytkownika:

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a>Witaj logowania użytkownika
Ponadto można użyć MSAL tooend sesji użytkownika z aplikacją hello po wybraniu użytkownika hello **Wyloguj**.  Korzystając z MSAL, jest to osiągane przez wyczyszczenie wszystkich tokenów hello z pamięci podręcznej tokenu hello:

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of hello user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in hello browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update hello UI tooshow hello user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-hello-sample-app"></a>Uruchom hello przykładowej aplikacji
Na koniec Skompiluj i uruchom próbkę hello.  Załóż aplikacji hello przy użyciu nazwa użytkownika lub adres e-mail. Wyloguj się i zaloguj się ponownie jako hello sam użytkownika. Edytuj profil użytkownika. Wyloguj się i zaloguj przy użyciu innego użytkownika.

## <a name="add-social-idps"></a>Dodaj IDPs społecznościowych
Obecnie aplikacji hello obsługuje tylko użytkownika rejestracji i logowania używanego **kont lokalnych**. Oto konta przechowywane w katalogu usługi B2C, korzystających z nazwy użytkownika i hasła. Za pomocą usługi Azure AD B2C, można dodać obsługę innych dostawców tożsamości (IDPs) bez zmieniania żadnego kodu.

tooadd społecznościowych IDPs tooyour aplikacji, Rozpocznij od następujących hello szczegółowe instrukcje w tych artykułach. Dla każdego IDP ma toosupport, należy tooregister aplikacji w tym systemie i Uzyskaj identyfikator klienta.

* [Konfigurowanie usługi Facebook jako dostawca tożsamości](active-directory-b2c-setup-fb-app.md)
* [Konfigurowanie usługi Google jako dostawca tożsamości](active-directory-b2c-setup-goog-app.md)
* [Konfigurowanie usługi Amazon jako dostawca tożsamości](active-directory-b2c-setup-amzn-app.md)
* [Konfigurowanie LinkedIn jako dostawca tożsamości](active-directory-b2c-setup-li-app.md)

Po dodaniu katalog tooyour B2C dostawców tożsamości hello należy tooedit każdego z trzech zbiorów zasad tooinclude hello IDPs nowe, jak opisano w hello [artykule o zasadach](active-directory-b2c-reference-policies.md). Po zapisaniu zasad, należy ponownie uruchomić aplikacji hello. Powinny pojawić się hello IDPs nowe dodane jako opcje logowania i rejestracji w każdym doświadczeniami tożsamości.

Możesz eksperymentować z zasadami i obserwować hello efekty w aplikacji przykładowej. Dodaj lub usuń IDPs, manipulować oświadczenia aplikacji lub zmień atrybuty rejestracji. Eksperymentu, aż zostanie wyświetlony, jak zasady, żądania uwierzytelniania i MSAL powiązać razem.

Odwołania, hello ukończone próbki [jest dostępna jako plik .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip). Można ją także sklonować z serwisu GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
