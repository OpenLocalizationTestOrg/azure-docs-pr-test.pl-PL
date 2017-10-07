---
title: aaaAzure AD Xamarin wprowadzenie | Dokumentacja firmy Microsoft
description: "Tworzenie aplikacji platformy Xamarin integracji z usługą Azure AD, logowania i wywoływanie Azure API chronione przez usługi AD w trybie OAuth."
services: active-directory
documentationcenter: xamarin
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a>Integrowanie usługi Azure AD przy użyciu aplikacji Xamarin
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Za pomocą platformy Xamarin można napisać aplikacji mobilnych w języku C#, który można uruchomić w systemach iOS, Android i Windows (urządzeń przenośnych i komputerów). Jeśli tworzysz aplikację za pomocą platformy Xamarin usługi Azure Active Directory (Azure AD) umożliwia proste tooauthenticate użytkownikom ich kont usługi Azure AD. Aplikacja Hello także bezpiecznie może używać dowolnego interfejsu API sieci web chronionej przez usługę Azure AD, takie jak hello interfejsami API usługi Office 365 lub hello interfejsu API usługi Azure.

W przypadku aplikacji platformy Xamarin wymagające tooaccess chronionych zasobów usługi Azure AD zapewnia hello Active Directory Authentication Library (ADAL). jedynym celem ADAL Hello jest toomake go łatwo tokenów dostępu tooget aplikacji. toodemonstrate, jak łatwo jest, w tym artykule przedstawiono sposób aplikacji DirectorySearcher toobuild który:

* Uruchom na systemu iOS, Android, Windows Desktop, Windows Phone i Sklep Windows.
* Użyj jednej klasy przenośnej biblioteki (PCL) tooauthenticate użytkowników i uzyskać tokenów dla hello Azure AD Graph API.
* Wyszukaj katalog dla użytkowników z danym głównej nazwy użytkownika.

## <a name="before-you-get-started"></a>Przed rozpoczęciem
* Pobierz hello [szkielet projektu](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), lub pobrać hello [ukończone próbki](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip). Każdego pobrania to rozwiązanie Visual Studio 2013.
* Należy również dzierżawa usługi Azure AD, w których użytkownicy toocreate i aplikacji hello rejestru. Jeśli nie masz już dzierżawę, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).

Gdy wszystko będzie gotowe, wykonaj procedury hello hello obok cztery sekcje.

## <a name="step-1-set-up-your-xamarin-development-environment"></a>Krok 1: Konfigurowanie środowiska deweloperskiego Xamarin
Ten samouczek zawiera projektów dla systemu iOS, Android i Windows, należy Xamarin i Visual Studio. toocreate hello wymagane środowisko, hello ukończenia procesu w [ustawić Konfigurowanie i instalowanie programu Visual Studio i Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) w witrynie MSDN. instrukcje Hello obejmować materiału, który można przejrzeć toolearn więcej informacji na temat platformy Xamarin w trakcie oczekiwania dla toobe instalacje hello ukończone.

Po zakończeniu instalacji hello Otwórz rozwiązanie hello w programie Visual Studio. Istnieje, można znaleźć projektów sześciu: pięć projektów specyficzne dla platformy i jeden PCL, DirectorySearcher.cs, które będą udostępniane na wszystkich platformach.

## <a name="step-2-register-hello-directorysearcher-app"></a>Krok 2: Rejestrowanie aplikacji DirectorySearcher hello
tooenable tokenów tooget aplikacji hello, musisz najpierw tooregister w usługi Azure AD dzierżawy i udzielić jej uprawnienia tooaccess hello Azure AD Graph API. Oto kroki tej procedury:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Na górnym pasku powitania kliknij swoje konto. Następnie w obszarze hello **katalogu** listy, wybierz hello dzierżawy usługi Active Directory, w którym ma tooregister aplikacji hello.
3. Kliknij przycisk **więcej usług** w lewym okienku hello, a następnie wybierz **usługi Azure Active Directory**.
4. Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.
5. toocreate nowy **natywną aplikację kliencką**, postępuj zgodnie z monitami hello.
  * **Nazwa** opisuje toousers aplikacji hello.
  * **Identyfikator URI przekierowania** to kombinacja schemat i ciąg używany tooreturn odpowiedzi tokenu w usłudze Azure AD. Wprowadź wartość (na przykład http://DirectorySearcher).
6. Po zakończeniu rejestracji usługi Azure AD przypisuje aplikacji hello identyfikatora aplikacji Skopiuj wartość hello z hello **aplikacji** karcie, ponieważ będzie on potrzebny później.
7. Na powitania **ustawienia** wybierz pozycję **wymagane uprawnienia**, a następnie wybierz **Dodaj**.
8. Wybierz **Microsoft Graph** jako hello interfejsu API. W obszarze **delegowane uprawnienia**, Dodaj hello **Czytaj dane katalogu** uprawnienia.  
Ta akcja umożliwia aplikacji hello tooquery hello interfejsu API programu Graph dla użytkowników.

## <a name="step-3-install-and-configure-adal"></a>Krok 3: Instalowanie i konfigurowanie biblioteki ADAL
Teraz, gdy masz aplikację w usłudze Azure AD, można zainstalować biblioteki ADAL i wpisz swój kod dotyczące tożsamości. tooenable toocommunicate ADAL w usłudze Azure AD, nadaj pewne informacje o rejestracji aplikacji hello.

1. Dodaj projekt DirectorySearcher ADAL toohello przy użyciu konsoli Menedżera pakietów hello.

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    Należy pamiętać, że dwa odwołania biblioteki są dodawane tooeach projektu: hello PCL część ADAL i części specyficzne dla platformy.
2. W projekcie DirectorySearcherLib hello Otwórz DirectorySearcher.cs.
3. Zastąp wartości elementu członkowskiego klasy hello hello wartości, które wprowadzono w hello portalu Azure. Kod odnosi się wartości toothese zawsze, gdy używa biblioteki ADAL.

  * Witaj *dzierżawy* jest hello domeny dzierżawy usługi Azure AD (np. contoso.onmicrosoft.com).
  * Witaj *clientId* jest hello identyfikator klienta aplikacji hello, który został skopiowany z portalu hello.
  * Witaj *returnUri* jest hello przekierowania URI, który został wprowadzony w portalu hello (na przykład http://DirectorySearcher).

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a>Krok 4: Użyj ADAL tooget tokenów z usługi Azure AD
Prawie wszystkie logika uwierzytelniania aplikacji hello znajduje się `DirectorySearcher.SearchByAlias(...)`. Wszystko, co jest niezbędne w projektach specyficzne dla platformy hello jest toopass toohello parametru kontekstowego `DirectorySearcher` PCL.

1. Otwórz DirectorySearcher.cs, a następnie dodaj nowe toohello parametr `SearchByAlias(...)` metody. `IPlatformParameters`jest uwierzytelniania ADAL potrzeb tooperform hello obiekty hello kontekstowe parametr, który hermetyzuje hello specyficzne dla platformy.

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. Inicjowanie `AuthenticationContext`, która jest hello klasy podstawowej biblioteki adal.  
Witaj ADAL przekazuje akcji koordynuje toocommunicate potrzeb z usługą Azure AD.
3. Wywołanie `AcquireTokenAsync(...)`, który akceptuje hello `IPlatformParameters` obiektu i wywołuje hello przepływ uwierzytelniania, który jest konieczne tooreturn aplikacji toohello tokenu.

    ```C#
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    `AcquireTokenAsync(...)`pierwszy tooreturn prób token dla hello żądanego zasobu (hello interfejsu API programu Graph w tym przypadku) bez monitowania użytkowników tooenter poświadczeń (za pośrednictwem buforowanie lub odświeżanie starego tokeny). W razie potrzeby przedstawia on użytkowników strony logowania dla usługi Azure AD hello przed uzyskiwanie hello żądanego tokenu.
4. Dołącz hello żądanie interfejsu API programu Graph token toohello dostępu w hello **autoryzacji** nagłówka:

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

To wszystko dla hello `DirectorySearcher` kodu dotyczące tożsamości PCL i hello aplikacji. Liście nie zostanie toocall hello `SearchByAlias(...)` metody w widokach każdej platformy i, w miarę potrzeby kodu tooadd poprawnie obsługi hello cykl życia interfejsu użytkownika.

### <a name="android"></a>Android
1. W MainActivity.cs, dodaj wywołanie za`SearchByAlias(...)` przycisku powitania kliknij program obsługi:

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. Zastąpienie hello `OnActivityResult` tooforward metody cykl życia uwierzytelniania przekierowuje wstecz toohello odpowiedniej metody. Biblioteka ADAL udostępnia metodę pomocnika dla tego w systemie Android:

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a>System Windows Desktop
W MainWindow.xaml.cs, nawiązywanie połączeń za`SearchByAlias(...)` przez przekazanie `WindowInteropHelper` na pulpicie hello `PlatformParameters` obiektu:

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a>iOS
W DirSearchClient_iOSViewController.cs, hello iOS `PlatformParameters` obiektu przyjmuje odwołanie toohello kontrolera widoku:

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a>Aplikacje uniwersalne systemu Windows
W uniwersalnych systemu Windows otwórz MainPage.xaml.cs, a następnie wdrożyć hello `Search` metody. Ta metoda używa metody pomocnika w projekcie udostępnionym tooupdate interfejsu użytkownika w razie potrzeby.

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a>Co dalej
Masz teraz pracy aplikacji platformy Xamarin, który może uwierzytelniać użytkowników i bezpiecznie wywoływać interfejsy API sieci web przy użyciu protokołu OAuth 2.0 na pięciu różnych platformach.

Jeśli nie zostało już wypełnione dzierżawy z użytkownikami, teraz jest toodo czas hello tak.

1. Uruchom aplikację DirectorySearcher, a następnie zaloguj się przy użyciu jednego z hello użytkowników.
2. Wyszukiwać innych użytkowników, w oparciu o ich nazwy UPN.

ADAL umożliwia łatwe tooincorporate wspólne funkcje tożsamości w aplikacji hello. Go zajmuje się wszystkie hello dirty pracy, takich jak zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający hello użytkownika za pomocą interfejsu użytkownika, nazwy logowania i odświeżanie wygasła tokenów. Należy wywołania tooknow tylko jednego interfejsu API `authContext.AcquireToken*(…)`.

Odwołania, Pobierz hello [ukończone próbki](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (bez wartości konfiguracji).

Możesz teraz przejść na tooadditional tożsamości scenariuszy. Na przykład, spróbuj [zabezpieczyć interfejs API sieci Web .NET z usługą Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
