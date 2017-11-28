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
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="fa5b5-103">Usługa Azure AD B2C: Tworzenie aplikacji klasycznej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="fa5b5-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="fa5b5-104">Za pomocą usługi Azure Active Directory (Azure AD) B2C, można dodawać tożsamości samoobsługi zaawansowane funkcje tooyour pulpitu aplikacji do zarządzania w kilku krótkich krokach.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features tooyour desktop app in a few short steps.</span></span> <span data-ttu-id="fa5b5-105">W tym artykule opisano, jak toocreate aplikacji .NET systemu Windows Presentation Foundation (WPF) "Lista zadań do wykonania", który zawiera użytkownika rejestrację, logowanie i zarządzanie profilami.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-105">This article will show you how toocreate a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="fa5b5-106">Aplikacja Hello obejmuje obsługę rejestracji i logowania przy użyciu nazwy użytkownika lub adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-106">hello app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="fa5b5-107">Zawiera również obsługę rejestracji i logowania przy użyciu kont społecznościowych, takich jak Facebook i Google.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="fa5b5-108">Tworzenie katalogu usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="fa5b5-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="fa5b5-109">Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="fa5b5-110">Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i innych elementów.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="fa5b5-111">Jeśli jeszcze go nie masz, [utwórz katalog usługi B2C](active-directory-b2c-get-started.md), zanim przejdziesz dalej.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="fa5b5-112">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="fa5b5-112">Create an application</span></span>
<span data-ttu-id="fa5b5-113">Następnie należy toocreate aplikację w katalogu usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-113">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="fa5b5-114">Dzięki temu informacje usługi Azure AD, czy go wymaga toosecurely komunikować się z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-114">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="fa5b5-115">toocreate usługi aplikacji, wykonaj [tych instrukcji](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="fa5b5-115">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="fa5b5-116">Należy pamiętać o wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="fa5b5-116">Be sure to:</span></span>

* <span data-ttu-id="fa5b5-117">Obejmują **klientami** w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-117">Include a **native client** in hello application.</span></span>
* <span data-ttu-id="fa5b5-118">Kopiuj hello **identyfikator URI przekierowania** `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-118">Copy hello **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="fa5b5-119">Jest hello domyślny adres URL dla tego przykładu kodu.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-119">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="fa5b5-120">Kopiuj hello **identyfikator aplikacji** czyli przypisanej tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-120">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="fa5b5-121">Będzie potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="fa5b5-122">Tworzenie zasad</span><span class="sxs-lookup"><span data-stu-id="fa5b5-122">Create your policies</span></span>
<span data-ttu-id="fa5b5-123">W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="fa5b5-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="fa5b5-124">Ten przykładowy kod obejmuje trzy środowiska tożsamości: Zarejestruj się, zaloguj się i edytowanie profilu.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="fa5b5-125">Należy dla każdego typu toocreate zasady zgodnie z opisem w [artykule o zasadach](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="fa5b5-125">You need toocreate a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="fa5b5-126">Podczas tworzenia hello trzech zbiorów zasad należy koniecznie:</span><span class="sxs-lookup"><span data-stu-id="fa5b5-126">When you create hello three policies, be sure to:</span></span>

* <span data-ttu-id="fa5b5-127">Wybierz **identyfikator użytkownika rejestracji** lub **tworzenia konta E-mail** w bloku dostawców tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-127">Choose either **User ID sign-up** or **Email sign-up** in hello identity providers blade.</span></span>
* <span data-ttu-id="fa5b5-128">Wybrać wartość **Nazwa wyświetlana** i inne atrybuty tworzenia konta w zasadach tworzenia konta.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="fa5b5-129">Wybrać oświadczenia **Nazwa wyświetlana** i **Identyfikator obiektu** jako oświadczenia aplikacji dla wszystkich zasad.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="fa5b5-130">Można również wybrać inne oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="fa5b5-131">Kopiuj hello **nazwa** poszczególnych zasad po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-131">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="fa5b5-132">Powinien on mieć prefiks hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-132">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="fa5b5-133">Te nazwy zasad będą potrzebne później.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="fa5b5-134">Po pomyślnym utworzeniu hello trzy zasady, wszystko jest gotowe toobuild aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-134">After you have successfully created hello three policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="fa5b5-135">Pobierz kod hello</span><span class="sxs-lookup"><span data-stu-id="fa5b5-135">Download hello code</span></span>
<span data-ttu-id="fa5b5-136">Witaj kodu w tym samouczku [jest przechowywany w serwisie GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="fa5b5-136">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="fa5b5-137">Przykładowe hello toobuild podczas przejść, możesz [pobrać szkielet projektu jako plik .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="fa5b5-137">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="fa5b5-138">Można również sklonować szkielet hello:</span><span class="sxs-lookup"><span data-stu-id="fa5b5-138">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="fa5b5-139">Aplikacja Hello ukończone jest również [dostępny jako plik zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) lub na powitania `complete` gałęzi hello tego samego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-139">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

<span data-ttu-id="fa5b5-140">Po pobraniu hello przykładowy kod tooget plik SLN programu Visual Studio Otwórz hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-140">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="fa5b5-141">Witaj `TaskClient` projekt jest hello WPF aplikacja komputerowa, która hello użytkownik wchodzi w interakcję z.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-141">hello `TaskClient` project is hello WPF desktop application that hello user interacts with.</span></span> <span data-ttu-id="fa5b5-142">Do celów tego samouczka hello wywołuje zadań zaplecza interfejsu API sieci web, hostowana na platformie Azure, która przechowuje listy zadań do wykonania poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-142">For hello purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="fa5b5-143">Nie trzeba interfejsu API sieci web hello toobuild, mamy już będzie działać dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-143">You do not need toobuild hello web API, we already have it running for you.</span></span>

<span data-ttu-id="fa5b5-144">toolearn jak bezpiecznie interfejsu API sieci web uwierzytelnia żądania przy użyciu usługi Azure AD B2C, zapoznaj się z [interfejsu API sieci web wprowadzenie artykułu](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="fa5b5-144">toolearn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="fa5b5-145">Zasady wykonywania</span><span class="sxs-lookup"><span data-stu-id="fa5b5-145">Execute policies</span></span>
<span data-ttu-id="fa5b5-146">Aplikacja komunikuje się z usługi Azure AD B2C przez wysyłanie komunikatów uwierzytelniania, określających zasady hello mają tooexecute jako część żądania hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-146">Your app communicates with Azure AD B2C by sending authentication messages that specify hello policy they want tooexecute as part of hello HTTP request.</span></span> <span data-ttu-id="fa5b5-147">Aplikacje .NET, można użyć hello Podgląd komunikatów uwierzytelniania OAuth 2.0 toosend biblioteki uwierzytelniania firmy Microsoft (MSAL), wykonaj zasad i uzyskiwać tokeny tego wywołania interfejsów API sieci web.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-147">For .NET desktop applications, you can use hello preview Microsoft Authentication Library (MSAL) toosend OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="fa5b5-148">Zainstaluj MSAL</span><span class="sxs-lookup"><span data-stu-id="fa5b5-148">Install MSAL</span></span>
<span data-ttu-id="fa5b5-149">Dodaj MSAL toohello `TaskClient` projektu przy użyciu hello Konsola Menedżera pakietów programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-149">Add MSAL toohello `TaskClient` project by using hello Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="fa5b5-150">Wprowadzanie szczegółów B2C</span><span class="sxs-lookup"><span data-stu-id="fa5b5-150">Enter your B2C details</span></span>
<span data-ttu-id="fa5b5-151">Witaj Otwórz plik `Globals.cs` i Zastąp wartości właściwości hello własne.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-151">Open hello file `Globals.cs` and replace each of hello property values with your own.</span></span> <span data-ttu-id="fa5b5-152">Ta klasa jest używana w całym `TaskClient` tooreference najczęściej używanych wartości.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-152">This class is used throughout `TaskClient` tooreference commonly used values.</span></span>

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

### <a name="create-hello-publicclientapplication"></a><span data-ttu-id="fa5b5-153">Utwórz hello PublicClientApplication</span><span class="sxs-lookup"><span data-stu-id="fa5b5-153">Create hello PublicClientApplication</span></span>
<span data-ttu-id="fa5b5-154">podstawowy klasa MSAL Hello jest `PublicClientApplication`.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-154">hello primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="fa5b5-155">Ta klasa reprezentuje aplikacji w systemie hello Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-155">This class represents your application in hello Azure AD B2C system.</span></span> <span data-ttu-id="fa5b5-156">Gdy hello initalizes aplikacji, Utwórz wystąpienie `PublicClientApplication` w `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-156">When hello app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="fa5b5-157">Można to w całym hello okna.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-157">This can be used throughout hello window.</span></span>

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

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="fa5b5-158">Inicjowanie przepływu rejestracji</span><span class="sxs-lookup"><span data-stu-id="fa5b5-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="fa5b5-159">Gdy użytkownik zażąda toosigns w górę, ma tooinitiate rejestracji przepływ, który korzysta z utworzonymi zasadami hello rejestracji.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-159">When a user opts toosigns up, you want tooinitiate a sign-up flow that uses hello sign-up policy you created.</span></span> <span data-ttu-id="fa5b5-160">Za pomocą MSAL, możesz po prostu Wywołaj `pca.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="fa5b5-161">Witaj parametry przekazywane za`AcquireTokenAsync(...)` ustalić, które token zostanie wyświetlony, używane w hello żądań uwierzytelnienia i inne zasady hello.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-161">hello parameters you pass too`AcquireTokenAsync(...)` determine which token you receive, hello policy used in hello authentication request, and more.</span></span>

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

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="fa5b5-162">Inicjowanie przepływu logowania</span><span class="sxs-lookup"><span data-stu-id="fa5b5-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="fa5b5-163">Możesz zainicjować przepływ logowania w hello taki sam sposób, że zainicjować przepływ rejestracji.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-163">You can initiate a sign-in flow in hello same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="fa5b5-164">Gdy użytkownik się zaloguje, upewnij się, hello same wywołać tooMSAL, teraz za pomocą zasad logowania:</span><span class="sxs-lookup"><span data-stu-id="fa5b5-164">When a user signs in, make hello same call tooMSAL, this time by using your sign-in policy:</span></span>

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

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="fa5b5-165">Zainicjować przepływ edycji profilu</span><span class="sxs-lookup"><span data-stu-id="fa5b5-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="fa5b5-166">Ponownie, możesz wykonać zasad edycji profilu w hello sam sposób:</span><span class="sxs-lookup"><span data-stu-id="fa5b5-166">Again, you can execute an edit-profile policy in hello same fashion:</span></span>

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

<span data-ttu-id="fa5b5-167">We wszystkich tych przypadkach MSAL albo zwraca token w `AuthenticationResult` lub zgłasza wyjątek.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="fa5b5-168">Zawsze uzyskać token z MSAL, można użyć hello `AuthenticationResult.User` obiekt tooupdate hello użytkownika danych w aplikacji hello, takie jak hello interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-168">Each time you get a token from MSAL, you can use hello `AuthenticationResult.User` object tooupdate hello user data in hello app, such as hello UI.</span></span> <span data-ttu-id="fa5b5-169">ADAL również pamięci podręcznych hello token do użycia w innych częściach aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-169">ADAL also caches hello token for use in other parts of hello application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="fa5b5-170">Sprawdź, czy tokeny przy uruchamianiu aplikacji</span><span class="sxs-lookup"><span data-stu-id="fa5b5-170">Check for tokens on app start</span></span>
<span data-ttu-id="fa5b5-171">Umożliwia także śledzenie tookeep MSAL hello użytkownika logowania stanu.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-171">You can also use MSAL tookeep track of hello user's sign-in state.</span></span>  <span data-ttu-id="fa5b5-172">W tej aplikacji chcemy hello tooremain użytkownik zalogowany nawet po aplikacji hello Zamknij i otwórz go ponownie.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-172">In this app, we want hello user tooremain signed in even after they close hello app & re-open it.</span></span>  <span data-ttu-id="fa5b5-173">Ponownie wewnątrz hello `OnInitialized` zastąpienia, należy użyć w MSAL `AcquireTokenSilent` toocheck — metoda pamięci podręcznej tokenów:</span><span class="sxs-lookup"><span data-stu-id="fa5b5-173">Back inside hello `OnInitialized` override, use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

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

## <a name="call-hello-task-api"></a><span data-ttu-id="fa5b5-174">Wywołanie interfejsu API zadań hello</span><span class="sxs-lookup"><span data-stu-id="fa5b5-174">Call hello task API</span></span>
<span data-ttu-id="fa5b5-175">Teraz używanych MSAL tooexecute zasad i uzyskać tokeny.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-175">You have now used MSAL tooexecute policies and get tokens.</span></span>  <span data-ttu-id="fa5b5-176">Toouse jednego interfejsu API te tokeny toocall hello zadań, należy ponownie można użyć w MSAL `AcquireTokenSilent` toocheck — metoda pamięci podręcznej tokenów:</span><span class="sxs-lookup"><span data-stu-id="fa5b5-176">When you want toouse one these tokens toocall hello task API, you can again use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

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

<span data-ttu-id="fa5b5-177">Gdy hello wywołanie za`AcquireTokenSilentAsync(...)` zakończy się pomyślnie i token znajduje się w pamięci podręcznej hello, możesz dodać hello token toohello `Authorization` nagłówka żądania hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-177">When hello call too`AcquireTokenSilentAsync(...)` succeeds and a token is found in hello cache, you can add hello token toohello `Authorization` header of hello HTTP request.</span></span> <span data-ttu-id="fa5b5-178">Hello interfejsu API sieci web zadania będą korzystać z listy zadań do wykonania tego nagłówka tooauthenticate hello żądania tooread hello użytkownika:</span><span class="sxs-lookup"><span data-stu-id="fa5b5-178">hello task web API will use this header tooauthenticate hello request tooread hello user's to-do list:</span></span>

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a><span data-ttu-id="fa5b5-179">Witaj logowania użytkownika</span><span class="sxs-lookup"><span data-stu-id="fa5b5-179">Sign hello user out</span></span>
<span data-ttu-id="fa5b5-180">Ponadto można użyć MSAL tooend sesji użytkownika z aplikacją hello po wybraniu użytkownika hello **Wyloguj**.  Korzystając z MSAL, jest to osiągane przez wyczyszczenie wszystkich tokenów hello z pamięci podręcznej tokenu hello:</span><span class="sxs-lookup"><span data-stu-id="fa5b5-180">Finally, you can use MSAL tooend a user's session with hello app when hello user selects **Sign out**.  When using MSAL, this is accomplished by clearing all of hello tokens from hello token cache:</span></span>

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

## <a name="run-hello-sample-app"></a><span data-ttu-id="fa5b5-181">Uruchom hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="fa5b5-181">Run hello sample app</span></span>
<span data-ttu-id="fa5b5-182">Na koniec Skompiluj i uruchom próbkę hello.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-182">Finally, build and run hello sample.</span></span>  <span data-ttu-id="fa5b5-183">Załóż aplikacji hello przy użyciu nazwa użytkownika lub adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-183">Sign up for hello app by using an email address or user name.</span></span> <span data-ttu-id="fa5b5-184">Wyloguj się i zaloguj się ponownie jako hello sam użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-184">Sign out and sign back in as hello same user.</span></span> <span data-ttu-id="fa5b5-185">Edytuj profil użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-185">Edit that user's profile.</span></span> <span data-ttu-id="fa5b5-186">Wyloguj się i zaloguj przy użyciu innego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-186">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="fa5b5-187">Dodaj IDPs społecznościowych</span><span class="sxs-lookup"><span data-stu-id="fa5b5-187">Add social IDPs</span></span>
<span data-ttu-id="fa5b5-188">Obecnie aplikacji hello obsługuje tylko użytkownika rejestracji i logowania używanego **kont lokalnych**.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-188">Currently, hello app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="fa5b5-189">Oto konta przechowywane w katalogu usługi B2C, korzystających z nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-189">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="fa5b5-190">Za pomocą usługi Azure AD B2C, można dodać obsługę innych dostawców tożsamości (IDPs) bez zmieniania żadnego kodu.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-190">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="fa5b5-191">tooadd społecznościowych IDPs tooyour aplikacji, Rozpocznij od następujących hello szczegółowe instrukcje w tych artykułach.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-191">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="fa5b5-192">Dla każdego IDP ma toosupport, należy tooregister aplikacji w tym systemie i Uzyskaj identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-192">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="fa5b5-193">Konfigurowanie usługi Facebook jako dostawca tożsamości</span><span class="sxs-lookup"><span data-stu-id="fa5b5-193">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="fa5b5-194">Konfigurowanie usługi Google jako dostawca tożsamości</span><span class="sxs-lookup"><span data-stu-id="fa5b5-194">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="fa5b5-195">Konfigurowanie usługi Amazon jako dostawca tożsamości</span><span class="sxs-lookup"><span data-stu-id="fa5b5-195">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="fa5b5-196">Konfigurowanie LinkedIn jako dostawca tożsamości</span><span class="sxs-lookup"><span data-stu-id="fa5b5-196">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="fa5b5-197">Po dodaniu katalog tooyour B2C dostawców tożsamości hello należy tooedit każdego z trzech zbiorów zasad tooinclude hello IDPs nowe, jak opisano w hello [artykule o zasadach](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="fa5b5-197">After you add hello identity providers tooyour B2C directory, you need tooedit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="fa5b5-198">Po zapisaniu zasad, należy ponownie uruchomić aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-198">After you save your policies, run hello app again.</span></span> <span data-ttu-id="fa5b5-199">Powinny pojawić się hello IDPs nowe dodane jako opcje logowania i rejestracji w każdym doświadczeniami tożsamości.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-199">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="fa5b5-200">Możesz eksperymentować z zasadami i obserwować hello efekty w aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-200">You can experiment with your policies and observe hello effects on your sample app.</span></span> <span data-ttu-id="fa5b5-201">Dodaj lub usuń IDPs, manipulować oświadczenia aplikacji lub zmień atrybuty rejestracji.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-201">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="fa5b5-202">Eksperymentu, aż zostanie wyświetlony, jak zasady, żądania uwierzytelniania i MSAL powiązać razem.</span><span class="sxs-lookup"><span data-stu-id="fa5b5-202">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="fa5b5-203">Odwołania, hello ukończone próbki [jest dostępna jako plik .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="fa5b5-203">For reference, hello completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="fa5b5-204">Można ją także sklonować z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="fa5b5-204">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
