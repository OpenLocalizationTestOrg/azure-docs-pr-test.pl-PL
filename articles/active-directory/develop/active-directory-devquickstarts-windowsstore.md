---
title: aaaAzure sklepu AD Windows wprowadzenie | Dokumentacja firmy Microsoft
description: "Aplikacje ze Sklepu Windows kompilacji integracji z usługą Azure AD, logowania, które wywołanie usługi Azure AD chronione interfejsów API w trybie OAuth."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a>Integrowanie usługi Azure AD z aplikacji ze Sklepu Windows
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Wcześniejsze niż wersja projektów i Sklepu Windows 8.1 nie są obsługiwane w programie Visual Studio 2017 r.  Aby uzyskać więcej informacji, zobacz [Obsługiwane platformy i zgodność programu Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

Jeśli projektujesz aplikacji dla Sklepu Windows hello Azure Active Directory (Azure AD) umożliwia proste i bezpośrednie tooauthenticate z użytkownikami przy użyciu ich kont usługi Active Directory. Dzięki integracji z usługą Azure AD, aplikacji można bezpiecznie korzystać z dowolnej sieci web interfejsu API, która jest chroniona przez usługę Azure AD, takie jak hello interfejsami API usługi Office 365 lub hello interfejsu API usługi Azure.

Dla Sklepu Windows aplikacji klasycznych wymagające tooaccess chronionych zasobów Usługa Azure AD zapewnia hello Active Directory Authentication Library (ADAL). jedynym celem ADAL Hello jest toomake go łatwo tokenów dostępu tooget aplikacji hello. toodemonstrate, jak łatwo jest, w tym artykule opisano, jak toobuild DirectorySearcher ze Sklepu Windows aplikacji który:

* Pobiera dostępu tokenów do wywoływania interfejsu API Azure AD Graph hello przy użyciu hello [protokół uwierzytelniania OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Przeszukuje katalog dla użytkowników z główną nazwę użytkownika (UPN).
* Znaki użytkowników.

## <a name="before-you-get-started"></a>Przed rozpoczęciem
* Pobierz hello [szkielet projektu](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), lub pobrać hello [ukończone próbki](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip). Każdego pobrania to rozwiązanie Visual Studio 2015.
* Należy również dzierżawa usługi Azure AD, w których użytkownicy toocreate i aplikacji hello rejestru. Jeśli nie masz już dzierżawę, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).

Gdy wszystko będzie gotowe, wykonaj procedury hello hello trzech kolejnych sekcjach.

## <a name="step-1-register-hello-directorysearcher-app"></a>Krok 1: Rejestrowanie aplikacji DirectorySearcher hello
tooenable tokenów tooget aplikacji hello, musisz najpierw tooregister w usługi Azure AD dzierżawy i udzielić jej uprawnienia tooaccess hello Azure AD Graph API. Oto kroki tej procedury:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Na górnym pasku powitania kliknij swoje konto. Następnie w obszarze hello **katalogu** listy, wybierz hello dzierżawy usługi Active Directory, w którym ma tooregister aplikacji hello.
3. Kliknij przycisk **więcej usług** w lewym okienku hello, a następnie wybierz **usługi Azure Active Directory**.
4. Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.
5. Wykonaj hello monity toocreate **natywną aplikację kliencką**.
  * **Nazwa** opisuje toousers aplikacji hello.
  * **Identyfikator URI przekierowania** to kombinacja schemat i ciąg używany tooreturn odpowiedzi tokenu w usłudze Azure AD. Wprowadź wartość symbolu zastępczego teraz (na przykład **http://DirectorySearcher**). Będzie Zamień wartość hello później.
6. Po zakończeniu rejestracji hello Azure AD przypisuje aplikacji hello identyfikatora aplikacji Kopiuj wartość hello na powitania **aplikacji** karcie, ponieważ będzie on potrzebny później.
7. Na powitania **ustawienia** wybierz pozycję **wymagane uprawnienia**, a następnie wybierz **Dodaj**.
8. Dla hello **usługi Azure Active Directory** aplikacji, wybierz opcję **Microsoft Graph** jako hello interfejsu API.
9. W obszarze **delegowane uprawnienia**, Dodaj hello **dostępu do katalogu hello jako hello zalogowanego użytkownika** uprawnienia. Umożliwi to aplikacja hello tooquery hello interfejsu API programu Graph dla użytkowników.

## <a name="step-2-install-and-configure-adal"></a>Krok 2: Instalowanie i konfigurowanie biblioteki ADAL
Teraz, gdy masz aplikację w usłudze Azure AD, można zainstalować biblioteki ADAL i wpisz swój kod dotyczące tożsamości. tooenable toocommunicate ADAL w usłudze Azure AD, nadaj pewne informacje o rejestracji aplikacji hello.

1. Dodaj projekt DirectorySearcher ADAL toohello przy użyciu konsoli Menedżera pakietów hello.

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. W projekcie DirectorySearcher hello Otwórz MainPage.xaml.cs.
3. Zastąp wartości hello hello **wartości konfiguracji** region hello wartości, które wprowadzono w hello portalu Azure. Kod odnosi się wartości toothese zawsze, gdy używa biblioteki ADAL.
  * Witaj *dzierżawy* jest hello domeny dzierżawy usługi Azure AD (np. contoso.onmicrosoft.com).
  * Witaj *clientId* jest hello identyfikator klienta aplikacji hello, który został skopiowany z portalu hello.
4. Teraz należy toodiscover identyfikator URI wywołania zwrotnego powitania dla aplikacji ze Sklepu Windows. Ustaw punkt przerwania w tym wierszu hello `MainPage` metody:
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. Utworzenie rozwiązania hello, upewniając się, że wszystkie odwołania do pakietu zostaną przywrócone. Jeśli brakuje żadnych pakietów, otwórz hello Menedżera pakietów NuGet, a następnie przywrócić je.
6. Uruchamianie aplikacji hello i skopiuj wartość hello `redirectUri` po hello przerwania zostaje trafiony. wartość Hello powinien wyglądać jak poniżej hello:

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. Wróć na powitania **ustawienia** kartę aplikacji hello w hello portalu Azure, Dodaj **RedirectUri** z hello poprzedzających wartość.  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a>Krok 3: Użyj ADAL tooget tokenów z usługi Azure AD
Witaj podstawową zasadą za ADAL jest czy zawsze, gdy aplikacja hello potrzebuje tokenu dostępu, po prostu wywołuje `authContext.AcquireToken(…)`, i ADAL hello rest.  

1. Inicjowanie aplikacji hello `AuthenticationContext`, która jest hello klasy podstawowej biblioteki adal. Ta akcja przekazuje współrzędne ADAL hello wymaga toocommunicate z usługą Azure AD i poinformuj go jak toocache tokenów.

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. Zlokalizuj hello `Search(...)` metodę, która jest wywoływana, gdy użytkownik kliknie hello **wyszukiwania** przycisk w Interfejsie użytkownika aplikacji hello. Ta metoda ułatwia tworzenie tooquery toohello interfejsu API usługi Azure AD Graph żądania get do użytkowników, których nazwy UPN zaczyna się hello danego wyszukiwanego terminu. Witaj tooquery interfejsu API programu Graph, obejmują token dostępu w żądaniu hello **autoryzacji** nagłówka. Jest to, gdzie ADAL jest dostarczany.

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    Gdy aplikacja hello żąda token przez wywołanie metody `AcquireTokenAsync(...)`, ADAL prób tooreturn token bez monitowania użytkownika hello o poświadczenia. Jeśli ADAL ustali, że ten użytkownik hello musi toosign w tooget token, wyświetla okno dialogowe logowania, służy do zbierania poświadczeń użytkownika hello i zwraca token po pomyślnym uwierzytelnieniu. Jeśli ADAL zostanie tooreturn tokenu z jakiegokolwiek powodu, hello *AuthenticationResult* stanu błędu.
3. Teraz jest token dostępu hello toouse czasu, uzyskanych. Również w hello `Search(...)` metody, Dołącz hello toohello token interfejsu API programu Graph pobrać żądania w hello **autoryzacji** nagłówka:

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. Można użyć hello `AuthenticationResult` obiekt toodisplay informacji na temat hello użytkownika w aplikacji hello, takie jak nazwa użytkownika hello:

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. Umożliwia także użytkowników ADAL toosign z aplikacji hello. Po kliknięciu przez użytkownika hello hello **Wyloguj** przycisku, upewnij się, hello kolejnego połączenia z tym zbyt`AcquireTokenAsync(...)` przedstawia widok logowania. Przy użyciu biblioteki ADAL ta akcja jest tak proste, jak czyszczenie pamięci podręcznej tokenu hello:

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a>Co dalej
Masz teraz pracy aplikacji do Sklepu Windows, który może uwierzytelniać użytkowników, bezpiecznie wywołać przy użyciu protokołu OAuth 2.0 interfejsów API sieci web i uzyskać podstawowe informacje o użytkowniku hello.

Jeśli nie zostało już wypełnione dzierżawy z użytkownikami, teraz jest toodo czas hello tak.
1. Uruchom aplikację DirectorySearcher, a następnie zaloguj się przy użyciu jednego z hello użytkowników.
2. Wyszukiwać innych użytkowników, w oparciu o ich nazwy UPN.
3. Aplikacja hello Zamknij i ponownie ją uruchomić. Zwróć uwagę, jak hello sesja pozostanie niezmieniona.
4. Wyloguj się, klikając prawym przyciskiem myszy toodisplay hello dolnym pasku, a następnie zalogować się jako inny użytkownik.

Biblioteka ADAL umożliwia łatwe tooincorporate wszystkie te wspólne tożsamości funkcje do aplikacji hello. Go zajmuje się wszystkie hello dirty pracy, takich jak zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający hello użytkownika za pomocą interfejsu użytkownika, nazwy logowania i odświeżanie wygasła tokenów. Należy wywołania tooknow tylko jednego interfejsu API `authContext.AcquireToken*(…)`.

Odwołania, Pobierz hello [ukończone próbki](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (bez wartości konfiguracji).

Możesz teraz przejść na tooadditional tożsamości scenariuszy. Na przykład, spróbuj [zabezpieczyć interfejs API sieci Web .NET z usługą Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
