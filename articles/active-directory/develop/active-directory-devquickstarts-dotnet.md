---
title: .NET aaaAzure AD wprowadzenie | Dokumentacja firmy Microsoft
description: "Jak toobuild aplikacji .NET pulpitu systemu Windows, która integruje się z usługą Azure AD w celu logowania się i wymaga usługi Azure AD chronione w trybie OAuth interfejsów API."
services: active-directory
documentationcenter: .net
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c09b358f24c7bfb371b34cf72ca48c0a45042f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a>Integrowanie usługi Azure AD w aplikacji WPF pulpitu systemu Windows
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Jeśli projektujesz klasycznej aplikacji usługi Azure AD umożliwia proste i bezpośrednie dla tooauthenticate można z użytkownikami przy użyciu ich kont usługi Active Directory.  Umożliwia również toosecurely Twojej aplikacji korzystać z dowolnej sieci web interfejsu API chronione przez usługę Azure AD, takich jak hello interfejsami API usługi Office 365 lub hello interfejsu API Azure.

W przypadku klientów platformy .NET native wymagające tooaccess chronionych zasobów usługi Azure AD zapewnia hello biblioteki uwierzytelniania usługi Active Directory lub biblioteki ADAL.  Jedynym celem ADAL jego życia jest toomake go łatwo tooget tokenów dostępu do aplikacji.  toodemonstrate Ci, jak łatwo jest, w tym miejscu będzie budujemy aplikacji listy zadań do wykonania WPF .NET który:

* Pobiera dostępu tokeny na potrzeby wywoływania hello Azure AD Graph API przy użyciu hello [protokół uwierzytelniania OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Przeszukuje katalog dla użytkowników z podanego aliasu.
* Znaki użytkowników.

toobuild hello pełną działającą aplikację, musisz:

1. Zarejestrować aplikację w usłudze Azure AD.
2. Instalowanie i konfigurowanie biblioteki ADAL.
3. Używaj tokenów ADAL tooget z usługi Azure AD.

Rozpoczęto, tooget [pobrać szkielet aplikacji hello](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) lub [pobieranie próbki ukończyć powitalnych](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).  Należy również dzierżawa usługi Azure AD można tworzyć użytkowników i zarejestrowanie aplikacji.  Jeśli nie masz już dzierżawę, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).

## <a name="1-register-hello-directorysearcher-application"></a>1. Zarejestruj hello DirectorySearcher aplikacji
tooenable tokenów tooget aplikacji, musisz najpierw tooregister dzierżawy w usługi Azure AD i udzielić jej uprawnienia tooaccess hello Azure AD Graph API:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Na górnym pasku hello, kliknij na Twoim koncie, a w obszarze hello **katalogu** wybierz hello dzierżawy usługi Active Directory, którym chcesz tooregister aplikacji.
3. Polecenie **więcej usług** w hello nawigacji po lewej stronie i wybierz polecenie **usługi Azure Active Directory**.
4. Polecenie **rejestracji aplikacji** i wybierz polecenie **Dodaj**.
5. Postępuj zgodnie z monitami hello i utworzyć nową **natywną aplikację kliencką**.
  * Witaj **nazwa** z hello aplikacji opisano użytkownikom tooend aplikacji
  * Witaj **identyfikator Uri przekierowania** jest kombinacją schemat i ciąg, które będą używane przez usługi Azure AD tooreturn odpowiedzi tokenu.  Wprowadź wartość tooyour określonych aplikacji, np. `http://DirectorySearcher`.
6. Po zakończeniu rejestracji usługi AAD przypisze aplikacji Unikatowy identyfikator aplikacji.  Ta wartość jest potrzebny w kolejnych sekcjach hello, dlatego skopiuj go ze strony aplikacji hello.
7. Z hello **ustawienia** wybierz pozycję **wymagane uprawnienia** i wybierz polecenie **Dodaj**. Wybierz hello **Microsoft Graph** jako hello interfejsu API i Dodaj hello **Czytaj dane katalogu** uprawnienie w obszarze **delegowane uprawnienia**.  Spowoduje to włączenie użytkownika hello tooquery aplikacji interfejsu API programu Graph dla użytkowników.

## <a name="2-install--configure-adal"></a>2. Instalowanie i konfigurowanie biblioteki ADAL
Teraz, gdy masz aplikacji w usłudze Azure AD, można zainstalować biblioteki ADAL i wpisz swój kod dotyczące tożsamości.  Aby mogli toocommunicate ADAL toobe z usługą Azure AD, należy tooprovide go niektóre informacje o rejestracji aplikacji.

* Rozpocznij, dodając ADAL toohello DirectorySearcher projektu przy użyciu konsoli Menedżera pakietów hello.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* W projekcie DirectorySearcher hello Otwórz `app.config`.  Zastąp wartości hello elementów hello na powitania `<appSettings>` hello tooreflect sekcji wartości danych wejściowych do hello portalu Azure.  Kod będzie odwoływać tych wartości, przy każdym użyciu biblioteki ADAL.
  * Witaj `ida:Tenant` jest hello domeny dzierżawy usługi Azure AD, np. contoso.onmicrosoft.com
  * Witaj `ida:ClientId` jest clientId hello skopiowany z portalu hello aplikacji.
  * Witaj `ida:RedirectUri` hello jest zarejestrowany w portalu hello adres url przekierowania.

## <a name="3----use-adal-tooget-tokens-from-aad"></a>3.    Używaj tokenów ADAL tooGet z usługi AAD
Witaj podstawową zasadą za ADAL jest czy zawsze, gdy Twoja aplikacja powinna tokenu dostępu, po prostu wywołuje `authContext.AcquireTokenAsync(...)`, i ADAL hello rest.  

* W hello `DirectorySearcher` otwarciu projektu `MainWindow.xaml.cs` i Znajdź hello `MainWindow()` metody.  pierwszym krokiem Hello jest tooinitialize aplikacji `AuthenticationContext` -ADAL obiektu klasy podstawowej.  Jest to, gdy przekazujesz ADAL hello współrzędne musi toocommunicate z usługą Azure AD i poinformuj go jak toocache tokenów.

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* Znajdź teraz hello `Search(...)` metodę, która będzie wywoływana, gdy przycisk "Wyszukiwanie" w Interfejsie użytkownika aplikacji hello hello hello cliks użytkownika.  Ta metoda ułatwia tworzenie tooquery toohello interfejsu API usługi Azure AD Graph żądania GET do użytkowników, których nazwy UPN zaczyna się hello danego wyszukiwanego terminu.  Jednak w kolejności tooquery hello interfejsu API programu Graph, tooinclude ' access_token ' w hello `Authorization` żądania nagłówek hello — jest to, gdzie ADAL jest dostarczany.

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate hello Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for hello tooDo item name");
        return;
    }

    // Get an Access Token for hello Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled hello sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* Gdy aplikacja żąda token przez wywołanie metody `AcquireTokenAsync(...)`, ADAL podejmie tooreturn token bez monitowania użytkownika hello o poświadczenia.  Jeśli ADAL ustali, że ten użytkownik hello musi toosign w tooget token, zostanie wyświetlane okno dialogowe logowania, zbieranie poświadczeń użytkownika hello i zwracają token, po pomyślnym uwierzytelnieniu.  Jeśli ADAL zostanie tooreturn tokenu z jakiegokolwiek powodu, zgłosi `AdalException`.
* Zwróć uwagę, że hello `AuthenticationResult` zawiera obiekt `UserInfo` obiektów, które mogą być używane toocollect informacji o aplikacji może być konieczne.  W hello DirectorySearcher `UserInfo` interfejsu użytkownika aplikacji hello toocustomize używanych z identyfikatorem użytkownika hello jest.
* Gdy hello użytkownik kliknie przycisk "Wyloguj" hello, chcemy tooensure, który hello następne wywołanie za`AcquireTokenAsync(...)` poprosi hello toosign użytkownika w.  Przy użyciu biblioteki ADAL jest tak proste, jak czyszczenie pamięci podręcznej tokenu hello:

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* Jednak jeśli użytkownik hello nie klikać przycisku "Wyloguj" hello, można toomaintain hello sesji użytkownika dla hello następnym uruchomieniu hello DirectorySearcher.  Po uruchomieniu aplikacji hello należy sprawdzić ADAL w pamięci podręcznej tokenu dla istniejącego tokenu, a następnie odpowiednio zaktualizować hello interfejsu użytkownika.  W hello `CheckForCachedToken()` metody wywoływania innego zbyt`AcquireTokenAsync(...)`, przekazując hello teraz `PromptBehavior.Never` parametru.  `PromptBehavior.Never`powiadomi ADAL, że użytkownik hello nie powinien być monitowany w celu logowania się i ADAL należy zamiast tego zgłoszenia wyjątku, jeśli jest tooreturn tokenu.

```C#
public async void CheckForCachedToken() 
{
    // As hello application starts, try tooget an access token without prompting hello user.  If one exists, show hello user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed toomain page without singing hello user in.
        return;
    }

    // A valid token is in hello cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

Gratulacje! Możesz teraz działa aplikacja .NET WPF, która ma hello możliwości tooauthenticate użytkowników, bezpiecznie wywoływania interfejsów API sieci Web przy użyciu protokołu OAuth 2.0 i uzyskać podstawowe informacje o użytkowniku hello.  Jeśli nie jest jeszcze teraz jest hello toopopulate czas dzierżawy z niektórych użytkowników.  Uruchom aplikację DirectorySearcher i zaloguj się przy użyciu jednej z tych użytkowników.  Wyszukiwać innych użytkowników, w oparciu o ich nazwy UPN.  Aplikacja hello Zamknij i uruchom je ponownie.  Zwróć uwagę, jak hello sesja pozostanie niezmieniona.  Wyloguj się i zaloguj się ponownie jako inny użytkownik.

Biblioteka ADAL umożliwia łatwe tooincorporate wszystkie te typowe funkcje tożsamości w aplikacji.  Zapewnia obsługę wszystkich hello dirty pracy dla Ciebie — Zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający hello użytkownika za pomocą interfejsu użytkownika, odświeżanie wygaśnięcia tokenów i inne nazwy logowania.  Naprawdę tooknow wystarczy jednego wywołania interfejsu API, `authContext.AcquireTokenAsync(...)`.

Odwołania, przykładowy ukończyć powitalnych (bez wartości konfiguracji) jest dostarczany [tutaj](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).  Możesz teraz przejść na tooadditional scenariuszy.  Można tootry:

[Zabezpieczanie interfejsu API za pomocą usługi Azure AD sieci Web .NET >>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

