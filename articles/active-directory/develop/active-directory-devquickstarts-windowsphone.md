---
title: aaaAzure Windows Phone AD wprowadzenie | Dokumentacja firmy Microsoft
description: "Jak toobuild aplikacji Windows Phone, która integruje się z usługą Azure AD w celu logowania się i wymaga usługi Azure AD chronione w trybie OAuth interfejsów API."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a>Integrowanie usługi Azure AD w aplikacji Windows Phone
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Projekty systemu Windows Phone 8.1 i wcześniejszych nie są obsługiwane w programie Visual Studio 2017 r.  Aby uzyskać więcej informacji, zobacz [Obsługiwane platformy i zgodność programu Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

Jeśli projektujesz aplikacji Windows Phone 8.1, usługi Azure AD umożliwia proste i bezpośrednie dla tooauthenticate możesz z użytkownikami przy użyciu ich kont usługi Active Directory.  Umożliwia również toosecurely Twojej aplikacji korzystać z dowolnej sieci web interfejsu API chronione przez usługę Azure AD, takich jak hello interfejsami API usługi Office 365 lub hello interfejsu API Azure.

> [!NOTE]
> Ten przykładowy kod używa biblioteki ADAL w wersji 2.0.  Hello najnowszych technologii, można spróbować tooinstead naszych [samouczek aplikacji uniwersalnych systemu Windows przy użyciu biblioteki ADAL w wersji 3.0](active-directory-devquickstarts-windowsstore.md).  Jeśli tworzysz rzeczywiście aplikacji dla systemu Windows Phone 8.1, to hello w odpowiednim miejscu.  ADAL w wersji 2.0 jest nadal w pełni obsługiwane, a jest hello zalecany sposób tworzenie agianst aplikacji Windows Phone 8.1 przy użyciu usługi Azure AD.
> 
> 

W przypadku klientów platformy .NET native wymagające tooaccess chronionych zasobów usługi Azure AD zapewnia hello biblioteki uwierzytelniania usługi Active Directory lub biblioteki ADAL.  Jedynym celem ADAL jego życia jest toomake go łatwo tooget tokenów dostępu do aplikacji.  toodemonstrate Ci, jak łatwo jest, w tym miejscu będzie budujemy "katalog modułu wyszukującego" aplikacji systemu Windows Phone 8.1 który:

* Pobiera dostępu tokeny na potrzeby wywoływania hello Azure AD Graph API przy użyciu hello [protokół uwierzytelniania OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Przeszukuje katalog dla użytkowników z danym głównej nazwy użytkownika.
* Znaki użytkowników.

toobuild hello pełną działającą aplikację, musisz:

1. Zarejestrować aplikację w usłudze Azure AD.
2. Instalowanie i konfigurowanie biblioteki ADAL.
3. Używaj tokenów ADAL tooget z usługi Azure AD.

Rozpoczęto, tooget [pobrać szkielet projektu](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) lub [pobieranie próbki ukończyć powitalnych](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  Każdy jest rozwiązanie Visual Studio 2013.  Należy również dzierżawa usługi Azure AD można tworzyć użytkowników i zarejestrowanie aplikacji.  Jeśli nie masz już dzierżawę, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).

## <a name="1-register-hello-directory-searcher-application"></a>1. Zarejestruj hello aplikacji poszukującego katalogu
tooenable tokenów tooget aplikacji, musisz najpierw tooregister dzierżawy w usługi Azure AD i udzielić jej uprawnienia tooaccess hello Azure AD Graph API:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Na górnym pasku hello, kliknij na Twoim koncie, a w obszarze hello **katalogu** wybierz hello dzierżawy usługi Active Directory, którym chcesz tooregister aplikacji.
3. Polecenie **więcej usług** w hello nawigacji po lewej stronie i wybierz polecenie **usługi Azure Active Directory**.
4. Polecenie **rejestracji aplikacji** i wybierz polecenie **Dodaj**.
5. Postępuj zgodnie z monitami hello i utworzyć nową **natywną aplikację kliencką**.
  * Witaj **nazwa** z hello aplikacji opisano użytkownikom tooend aplikacji
  * Witaj **identyfikator Uri przekierowania** jest kombinacją schemat i ciąg, które będą używane przez usługi Azure AD tooreturn odpowiedzi tokenu.  Wprowadź wartość symbolu zastępczego teraz, np. `http://DirectorySearcher`.  Firma Microsoft będzie później Zastąp tę wartość.
6. Po zakończeniu rejestracji usługi AAD przypisze aplikacji Unikatowy identyfikator aplikacji.  Ta wartość jest potrzebny w kolejnych sekcjach hello, dlatego skopiuj go na karcie aplikacji hello.
7. Z hello **ustawienia** wybierz pozycję **wymagane uprawnienia** i wybierz polecenie **Dodaj**. Wybierz hello **Microsoft Graph** jako hello interfejsu API i Dodaj hello **Czytaj dane katalogu** uprawnienie w obszarze **delegowane uprawnienia**.  Spowoduje to włączenie użytkownika hello tooquery aplikacji interfejsu API programu Graph dla użytkowników.

## <a name="2-install--configure-adal"></a>2. Instalowanie i konfigurowanie biblioteki ADAL
Teraz, gdy masz aplikacji w usłudze Azure AD, można zainstalować biblioteki ADAL i wpisz swój kod dotyczące tożsamości.  Aby mogli toocommunicate ADAL toobe z usługą Azure AD, należy tooprovide go niektóre informacje o rejestracji aplikacji.

* Rozpocznij, dodając ADAL toohello DirectorySearcher projektu przy użyciu konsoli Menedżera pakietów hello.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* W projekcie DirectorySearcher hello Otwórz `MainPage.xaml.cs`.  Zastąp wartości hello hello `Config Values` region tooreflect hello wartości danych wejściowych do hello portalu Azure.  Kod będzie odwoływać tych wartości, przy każdym użyciu biblioteki ADAL.
  * Witaj `tenant` jest hello domeny dzierżawy usługi Azure AD, np. contoso.onmicrosoft.com
  * Witaj `clientId` jest clientId hello skopiowany z portalu hello aplikacji.
* Teraz należy toodiscover hello wywołania zwrotnego uri dla aplikacji Windows Phone.  Ustaw punkt przerwania w tym wierszu hello `MainPage` metody:

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* Uruchamianie aplikacji hello i skopiuj Odłóż wartość hello `redirectUri` po hello przerwania zostaje trafiony.  Powinien on wyglądać podobnie jak

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* Wróć na powitania **Konfiguruj** kartę aplikacji hello portalu zarządzania Azure, zastąp wartość hello hello **RedirectUri** o tej wartości.  

## <a name="3-use-adal-tooget-tokens-from-aad"></a>3. Używaj tokenów ADAL tooGet z usługi AAD
Witaj podstawową zasadą za ADAL jest czy zawsze, gdy Twoja aplikacja powinna tokenu dostępu, po prostu wywołuje `authContext.AcquireToken(…)`, i ADAL hello rest.  

* pierwszym krokiem Hello jest tooinitialize aplikacji `AuthenticationContext` -ADAL obiektu klasy podstawowej.  Jest to, gdy przekazujesz ADAL hello współrzędne musi toocommunicate z usługą Azure AD i poinformuj go jak toocache tokenów.

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* Znajdź teraz hello `Search(...)` metodę, która będzie wywoływana, gdy przycisk "Wyszukiwanie" w Interfejsie użytkownika aplikacji hello hello hello cliks użytkownika.  Ta metoda ułatwia tworzenie tooquery toohello interfejsu API usługi Azure AD Graph żądania GET do użytkowników, których nazwy UPN zaczyna się hello danego wyszukiwanego terminu.  Jednak w kolejności tooquery hello interfejsu API programu Graph, tooinclude ' access_token ' w hello `Authorization` żądania nagłówek hello — jest to, gdzie ADAL jest dostarczany.

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* Jeśli konieczne jest uwierzytelnianie interakcyjne, ADAL użyje Książka adresowa systemu (Windows, Windows Phone w sieci Web uwierzytelniania Broker) i [modelu kontynuacji](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD, zaloguj się na stronie.  Po zalogowaniu użytkownika hello Twoja aplikacja powinna toopass ADAL hello wyniki interakcji Książka adresowa systemu Windows hello.  Jest tak proste, jak implementacja hello `ContinueWebAuthentication` interfejsu:

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* Teraz nadszedł czas toouse hello `AuthenticationResult` tego ADAL zwrócił tooyour aplikacji.  W hello `QueryGraph(...)` wywołania zwrotnego, Dołącz ' access_token ' hello nabył toohello żądanie GET w nagłówku autoryzacji hello:

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* Można również użyć hello `AuthenticationResult` obiekt toodisplay informacji na temat hello użytkownika w aplikacji. W hello `QueryGraph(...)` metoda, użyj hello wynik tooshow hello identyfikatora użytkownika na stronie powitania:

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* Ponadto można użyć użytkownika hello ADAL toosign z aplikacji, a także.  Gdy hello użytkownik kliknie przycisk "Wyloguj" hello, chcemy tooensure, który hello następne wywołanie za`AcquireTokenSilentAsync(...)` zakończy się niepowodzeniem.  Przy użyciu biblioteki ADAL jest tak proste, jak czyszczenie pamięci podręcznej tokenu hello:

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

Gratulacje! Teraz masz pracy aplikacji Windows Phone, który ma hello możliwości tooauthenticate użytkowników, bezpiecznie wywoływać interfejsy API sieci Web przy użyciu protokołu OAuth 2.0, a uzyskać podstawowe informacje o użytkowniku hello.  Jeśli nie jest jeszcze teraz jest hello toopopulate czas dzierżawy z niektórych użytkowników.  Uruchom aplikację DirectorySearcher i zaloguj się przy użyciu jednej z tych użytkowników.  Wyszukiwać innych użytkowników, w oparciu o ich nazwy UPN.  Aplikacja hello Zamknij i uruchom je ponownie.  Zwróć uwagę, jak hello sesja pozostanie niezmieniona.  Wyloguj się i zaloguj się ponownie jako inny użytkownik.

Biblioteka ADAL umożliwia łatwe tooincorporate wszystkie te typowe funkcje tożsamości w aplikacji.  Zapewnia obsługę wszystkich hello dirty pracy dla Ciebie — Zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający hello użytkownika za pomocą interfejsu użytkownika, odświeżanie wygaśnięcia tokenów i inne nazwy logowania.  Naprawdę tooknow wystarczy jednego wywołania interfejsu API, `authContext.AcquireToken*(…)`.

Odwołania, przykładowy ukończyć powitalnych (bez wartości konfiguracji) jest dostarczany [tutaj](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  Możesz teraz przejść na tooadditional tożsamości scenariuszy.  Można tootry:

[Zabezpieczanie interfejsu API za pomocą usługi Azure AD sieci Web .NET >>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

