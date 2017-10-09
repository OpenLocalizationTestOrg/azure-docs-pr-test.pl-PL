---
title: "aaaAzure AD v2 Windows Desktop wprowadzenie - Użyj | Dokumentacja firmy Microsoft"
description: "Jak aplikacje .NET pulpitu systemu Windows (XAML) można wywołać interfejsu API, które wymagają tokenów dostępu przez punkt końcowy w wersji 2 usługi Azure Active Directory"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: bb258fe5f523ec727ca02716fd823d853d3349b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Użyj hello biblioteki uwierzytelniania firmy Microsoft (MSAL) tooget token dla hello interfejsu API programu Microsoft Graph

W tej sekcji przedstawiono, jak toouse MSAL tooget token hello interfejsu API programu Microsoft Graph.

1.  W `MainWindow.xaml.cs`, Dodaj odwołanie hello MSAL biblioteki toohello klasy:

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Zastąp <code>MainWindow</code> kod z klasy:
</li>
</ol>

```csharp
public partial class MainWindow : Window
{
    //Set hello API Endpoint tooGraph 'me' endpoint
    string _graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";

    //Set hello scope for API call toouser.read
    string[] _scopes = new string[] { "user.read" };


    public MainWindow()
    {
        InitializeComponent();
    }

    /// <summary>
    /// Call AcquireTokenAsync - tooacquire a token requiring user toosign-in
    /// </summary>
    private async void CallGraphButton_Click(object sender, RoutedEventArgs e)
    {
        AuthenticationResult authResult = null;

        try
        {
            authResult = await App.PublicClientApp.AcquireTokenSilentAsync(_scopes, App.PublicClientApp.Users.FirstOrDefault());
        }
        catch (MsalUiRequiredException ex)
        {
            // A MsalUiRequiredException happened on AcquireTokenSilentAsync. This indicates you need toocall AcquireTokenAsync tooacquire a token
            System.Diagnostics.Debug.WriteLine($"MsalUiRequiredException: {ex.Message}");

            try
            {
                authResult = await App.PublicClientApp.AcquireTokenAsync(_scopes);
            }
            catch (MsalException msalex)
            {
                ResultText.Text = $"Error Acquiring Token:{System.Environment.NewLine}{msalex}";
            }
        }
        catch (Exception ex)
        {
            ResultText.Text = $"Error Acquiring Token Silently:{System.Environment.NewLine}{ex}";
            return;
        }

        if (authResult != null)
        {
            ResultText.Text = await GetHttpContentWithToken(_graphAPIEndpoint, authResult.AccessToken);
            DisplayBasicTokenInfo(authResult);
            this.SignOutButton.Visibility = Visibility.Visible;
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>Więcej informacji
#### <a name="getting-a-user-token-interactive"></a>Pobieranie tokenu użytkownika interakcyjnego
Wywoływanie hello `AcquireTokenAsync` — metoda powoduje monitowanie okna hello toosign użytkownika w. Aplikacje zwykle wymagają toosign użytkownika, w interaktywnie hello muszą tooaccess po raz pierwszy chronionego zasobu lub tooacquire dyskretnej operacji tokenu nie powiedzie się, (np. hasło użytkownika hello ważność).

#### <a name="getting-a-user-token-silently"></a>Pobieranie tokenu użytkownika dyskretnej
`AcquireTokenSilentAsync`obsługuje przejęć tokenu i wznowienie bez interakcji użytkownika. Po `AcquireTokenAsync` jest wykonywana na powitania po raz pierwszy, `AcquireTokenSilentAsync` hello zwykle metodę tooobtain tokenów używanych tooaccess chronionych zasobów w kolejnych wywołaniach — jako toorequest wywołania lub odnowić tokeny są wprowadzane w trybie dyskretnym.
Po pewnym czasie `AcquireTokenSilentAsync` zakończy się niepowodzeniem — np. użytkownika hello zalogował lub została zmieniona hasła na innym urządzeniu. Gdy MSAL wykryje, że hello problem można rozwiązać, gdyż akcję interaktywne, jego generowane `MsalUiRequiredException`. Aplikacja może obsłużyć tego wyjątku na dwa sposoby:

1.  Nawiązywanie połączeń z `AcquireTokenAsync` natychmiast, która powoduje monitowanie użytkownika hello toosign w. Ten wzorzec jest zazwyczaj używany w aplikacji online w przypadku, gdy nie żadnej zawartości w trybie offline w aplikacji hello dostępnej dla użytkownika hello. Hello próbki wygenerowane za pomocą tego Instalatora z przewodnikiem używa tego wzorca: Zobacz go w akcji powitania po raz pierwszy wykonać próbki hello: ponieważ żaden użytkownik nigdy używana aplikacja hello `PublicClientApp.Users.FirstOrDefault()` będzie zawierać wartości null i `MsalUiRequiredException` zostanie wygenerowany wyjątek. Witaj kodu w przykładowym hello, a następnie uchwytów hello wyjątku przez wywołanie metody `AcquireTokenAsync` powodujące monitowania użytkownika hello toosign w.

2.  Aplikacje można również ustawić oznaczenia wizualne użytkownik toohello interakcyjne logowanie jest wymagany, dlatego hello użytkownik może wybrać toosign odpowiednich momentach hello w lub ponowić aplikacji hello `AcquireTokenSilentAsync` w późniejszym czasie. Służy to zwykle gdy hello użytkownik może użyć innych funkcji aplikacji hello bez są zakłócone — na przykład Brak dostępnej zawartości w trybie offline w aplikacji hello. W takim przypadku hello użytkownika można określić, gdy mają toosign w tooaccess hello chroniony zasób, lub toorefresh hello przestarzałe informacje lub aplikacji można określić tooretry `AcquireTokenSilentAsync` przywrócenie sieci po są tymczasowo niedostępne.
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Wywołanie interfejsu API programu Microsoft Graph hello przy użyciu tokenu hello, który został uzyskany

1. Dodaj nową metodę hello poniżej tooyour `MainWindow.xaml.cs`. Witaj metoda jest używana toomake `GET` żądania interfejsu API programu Graph przy użyciu nagłówka autoryzacji:

```csharp
/// <summary>
/// Perform an HTTP GET request tooa URL using an HTTP Authorization header
/// </summary>
/// <param name="url">hello URL</param>
/// <param name="token">hello token</param>
/// <returns>String containing hello results of hello GET operation</returns>
public async Task<string> GetHttpContentWithToken(string url, string token)
{
    var httpClient = new System.Net.Http.HttpClient();
    System.Net.Http.HttpResponseMessage response;
    try
    {
        var request = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, url);
        //Add hello token in Authorization header
        request.Headers.Authorization = new System.Net.Http.Headers.AuthenticationHeaderValue("Bearer", token);
        response = await httpClient.SendAsync(request);
        var content = await response.Content.ReadAsStringAsync();
        return content;
    }
    catch (Exception ex)
    {
        return ex.ToString();
    }
}
```
<!--start-collapse-->
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Więcej informacji na temat nawiązywania połączenia przed chronionego interfejsu API REST

W tej przykładowej aplikacji hello `GetHttpContentWithToken` metoda jest używana toomake HTTP `GET` żądania dotyczącego zasobu chronionego wymagającego wywołującego zawartości toohello token, a następnie wróć hello. Ta metoda dodaje token hello nabyte w hello *nagłówek autoryzacji HTTP*. Dla tego przykładu zasób hello jest hello interfejsu API programu Microsoft Graph *mnie* punktu końcowego — Wyświetla informacje o profilu użytkownika hello.
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Dodaj metody toosign limit hello użytkownika

1. Dodaj następujące metody tooyour hello `MainWindow.xaml.cs` toosign limit hello użytkownika:

```csharp
/// <summary>
/// Sign out hello current user
/// </summary>
private void SignOutButton_Click(object sender, RoutedEventArgs e)
{
    if (App.PublicClientApp.Users.Any())
    {
        try
        {
            App.PublicClientApp.Remove(App.PublicClientApp.Users.FirstOrDefault());
            this.ResultText.Text = "User has signed-out";
            this.CallGraphButton.Visibility = Visibility.Visible;
            this.SignOutButton.Visibility = Visibility.Collapsed;
        }
        catch (MsalException ex)
        {
            ResultText.Text = $"Error signing-out user: {ex.Message}";
        }
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a>Więcej informacji dotyczących wylogowania

`SignOutButton_Click`Usuwa hello użytkownika z pamięci podręcznej użytkownika MSAL — to skutecznie poinformuje MSAL tooforget hello bieżącego użytkownika, tooacquire przyszłych żądania tokenu tylko powiedzie się, jeśli zawiera ona toobe interaktywnego.
Mimo że aplikacji hello w tym przykładzie obsługuje pojedynczego użytkownika, MSAL obsługuje scenariusze, gdzie wiele kont może być zalogowany na powitania jednocześnie — przykładem jest aplikacja poczty e-mail których użytkownik ma wiele kont.
<!--end-collapse-->

## <a name="display-basic-token-information"></a>Wyświetlanie informacji o tokenie podstawowe

1. Dodaj następujące metody tootooyour hello `MainWindow.xaml.cs` toodisplay podstawowe informacje o tokenie hello:

```csharp
/// <summary>
/// Display basic information contained in hello token
/// </summary>
private void DisplayBasicTokenInfo(AuthenticationResult authResult)
{
    TokenInfoText.Text = "";
    if (authResult != null)
    {
        TokenInfoText.Text += $"Name: {authResult.User.Name}" + Environment.NewLine;
        TokenInfoText.Text += $"Username: {authResult.User.DisplayableId}" + Environment.NewLine;
        TokenInfoText.Text += $"Token Expires: {authResult.ExpiresOn.ToLocalTime()}" + Environment.NewLine;
        TokenInfoText.Text += $"Access Token: {authResult.AccessToken}" + Environment.NewLine;
    }
}
```
<!--start-collapse-->
### <a name="more-information"></a>Więcej informacji

Tokeny nabyte za pośrednictwem *OpenID Connect* również zawierać małego podzbioru użytkownika toohello odpowiednich informacji. `DisplayBasicTokenInfo`zawiera podstawowe informacje zawarte w tokenie hello: na przykład hello użytkownika wyświetlane nazwy i Identyfikatora, jak również hello wygaśnięcia tokenu daty i hello ciąg reprezentujący tokenu dostępu hello samej siebie. Te informacje są wyświetlane dla toosee użytkownik. Naciśnij klawisz hello *wywołać Microsoft interfejsu API programu Graph* przycisk wielokrotnie i zobacz hello, ten sam token został ponownie dla kolejnych żądań. Można również sprawdzić Data wygaśnięcia hello rozszerzany podczas MSAL decyduje o czasie toorenew hello token nie jest.
<!--end-collapse-->

