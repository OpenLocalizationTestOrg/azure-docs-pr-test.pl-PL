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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="0e9a1-103">Użyj hello biblioteki uwierzytelniania firmy Microsoft (MSAL) tooget token dla hello interfejsu API programu Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="0e9a1-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="0e9a1-104">W tej sekcji przedstawiono, jak toouse MSAL tooget token hello interfejsu API programu Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-104">This section shows how toouse MSAL tooget a token hello Microsoft Graph API.</span></span>

1.  <span data-ttu-id="0e9a1-105">W `MainWindow.xaml.cs`, Dodaj odwołanie hello MSAL biblioteki toohello klasy:</span><span class="sxs-lookup"><span data-stu-id="0e9a1-105">In `MainWindow.xaml.cs`, add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="0e9a1-106">Zastąp <code>MainWindow</code> kod z klasy:</span><span class="sxs-lookup"><span data-stu-id="0e9a1-106">Replace <code>MainWindow</code> class code with:</span></span>
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
### <a name="more-information"></a><span data-ttu-id="0e9a1-107">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="0e9a1-107">More Information</span></span>
#### <a name="getting-a-user-token-interactive"></a><span data-ttu-id="0e9a1-108">Pobieranie tokenu użytkownika interakcyjnego</span><span class="sxs-lookup"><span data-stu-id="0e9a1-108">Getting a user token interactive</span></span>
<span data-ttu-id="0e9a1-109">Wywoływanie hello `AcquireTokenAsync` — metoda powoduje monitowanie okna hello toosign użytkownika w.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-109">Calling hello `AcquireTokenAsync` method results in a window prompting hello user toosign in.</span></span> <span data-ttu-id="0e9a1-110">Aplikacje zwykle wymagają toosign użytkownika, w interaktywnie hello muszą tooaccess po raz pierwszy chronionego zasobu lub tooacquire dyskretnej operacji tokenu nie powiedzie się, (np. hasło użytkownika hello ważność).</span><span class="sxs-lookup"><span data-stu-id="0e9a1-110">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="0e9a1-111">Pobieranie tokenu użytkownika dyskretnej</span><span class="sxs-lookup"><span data-stu-id="0e9a1-111">Getting a user token silently</span></span>
<span data-ttu-id="0e9a1-112">`AcquireTokenSilentAsync`obsługuje przejęć tokenu i wznowienie bez interakcji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-112">`AcquireTokenSilentAsync` handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="0e9a1-113">Po `AcquireTokenAsync` jest wykonywana na powitania po raz pierwszy, `AcquireTokenSilentAsync` hello zwykle metodę tooobtain tokenów używanych tooaccess chronionych zasobów w kolejnych wywołaniach — jako toorequest wywołania lub odnowić tokeny są wprowadzane w trybie dyskretnym.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-113">After `AcquireTokenAsync` is executed for hello first time, `AcquireTokenSilentAsync` is hello usual method used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="0e9a1-114">Po pewnym czasie `AcquireTokenSilentAsync` zakończy się niepowodzeniem — np. użytkownika hello zalogował lub została zmieniona hasła na innym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-114">Eventually, `AcquireTokenSilentAsync` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="0e9a1-115">Gdy MSAL wykryje, że hello problem można rozwiązać, gdyż akcję interaktywne, jego generowane `MsalUiRequiredException`.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-115">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException`.</span></span> <span data-ttu-id="0e9a1-116">Aplikacja może obsłużyć tego wyjątku na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="0e9a1-116">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="0e9a1-117">Nawiązywanie połączeń z `AcquireTokenAsync` natychmiast, która powoduje monitowanie użytkownika hello toosign w.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-117">Make a call against `AcquireTokenAsync` immediately, which results in prompting hello user toosign-in.</span></span> <span data-ttu-id="0e9a1-118">Ten wzorzec jest zazwyczaj używany w aplikacji online w przypadku, gdy nie żadnej zawartości w trybie offline w aplikacji hello dostępnej dla użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-118">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="0e9a1-119">Hello próbki wygenerowane za pomocą tego Instalatora z przewodnikiem używa tego wzorca: Zobacz go w akcji powitania po raz pierwszy wykonać próbki hello: ponieważ żaden użytkownik nigdy używana aplikacja hello `PublicClientApp.Users.FirstOrDefault()` będzie zawierać wartości null i `MsalUiRequiredException` zostanie wygenerowany wyjątek.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-119">hello sample generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello sample: because no user ever used hello application, `PublicClientApp.Users.FirstOrDefault()` will contain a null value, and an `MsalUiRequiredException` exception will be thrown.</span></span> <span data-ttu-id="0e9a1-120">Witaj kodu w przykładowym hello, a następnie uchwytów hello wyjątku przez wywołanie metody `AcquireTokenAsync` powodujące monitowania użytkownika hello toosign w.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-120">hello code in hello sample then handles hello exception by calling `AcquireTokenAsync` resulting in prompting hello user toosign-in.</span></span>

2.  <span data-ttu-id="0e9a1-121">Aplikacje można również ustawić oznaczenia wizualne użytkownik toohello interakcyjne logowanie jest wymagany, dlatego hello użytkownik może wybrać toosign odpowiednich momentach hello w lub ponowić aplikacji hello `AcquireTokenSilentAsync` w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-121">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `AcquireTokenSilentAsync` at a later time.</span></span> <span data-ttu-id="0e9a1-122">Służy to zwykle gdy hello użytkownik może użyć innych funkcji aplikacji hello bez są zakłócone — na przykład Brak dostępnej zawartości w trybie offline w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-122">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="0e9a1-123">W takim przypadku hello użytkownika można określić, gdy mają toosign w tooaccess hello chroniony zasób, lub toorefresh hello przestarzałe informacje lub aplikacji można określić tooretry `AcquireTokenSilentAsync` przywrócenie sieci po są tymczasowo niedostępne.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-123">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `AcquireTokenSilentAsync` when network is restored after being unavailable temporarily.</span></span>
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="0e9a1-124">Wywołanie interfejsu API programu Microsoft Graph hello przy użyciu tokenu hello, który został uzyskany</span><span class="sxs-lookup"><span data-stu-id="0e9a1-124">Call hello Microsoft Graph API using hello token you just obtained</span></span>

1. <span data-ttu-id="0e9a1-125">Dodaj nową metodę hello poniżej tooyour `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-125">Add hello new method below tooyour `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="0e9a1-126">Witaj metoda jest używana toomake `GET` żądania interfejsu API programu Graph przy użyciu nagłówka autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="0e9a1-126">hello method is used toomake a `GET` request against Graph API using an Authorize header:</span></span>

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
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="0e9a1-127">Więcej informacji na temat nawiązywania połączenia przed chronionego interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="0e9a1-127">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="0e9a1-128">W tej przykładowej aplikacji hello `GetHttpContentWithToken` metoda jest używana toomake HTTP `GET` żądania dotyczącego zasobu chronionego wymagającego wywołującego zawartości toohello token, a następnie wróć hello.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-128">In this sample application, hello `GetHttpContentWithToken` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="0e9a1-129">Ta metoda dodaje token hello nabyte w hello *nagłówek autoryzacji HTTP*.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-129">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="0e9a1-130">Dla tego przykładu zasób hello jest hello interfejsu API programu Microsoft Graph *mnie* punktu końcowego — Wyświetla informacje o profilu użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-130">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="0e9a1-131">Dodaj metody toosign limit hello użytkownika</span><span class="sxs-lookup"><span data-stu-id="0e9a1-131">Add a method toosign out hello user</span></span>

1. <span data-ttu-id="0e9a1-132">Dodaj następujące metody tooyour hello `MainWindow.xaml.cs` toosign limit hello użytkownika:</span><span class="sxs-lookup"><span data-stu-id="0e9a1-132">Add hello following method tooyour `MainWindow.xaml.cs` toosign out hello user:</span></span>

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
### <a name="more-info-on-sign-out"></a><span data-ttu-id="0e9a1-133">Więcej informacji dotyczących wylogowania</span><span class="sxs-lookup"><span data-stu-id="0e9a1-133">More info on Sign-Out</span></span>

<span data-ttu-id="0e9a1-134">`SignOutButton_Click`Usuwa hello użytkownika z pamięci podręcznej użytkownika MSAL — to skutecznie poinformuje MSAL tooforget hello bieżącego użytkownika, tooacquire przyszłych żądania tokenu tylko powiedzie się, jeśli zawiera ona toobe interaktywnego.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-134">`SignOutButton_Click` removes hello user from MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>
<span data-ttu-id="0e9a1-135">Mimo że aplikacji hello w tym przykładzie obsługuje pojedynczego użytkownika, MSAL obsługuje scenariusze, gdzie wiele kont może być zalogowany na powitania jednocześnie — przykładem jest aplikacja poczty e-mail których użytkownik ma wiele kont.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-135">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed-in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="display-basic-token-information"></a><span data-ttu-id="0e9a1-136">Wyświetlanie informacji o tokenie podstawowe</span><span class="sxs-lookup"><span data-stu-id="0e9a1-136">Display Basic Token Information</span></span>

1. <span data-ttu-id="0e9a1-137">Dodaj następujące metody tootooyour hello `MainWindow.xaml.cs` toodisplay podstawowe informacje o tokenie hello:</span><span class="sxs-lookup"><span data-stu-id="0e9a1-137">Add hello following method tootooyour `MainWindow.xaml.cs` toodisplay basic information about hello token:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="0e9a1-138">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="0e9a1-138">More Information</span></span>

<span data-ttu-id="0e9a1-139">Tokeny nabyte za pośrednictwem *OpenID Connect* również zawierać małego podzbioru użytkownika toohello odpowiednich informacji.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-139">Tokens acquired via *OpenID Connect* also contain a small subset of information pertinent toohello user.</span></span> <span data-ttu-id="0e9a1-140">`DisplayBasicTokenInfo`zawiera podstawowe informacje zawarte w tokenie hello: na przykład hello użytkownika wyświetlane nazwy i Identyfikatora, jak również hello wygaśnięcia tokenu daty i hello ciąg reprezentujący tokenu dostępu hello samej siebie.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-140">`DisplayBasicTokenInfo` displays basic information contained in hello token: for example, hello user's display name and ID, as well as hello token expiration date and hello string representing hello access token itself.</span></span> <span data-ttu-id="0e9a1-141">Te informacje są wyświetlane dla toosee użytkownik.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-141">This information is displayed for you toosee.</span></span> <span data-ttu-id="0e9a1-142">Naciśnij klawisz hello *wywołać Microsoft interfejsu API programu Graph* przycisk wielokrotnie i zobacz hello, ten sam token został ponownie dla kolejnych żądań.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-142">You can hit hello *Call Microsoft Graph API* button multiple times and see that hello same token was reused for subsequent requests.</span></span> <span data-ttu-id="0e9a1-143">Można również sprawdzić Data wygaśnięcia hello rozszerzany podczas MSAL decyduje o czasie toorenew hello token nie jest.</span><span class="sxs-lookup"><span data-stu-id="0e9a1-143">You can also see hello expiration date being extended when MSAL decides it is time toorenew hello token.</span></span>
<!--end-collapse-->

