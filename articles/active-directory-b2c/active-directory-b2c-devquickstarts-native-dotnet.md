---
title: Azure Active Directory B2C | Dokumentacja firmy Microsoft
description: "Jak utworzyć aplikację pulpitu systemu Windows, która obejmuje logowania, rejestracji, i zarządzania profilami za pomocą usługi Azure Active Directory B2C."
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
ms.openlocfilehash: 8e2b5c704230ee2ba1395dc76a1551aaa8e7af7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="01192-103">Usługa Azure AD B2C: Tworzenie aplikacji klasycznej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="01192-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="01192-104">Za pomocą usługi Azure Active Directory (Azure AD) B2C, można dodać tożsamości samoobsługi zaawansowanych funkcji zarządzania do aplikacji pulpitu w kilku krótkich krokach.</span><span class="sxs-lookup"><span data-stu-id="01192-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features to your desktop app in a few short steps.</span></span> <span data-ttu-id="01192-105">W tym artykule opisano sposób tworzenia aplikacji "Lista zadań do wykonania".NET systemu Windows Presentation Foundation (WPF), która zawiera użytkowników rejestrację, logowanie i zarządzanie profilami.</span><span class="sxs-lookup"><span data-stu-id="01192-105">This article will show you how to create a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="01192-106">Aplikacja będzie zawierać obsługę rejestracji i logowania przy użyciu nazwy użytkownika lub adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="01192-106">The app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="01192-107">Zawiera również obsługę rejestracji i logowania przy użyciu kont społecznościowych, takich jak Facebook i Google.</span><span class="sxs-lookup"><span data-stu-id="01192-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="01192-108">Tworzenie katalogu usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="01192-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="01192-109">Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę.</span><span class="sxs-lookup"><span data-stu-id="01192-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="01192-110">Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i innych elementów.</span><span class="sxs-lookup"><span data-stu-id="01192-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="01192-111">Jeśli jeszcze go nie masz, [utwórz katalog usługi B2C](active-directory-b2c-get-started.md), zanim przejdziesz dalej.</span><span class="sxs-lookup"><span data-stu-id="01192-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="01192-112">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="01192-112">Create an application</span></span>
<span data-ttu-id="01192-113">Następnie musisz utworzyć aplikację w katalogu usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="01192-113">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="01192-114">Dzięki temu informacje wymagane do bezpiecznego komunikowania się z aplikacją będą przekazywane do usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01192-114">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="01192-115">Aby utworzyć aplikację, postępuj zgodnie z [tymi instrukcjami](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="01192-115">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="01192-116">Należy pamiętać o wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="01192-116">Be sure to:</span></span>

* <span data-ttu-id="01192-117">Obejmują **klientami** w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="01192-117">Include a **native client** in the application.</span></span>
* <span data-ttu-id="01192-118">Kopiuj **identyfikator URI przekierowania** `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="01192-118">Copy the **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="01192-119">Jest to domyślny adres URL dla tej próbki kodu.</span><span class="sxs-lookup"><span data-stu-id="01192-119">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="01192-120">Skopiuj **Identyfikator aplikacji** przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="01192-120">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="01192-121">Będzie potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="01192-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="01192-122">Tworzenie zasad</span><span class="sxs-lookup"><span data-stu-id="01192-122">Create your policies</span></span>
<span data-ttu-id="01192-123">W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="01192-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="01192-124">Ten przykładowy kod obejmuje trzy środowiska tożsamości: Zarejestruj się, zaloguj się i edytowanie profilu.</span><span class="sxs-lookup"><span data-stu-id="01192-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="01192-125">Musisz utworzyć zasady dla każdego typu zgodnie z opisem w [artykule o zasadach](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="01192-125">You need to create a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="01192-126">Podczas tworzenia trzech zbiorów zasad należy koniecznie:</span><span class="sxs-lookup"><span data-stu-id="01192-126">When you create the three policies, be sure to:</span></span>

* <span data-ttu-id="01192-127">W bloku dostawców tożsamości wybrać opcję **tworzenia konta przy użyciu identyfikatora użytkownika** lub **tworzenia konta przy użyciu adresu e-mail**.</span><span class="sxs-lookup"><span data-stu-id="01192-127">Choose either **User ID sign-up** or **Email sign-up** in the identity providers blade.</span></span>
* <span data-ttu-id="01192-128">Wybrać wartość **Nazwa wyświetlana** i inne atrybuty tworzenia konta w zasadach tworzenia konta.</span><span class="sxs-lookup"><span data-stu-id="01192-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="01192-129">Wybrać oświadczenia **Nazwa wyświetlana** i **Identyfikator obiektu** jako oświadczenia aplikacji dla wszystkich zasad.</span><span class="sxs-lookup"><span data-stu-id="01192-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="01192-130">Można również wybrać inne oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="01192-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="01192-131">Skopiować każdą utworzoną wartość **Nazwa** zasad.</span><span class="sxs-lookup"><span data-stu-id="01192-131">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="01192-132">Powinny zawierać prefiks `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="01192-132">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="01192-133">Te nazwy zasad będą potrzebne później.</span><span class="sxs-lookup"><span data-stu-id="01192-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="01192-134">Po pomyślnym utworzeniu trzech zasad możesz rozpocząć tworzenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="01192-134">After you have successfully created the three policies, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="01192-135">Pobieranie kodu</span><span class="sxs-lookup"><span data-stu-id="01192-135">Download the code</span></span>
<span data-ttu-id="01192-136">Kod używany w tym samouczku [jest przechowywany w serwisie GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="01192-136">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="01192-137">Aby samodzielnie tworzyć przykładowy kod w trakcie pracy, możesz [pobrać plik ZIP ze szkieletem projektu](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="01192-137">To build the sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="01192-138">Można również sklonować szkielet:</span><span class="sxs-lookup"><span data-stu-id="01192-138">You can also clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="01192-139">Ukończona aplikacja jest również [dostępna jako plik ZIP](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) lub w gałęzi `complete` tego samego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="01192-139">The completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on the `complete` branch of the same repository.</span></span>

<span data-ttu-id="01192-140">Po pobraniu przykładu kodu otwórz plik SLN programu Visual Studio, aby rozpocząć.</span><span class="sxs-lookup"><span data-stu-id="01192-140">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="01192-141">`TaskClient` Projekt jest aplikacji klasycznych WPF, którą użytkownik wchodzi w interakcję z.</span><span class="sxs-lookup"><span data-stu-id="01192-141">The `TaskClient` project is the WPF desktop application that the user interacts with.</span></span> <span data-ttu-id="01192-142">Do celów tego samouczka wywołuje zadań zaplecza interfejsu API sieci web, hostowana na platformie Azure, która przechowuje listy zadań do wykonania poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="01192-142">For the purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="01192-143">Nie jest potrzebne do tworzenia interfejsu API sieci web, mamy już będzie działać dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="01192-143">You do not need to build the web API, we already have it running for you.</span></span>

<span data-ttu-id="01192-144">Aby dowiedzieć się, jak interfejsu API sieci web bezpiecznie uwierzytelnia żądania przy użyciu usługi Azure AD B2C, zapoznaj się [interfejsu API sieci web wprowadzenie artykułu](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="01192-144">To learn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="01192-145">Zasady wykonywania</span><span class="sxs-lookup"><span data-stu-id="01192-145">Execute policies</span></span>
<span data-ttu-id="01192-146">Aplikacja komunikuje się z usługi Azure AD B2C przez wysyłanie komunikatów uwierzytelniania, które określają zasady, które mają być wykonywane jako część żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="01192-146">Your app communicates with Azure AD B2C by sending authentication messages that specify the policy they want to execute as part of the HTTP request.</span></span> <span data-ttu-id="01192-147">Dla aplikacji .NET, korzystając z podglądu biblioteki uwierzytelniania firmy Microsoft (MSAL) do wysyłania wiadomości uwierzytelniania OAuth 2.0, należy wykonać zasad i uzyskiwać tokeny, które mogą wywoływać interfejsy API sieci web.</span><span class="sxs-lookup"><span data-stu-id="01192-147">For .NET desktop applications, you can use the preview Microsoft Authentication Library (MSAL) to send OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="01192-148">Zainstaluj MSAL</span><span class="sxs-lookup"><span data-stu-id="01192-148">Install MSAL</span></span>
<span data-ttu-id="01192-149">Dodaj MSAL do `TaskClient` projektu przy użyciu konsoli Menedżera pakietów programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="01192-149">Add MSAL to the `TaskClient` project by using the Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="01192-150">Wprowadzanie szczegółów B2C</span><span class="sxs-lookup"><span data-stu-id="01192-150">Enter your B2C details</span></span>
<span data-ttu-id="01192-151">Otwórz plik `Globals.cs` i Zastąp wartości właściwości własne.</span><span class="sxs-lookup"><span data-stu-id="01192-151">Open the file `Globals.cs` and replace each of the property values with your own.</span></span> <span data-ttu-id="01192-152">Ta klasa jest używana w całym `TaskClient` wartości odwołania często używane.</span><span class="sxs-lookup"><span data-stu-id="01192-152">This class is used throughout `TaskClient` to reference commonly used values.</span></span>

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

### <a name="create-the-publicclientapplication"></a><span data-ttu-id="01192-153">Utwórz PublicClientApplication</span><span class="sxs-lookup"><span data-stu-id="01192-153">Create the PublicClientApplication</span></span>
<span data-ttu-id="01192-154">Podstawowy klasa MSAL jest `PublicClientApplication`.</span><span class="sxs-lookup"><span data-stu-id="01192-154">The primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="01192-155">Ta klasa reprezentuje aplikacji w systemie Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="01192-155">This class represents your application in the Azure AD B2C system.</span></span> <span data-ttu-id="01192-156">Gdy initalizes aplikacji, Utwórz wystąpienie `PublicClientApplication` w `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="01192-156">When the app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="01192-157">Może być używany w oknie.</span><span class="sxs-lookup"><span data-stu-id="01192-157">This can be used throughout the window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens to persist when the user closes the app,
        // we've extended the MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="01192-158">Inicjowanie przepływu rejestracji</span><span class="sxs-lookup"><span data-stu-id="01192-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="01192-159">Jeśli użytkownik zdecyduje się loguje się, chcesz zainicjować przepływu rejestracji, który korzysta z utworzonymi zasadami tworzenia konta.</span><span class="sxs-lookup"><span data-stu-id="01192-159">When a user opts to signs up, you want to initiate a sign-up flow that uses the sign-up policy you created.</span></span> <span data-ttu-id="01192-160">Za pomocą MSAL, możesz po prostu Wywołaj `pca.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="01192-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="01192-161">Parametry są przekazywane do `AcquireTokenAsync(...)` określić token, który zostanie wyświetlony, używane w żądanie uwierzytelnienia i inne zasady.</span><span class="sxs-lookup"><span data-stu-id="01192-161">The parameters you pass to `AcquireTokenAsync(...)` determine which token you receive, the policy used in the authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use the app's clientId here as the scope parameter, indicating that
        // you want a token to the your app's backend web API (represented by
        // the cloud hosted task API).  Use the UiOptions.ForceLogin flag to
        // indicate to MSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in the app that the user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When the request completes successfully, you can get user
        // information from the AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After the sign up successfully completes, display the user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of the policy.
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

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="01192-162">Inicjowanie przepływu logowania</span><span class="sxs-lookup"><span data-stu-id="01192-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="01192-163">W ten sam sposób, aby zainicjować tworzenia konta przepływu można zainicjować przepływu logowania.</span><span class="sxs-lookup"><span data-stu-id="01192-163">You can initiate a sign-in flow in the same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="01192-164">Kiedy użytkownik się zaloguje, należy to samo wywołanie do MSAL, teraz za pomocą zasad logowania:</span><span class="sxs-lookup"><span data-stu-id="01192-164">When a user signs in, make the same call to MSAL, this time by using your sign-in policy:</span></span>

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

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="01192-165">Zainicjować przepływ edycji profilu</span><span class="sxs-lookup"><span data-stu-id="01192-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="01192-166">Ponownie możesz wykonać edycji profil zasady w taki sam sposób:</span><span class="sxs-lookup"><span data-stu-id="01192-166">Again, you can execute an edit-profile policy in the same fashion:</span></span>

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

<span data-ttu-id="01192-167">We wszystkich tych przypadkach MSAL albo zwraca token w `AuthenticationResult` lub zgłasza wyjątek.</span><span class="sxs-lookup"><span data-stu-id="01192-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="01192-168">Zawsze uzyskać token z MSAL, można użyć `AuthenticationResult.User` obiekt, aby zaktualizować dane użytkownika w aplikacji, takich jak interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="01192-168">Each time you get a token from MSAL, you can use the `AuthenticationResult.User` object to update the user data in the app, such as the UI.</span></span> <span data-ttu-id="01192-169">Biblioteka ADAL buforuje token do użycia w innych częściach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="01192-169">ADAL also caches the token for use in other parts of the application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="01192-170">Sprawdź, czy tokeny przy uruchamianiu aplikacji</span><span class="sxs-lookup"><span data-stu-id="01192-170">Check for tokens on app start</span></span>
<span data-ttu-id="01192-171">Umożliwia także MSAL do śledzenia stanu logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="01192-171">You can also use MSAL to keep track of the user's sign-in state.</span></span>  <span data-ttu-id="01192-172">W tej aplikacji chcemy użytkownik pozostaje zalogowany, nawet po Zamknij aplikację i otwórz go ponownie.</span><span class="sxs-lookup"><span data-stu-id="01192-172">In this app, we want the user to remain signed in even after they close the app & re-open it.</span></span>  <span data-ttu-id="01192-173">Ponownie wewnątrz `OnInitialized` zastąpienia, użyj tego MSAL `AcquireTokenSilent` metodę sprawdzania dla pamięci podręcznej tokenów:</span><span class="sxs-lookup"><span data-stu-id="01192-173">Back inside the `OnInitialized` override, use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If the user has has a token cached with any policy, we'll display them as signed-in.
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
        // There are no tokens in the cache.  Proceed without calling the To Do list service.
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

## <a name="call-the-task-api"></a><span data-ttu-id="01192-174">Wywołanie interfejsu API zadań</span><span class="sxs-lookup"><span data-stu-id="01192-174">Call the task API</span></span>
<span data-ttu-id="01192-175">MSAL ma teraz używane do wykonywania zasad i uzyskiwać tokeny.</span><span class="sxs-lookup"><span data-stu-id="01192-175">You have now used MSAL to execute policies and get tokens.</span></span>  <span data-ttu-id="01192-176">Za jego pomocą tokeny te wywołania interfejsu API zadań, należy ponownie można użyć w MSAL `AcquireTokenSilent` metodę sprawdzania dla pamięci podręcznej tokenów:</span><span class="sxs-lookup"><span data-stu-id="01192-176">When you want to use one these tokens to call the task API, you can again use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want to check for a cached token, independent of whatever policy was used to acquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent to indicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch the exception and show the user a message.
    catch (MsalException ex)
    {
        // There is no access token in the cache, so prompt the user to sign-in.
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

<span data-ttu-id="01192-177">Po wywołaniu `AcquireTokenSilentAsync(...)` zakończy się pomyślnie i token został znaleziony w pamięci podręcznej, można dodać token do `Authorization` nagłówka żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="01192-177">When the call to `AcquireTokenSilentAsync(...)` succeeds and a token is found in the cache, you can add the token to the `Authorization` header of the HTTP request.</span></span> <span data-ttu-id="01192-178">Interfejs API sieci web zadań będzie używają tego nagłówka do uwierzytelniania żądań odczytu listy zadań do wykonania użytkownika:</span><span class="sxs-lookup"><span data-stu-id="01192-178">The task web API will use this header to authenticate the request to read the user's to-do list:</span></span>

```C#
    ...
    // Once the token has been returned by MSAL, add it to the http authorization header, before making the call to access the To Do list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call the To Do list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-the-user-out"></a><span data-ttu-id="01192-179">Wylogowanie użytkownika</span><span class="sxs-lookup"><span data-stu-id="01192-179">Sign the user out</span></span>
<span data-ttu-id="01192-180">Ponadto umożliwia MSAL kończenie sesji użytkownika z aplikacją, gdy użytkownik wybierze **Wyloguj**.</span><span class="sxs-lookup"><span data-stu-id="01192-180">Finally, you can use MSAL to end a user's session with the app when the user selects **Sign out**.</span></span>  <span data-ttu-id="01192-181">Korzystając z MSAL, jest to osiągane przez wyczyszczenie wszystkich tokenów z pamięci podręcznej tokenu:</span><span class="sxs-lookup"><span data-stu-id="01192-181">When using MSAL, this is accomplished by clearing all of the tokens from the token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of the user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in the browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update the UI to show the user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="01192-182">Uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="01192-182">Run the sample app</span></span>
<span data-ttu-id="01192-183">Na koniec Skompiluj i uruchom próbkę.</span><span class="sxs-lookup"><span data-stu-id="01192-183">Finally, build and run the sample.</span></span>  <span data-ttu-id="01192-184">Utwórz aplikację za pomocą nazwa użytkownika lub adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="01192-184">Sign up for the app by using an email address or user name.</span></span> <span data-ttu-id="01192-185">Wyloguj się i zaloguj się ponownie jako ten sam użytkownik.</span><span class="sxs-lookup"><span data-stu-id="01192-185">Sign out and sign back in as the same user.</span></span> <span data-ttu-id="01192-186">Edytuj profil użytkownika.</span><span class="sxs-lookup"><span data-stu-id="01192-186">Edit that user's profile.</span></span> <span data-ttu-id="01192-187">Wyloguj się i zaloguj przy użyciu innego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="01192-187">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="01192-188">Dodaj IDPs społecznościowych</span><span class="sxs-lookup"><span data-stu-id="01192-188">Add social IDPs</span></span>
<span data-ttu-id="01192-189">Obecnie aplikacji obsługuje wyłącznie użytkownika rejestracji i logowania używanego **kont lokalnych**.</span><span class="sxs-lookup"><span data-stu-id="01192-189">Currently, the app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="01192-190">Oto konta przechowywane w katalogu usługi B2C, korzystających z nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="01192-190">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="01192-191">Za pomocą usługi Azure AD B2C, można dodać obsługę innych dostawców tożsamości (IDPs) bez zmieniania żadnego kodu.</span><span class="sxs-lookup"><span data-stu-id="01192-191">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="01192-192">Aby dodać społecznościowych IDPs do aplikacji, Rozpocznij zgodnie z instrukcjami szczegółowe w tych artykułach.</span><span class="sxs-lookup"><span data-stu-id="01192-192">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="01192-193">Dla każdego dostawców tożsamości, które mają być obsługiwane musisz zarejestrować aplikację w tym systemie i Uzyskaj identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="01192-193">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="01192-194">Konfigurowanie usługi Facebook jako dostawca tożsamości</span><span class="sxs-lookup"><span data-stu-id="01192-194">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="01192-195">Konfigurowanie usługi Google jako dostawca tożsamości</span><span class="sxs-lookup"><span data-stu-id="01192-195">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="01192-196">Konfigurowanie usługi Amazon jako dostawca tożsamości</span><span class="sxs-lookup"><span data-stu-id="01192-196">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="01192-197">Konfigurowanie LinkedIn jako dostawca tożsamości</span><span class="sxs-lookup"><span data-stu-id="01192-197">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="01192-198">Po dodaniu dostawców tożsamości do katalogu usługi B2C należy edytować każdego z trzech zbiorów zasad uwzględnienie nowych IDPs, zgodnie z opisem w [artykule o zasadach](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="01192-198">After you add the identity providers to your B2C directory, you need to edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="01192-199">Po zapisaniu zasad, uruchom ponownie aplikację.</span><span class="sxs-lookup"><span data-stu-id="01192-199">After you save your policies, run the app again.</span></span> <span data-ttu-id="01192-200">Powinien zostać wyświetlony nowy IDPs, dodawane jako logowania oraz wrażenia opcji zapisywania w każdym z Twoją tożsamość.</span><span class="sxs-lookup"><span data-stu-id="01192-200">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="01192-201">Możesz eksperymentować z zasadami i obserwować efekty w aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="01192-201">You can experiment with your policies and observe the effects on your sample app.</span></span> <span data-ttu-id="01192-202">Dodaj lub usuń IDPs, manipulować oświadczenia aplikacji lub zmień atrybuty rejestracji.</span><span class="sxs-lookup"><span data-stu-id="01192-202">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="01192-203">Eksperymentu, aż zostanie wyświetlony, jak zasady, żądania uwierzytelniania i MSAL powiązać razem.</span><span class="sxs-lookup"><span data-stu-id="01192-203">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="01192-204">Próbka ukończone [jest dostępna jako plik .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="01192-204">For reference, the completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="01192-205">Można ją także sklonować z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="01192-205">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
