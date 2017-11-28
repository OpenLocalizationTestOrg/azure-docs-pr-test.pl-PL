---
title: aaaAzure Active Directory B2C | Dokumentacja firmy Microsoft
description: "Jak toobuild aplikacji sieci web, z konta-konta/logowania, profilu edycji, a hasło resetowania przy użyciu usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a><span data-ttu-id="770f9-103">Tworzenie aplikacji sieci web platformy ASP.NET z usługi Azure Active Directory B2C profilu rejestracji, logowania, edycji i resetowania hasła</span><span class="sxs-lookup"><span data-stu-id="770f9-103">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>

<span data-ttu-id="770f9-104">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="770f9-104">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="770f9-105">Dodawanie aplikacji sieci web tooyour funkcje tożsamości usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="770f9-105">Add Azure AD B2C identity features tooyour web app</span></span>
> * <span data-ttu-id="770f9-106">Rejestrowanie aplikacji sieci web w katalogu usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="770f9-106">Register your web app in your Azure AD B2C directory</span></span>
> * <span data-ttu-id="770f9-107">Tworzenie użytkownika konta-konta/logowania, edycji profilu i zasady resetowania hasła dla aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="770f9-107">Create a user sign-up/sign-in, profile edit, and password reset policy for your web app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="770f9-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="770f9-108">Prerequisites</span></span>

- <span data-ttu-id="770f9-109">Należy połączyć z tooan dzierżawy B2C konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="770f9-109">You must connect your B2C Tenant tooan Azure account.</span></span> <span data-ttu-id="770f9-110">Możesz utworzyć bezpłatne konto platformy Azure [tutaj](https://azure.microsoft.com/en-us/).</span><span class="sxs-lookup"><span data-stu-id="770f9-110">You can create a free Azure account [here](https://azure.microsoft.com/en-us/).</span></span>
- <span data-ttu-id="770f9-111">Należy [programu Microsoft Visual Studio](https://www.visualstudio.com/) lub podobnych program tooview i zmodyfikuj hello przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="770f9-111">You need [Microsoft Visual Studio](https://www.visualstudio.com/) or a similar program tooview and modify hello sample code.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="770f9-112">Tworzenie katalogu usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="770f9-112">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="770f9-113">Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę.</span><span class="sxs-lookup"><span data-stu-id="770f9-113">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="770f9-114">Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i inne.</span><span class="sxs-lookup"><span data-stu-id="770f9-114">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="770f9-115">Jeśli nie masz już, tworzenia katalogu B2C, przed kontynuowaniem w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="770f9-115">If you don't have one already, create a B2C directory before you continue in this guide.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> <span data-ttu-id="770f9-116">Należy tooconnect hello dzierżawy B2C tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="770f9-116">You need tooconnect hello B2C Tenant tooyour Azure subscription.</span></span> <span data-ttu-id="770f9-117">Po wybraniu **Utwórz**, wybierz pozycję hello **toomy dzierżawy łącze istniejącej usługi Azure AD B2C subskrypcji platformy Azure** opcji, a następnie w hello **dzierżawy usługi Azure AD B2C** listy rozwijanej wybierz pozycję Dzierżawca Hello ma tooassociate.</span><span class="sxs-lookup"><span data-stu-id="770f9-117">After selecting **Create**, select hello **Link an existing Azure AD B2C Tenant toomy Azure subscription** option, and then in hello **Azure AD B2C Tenant** drop down, select hello tenant you want tooassociate.</span></span>

## <a name="create-and-register-an-application"></a><span data-ttu-id="770f9-118">Tworzenie i rejestrowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="770f9-118">Create and register an application</span></span>

<span data-ttu-id="770f9-119">Następnie należy toocreate i rejestrowanie aplikacji hello w katalogu usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="770f9-119">Next, you need toocreate and register hello app in your B2C directory.</span></span> <span data-ttu-id="770f9-120">Zapewnia to informacji wymaganych przez program Azure AD B2C toosecurely komunikacji z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="770f9-120">This provides information that Azure AD B2C needs toosecurely communicate with your app.</span></span> 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

<span data-ttu-id="770f9-121">Gdy wszystko będzie gotowe, będzie mieć zarówno interfejs API i aplikacji natywnej w ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="770f9-121">When you are done, you will have both an API and a native application in your application settings.</span></span>

## <a name="create-policies-on-your-b2c-tenant"></a><span data-ttu-id="770f9-122">Tworzenie zasad na dzierżawę B2C</span><span class="sxs-lookup"><span data-stu-id="770f9-122">Create policies on your B2C tenant</span></span>

<span data-ttu-id="770f9-123">W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="770f9-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="770f9-124">Ten przykładowy kod obejmuje trzy środowiska tożsamości: **rejestracji i logowania**, **edycji profilu**, i **resetowania hasła**.</span><span class="sxs-lookup"><span data-stu-id="770f9-124">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit**, and **password reset**.</span></span>  <span data-ttu-id="770f9-125">Należy jedna zasada toocreate każdego typu zgodnie z opisem w hello [artykule o zasadach](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="770f9-125">You need toocreate one policy of each type, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="770f9-126">Dla każdej zasady można się, że atrybut nazwy wyświetlania hello tooselect lub oświadczeń i toocopy dół hello nazwę tej zasady do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="770f9-126">For each policy, be sure tooselect hello Display name attribute or claim, and toocopy down hello name of your policy for later use.</span></span>

### <a name="add-your-identity-providers"></a><span data-ttu-id="770f9-127">Dodaj użytkownika dostawców tożsamości</span><span class="sxs-lookup"><span data-stu-id="770f9-127">Add your identity providers</span></span>

<span data-ttu-id="770f9-128">Wybierz z ustawień **dostawców tożsamości** i wybierz polecenie zapisywania nazwy użytkownika lub rejestracji poczty E-mail.</span><span class="sxs-lookup"><span data-stu-id="770f9-128">From your settings, select **Identity Providers** and choose Username signup or Email signup.</span></span>

### <a name="create-a-sign-up-and-sign-in-policy"></a><span data-ttu-id="770f9-129">Tworzenie zasad rejestracji i logowania</span><span class="sxs-lookup"><span data-stu-id="770f9-129">Create a sign-up and sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="770f9-130">Utwórz profil edytowanie zasad</span><span class="sxs-lookup"><span data-stu-id="770f9-130">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="770f9-131">Utwórz zasady resetowania hasła</span><span class="sxs-lookup"><span data-stu-id="770f9-131">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

<span data-ttu-id="770f9-132">Po utworzeniu zasad, wszystko jest gotowe toobuild aplikacji.</span><span class="sxs-lookup"><span data-stu-id="770f9-132">After you create your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="770f9-133">Pobierz hello przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="770f9-133">Download hello sample code</span></span>

<span data-ttu-id="770f9-134">Witaj kod dla tego samouczka jest przechowywany w [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="770f9-134">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="770f9-135">Przykład Witaj można sklonować, uruchamiając:</span><span class="sxs-lookup"><span data-stu-id="770f9-135">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="770f9-136">Po pobraniu hello przykładowy kod tooget plik SLN programu Visual Studio Otwórz hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="770f9-136">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="770f9-137">Witaj plik rozwiązania zawiera dwa projekty: `TaskWebApp` i `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="770f9-137">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="770f9-138">`TaskWebApp`jest hello aplikację sieci web MVC hello użytkownik wchodzi w interakcję z.</span><span class="sxs-lookup"><span data-stu-id="770f9-138">`TaskWebApp` is hello MVC web application that hello user interacts with.</span></span> <span data-ttu-id="770f9-139">`TaskService`to interfejs API sieci web zaplecza aplikacji hello, który przechowuje listy zadań do wykonania poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="770f9-139">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="770f9-140">W tym artykule przedstawimy tylko hello `TaskWebApp` aplikacji.</span><span class="sxs-lookup"><span data-stu-id="770f9-140">This article will only discuss hello `TaskWebApp` application.</span></span> <span data-ttu-id="770f9-141">toolearn jak toobuild `TaskService` za pomocą usługi Azure AD B2C, zobacz [naszym samouczkiem interfejsu api sieci web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="770f9-141">toolearn how toobuild `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="update-code-toouse-your-tenant-and-policies"></a><span data-ttu-id="770f9-142">Aktualizowanie kodu toouse dzierżawy i zasady</span><span class="sxs-lookup"><span data-stu-id="770f9-142">Update code toouse your tenant and policies</span></span>

<span data-ttu-id="770f9-143">Naszej próbki jest skonfigurowany toouse hello zasady i klienta identyfikator dzierżawy naszych pokaz.</span><span class="sxs-lookup"><span data-stu-id="770f9-143">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="770f9-144">tooconnect on tooyour własne dzierżawy, należy tooopen `web.config` w hello `TaskWebApp` projektu i Zastąp hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="770f9-144">tooconnect it tooyour own tenant, you need tooopen `web.config` in hello `TaskWebApp` project and replace hello following values:</span></span>

* <span data-ttu-id="770f9-145">`ida:Tenant` nazwą dzierżawy</span><span class="sxs-lookup"><span data-stu-id="770f9-145">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="770f9-146">`ida:ClientId` identyfikatorem aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="770f9-146">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="770f9-147">`ida:ClientSecret` kluczem tajnym aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="770f9-147">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="770f9-148">`ida:SignUpSignInPolicyId` nazwą zasady tworzenia konta/logowania</span><span class="sxs-lookup"><span data-stu-id="770f9-148">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="770f9-149">`ida:EditProfilePolicyId` nazwą zasady edycji profilu</span><span class="sxs-lookup"><span data-stu-id="770f9-149">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="770f9-150">`ida:ResetPasswordPolicyId` nazwą zasady resetowania hasła</span><span class="sxs-lookup"><span data-stu-id="770f9-150">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="launch-hello-app"></a><span data-ttu-id="770f9-151">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="770f9-151">Launch hello app</span></span>
<span data-ttu-id="770f9-152">Z poziomu programu Visual Studio, uruchomienie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="770f9-152">From within Visual Studio, launch hello app.</span></span> <span data-ttu-id="770f9-153">Przejdź toohello kartę Lista zadań do wykonania i adres URl jest hello Uwaga: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id = *YourclientID*...</span><span class="sxs-lookup"><span data-stu-id="770f9-153">Navigate toohello To-Do List tab, and note hello URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span></span>

<span data-ttu-id="770f9-154">Załóż aplikacji hello przy użyciu poczty e-mail nazwy adres lub użytkownika.</span><span class="sxs-lookup"><span data-stu-id="770f9-154">Sign up for hello app by using your email address or user name.</span></span> <span data-ttu-id="770f9-155">Wyloguj się, a następnie zaloguj się ponownie i edytowanie profilu hello lub zresetować hasła hello.</span><span class="sxs-lookup"><span data-stu-id="770f9-155">Sign out, then sign in again and edit hello profile or reset hello password.</span></span> <span data-ttu-id="770f9-156">Wyloguj się i zaloguj się jako inny użytkownik.</span><span class="sxs-lookup"><span data-stu-id="770f9-156">Sign out and sign in as a different user.</span></span> 

## <a name="add-social-idps"></a><span data-ttu-id="770f9-157">Dodaj IDPs społecznościowych</span><span class="sxs-lookup"><span data-stu-id="770f9-157">Add social IDPs</span></span>

<span data-ttu-id="770f9-158">Obecnie obsługuje tylko użytkownik, rejestracji i logowania przy użyciu aplikacji hello **kont lokalnych**; kontom przechowywane w katalogu B2C, użyj nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="770f9-158">Currently, hello app supports only user sign-up and sign-in by using **local accounts**; accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="770f9-159">Za pomocą usługi Azure AD B2C, można dodać obsługę innych **dostawców tożsamości** (IDPs) bez zmieniania żadnego kodu.</span><span class="sxs-lookup"><span data-stu-id="770f9-159">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="770f9-160">tooadd społecznościowych IDPs tooyour aplikacji, Rozpocznij od następujących hello szczegółowe instrukcje w tych artykułach.</span><span class="sxs-lookup"><span data-stu-id="770f9-160">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="770f9-161">Dla każdego IDP ma toosupport, należy tooregister aplikacji w tym systemie i Uzyskaj identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="770f9-161">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="770f9-162">Konfigurowanie usługi Facebook jako dostawca tożsamości</span><span class="sxs-lookup"><span data-stu-id="770f9-162">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="770f9-163">Konfigurowanie usługi Google jako dostawca tożsamości</span><span class="sxs-lookup"><span data-stu-id="770f9-163">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="770f9-164">Konfigurowanie usługi Amazon jako dostawca tożsamości</span><span class="sxs-lookup"><span data-stu-id="770f9-164">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="770f9-165">Konfigurowanie LinkedIn jako dostawca tożsamości</span><span class="sxs-lookup"><span data-stu-id="770f9-165">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="770f9-166">Po dodaniu tooyour dostawców tożsamości hello katalogu B2C, edycji każdego z trzech zbiorów zasad tooinclude hello IDPs nowe, zgodnie z opisem w hello [artykule o zasadach](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="770f9-166">After you add hello identity providers tooyour B2C directory, edit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="770f9-167">Po zapisaniu zasad, należy ponownie uruchomić aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="770f9-167">After you save your policies, run hello app again.</span></span>  <span data-ttu-id="770f9-168">Powinny pojawić się hello IDPs nowe dodane jako opcje logowania i rejestracji w każdym doświadczeniami tożsamości.</span><span class="sxs-lookup"><span data-stu-id="770f9-168">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="770f9-169">Możesz eksperymentować z zasadami i obserwować wpływ hello w przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="770f9-169">You can experiment with your policies and observe hello effect on your sample app.</span></span> <span data-ttu-id="770f9-170">Dodaj lub usuń IDPs, manipulować oświadczenia aplikacji lub zmień atrybuty rejestracji.</span><span class="sxs-lookup"><span data-stu-id="770f9-170">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="770f9-171">Eksperymentu, aż zostanie wyświetlony, jak zasady, żądania uwierzytelniania i OWIN powiązać razem.</span><span class="sxs-lookup"><span data-stu-id="770f9-171">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

## <a name="sample-code-walkthrough"></a><span data-ttu-id="770f9-172">Przykładowy kod wskazówki</span><span class="sxs-lookup"><span data-stu-id="770f9-172">Sample code walkthrough</span></span>
<span data-ttu-id="770f9-173">następujące sekcje Hello Pokaż konfiguracji hello przykładowy kod aplikacji.</span><span class="sxs-lookup"><span data-stu-id="770f9-173">hello following sections show you how hello sample application code is configured.</span></span> <span data-ttu-id="770f9-174">Mogą wykorzystać te informacje jako przewodnika przy projektowaniu aplikacji w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="770f9-174">You may use this as a guide in your future app development.</span></span>

### <a name="add-authentication-support"></a><span data-ttu-id="770f9-175">Dodaj obsługę uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="770f9-175">Add authentication support</span></span>

<span data-ttu-id="770f9-176">Można teraz skonfigurować toouse Twojej aplikacji usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="770f9-176">You can now configure your app toouse Azure AD B2C.</span></span> <span data-ttu-id="770f9-177">Aplikacja komunikuje się z usługi Azure AD B2C, wysyłając żądania uwierzytelniania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="770f9-177">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="770f9-178">Witaj żądań jest wymagane przez środowisko użytkownika hello aplikacji chce tooexecute przez określenie hello zasad.</span><span class="sxs-lookup"><span data-stu-id="770f9-178">hello requests dictate hello user experience your app wants tooexecute by specifying hello policy.</span></span> <span data-ttu-id="770f9-179">Można użyć firmy Microsoft OWIN biblioteki toosend te żądania, wykonania zasady, zarządzania sesjami użytkownika i inne.</span><span class="sxs-lookup"><span data-stu-id="770f9-179">You can use Microsoft's OWIN library toosend these requests, execute policies, manage user sessions, and more.</span></span>

#### <a name="install-owin"></a><span data-ttu-id="770f9-180">Instalowanie interfejsu OWIN</span><span class="sxs-lookup"><span data-stu-id="770f9-180">Install OWIN</span></span>

<span data-ttu-id="770f9-181">toobegin, dodać hello OWIN oprogramowanie pośredniczące NuGet pakiety toohello projektu przy użyciu hello Konsola Menedżera pakietów programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="770f9-181">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a><span data-ttu-id="770f9-182">Dodawanie klasy początkowej OWIN</span><span class="sxs-lookup"><span data-stu-id="770f9-182">Add an OWIN startup class</span></span>

<span data-ttu-id="770f9-183">Dodaj toohello klasy interfejsu API OWIN uruchamiania o nazwie `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="770f9-183">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="770f9-184">Kliknij prawym przyciskiem myszy na powitania projektu, zaznacz **Dodaj** i **nowy element**, a następnie wyszukaj interfejs OWIN.</span><span class="sxs-lookup"><span data-stu-id="770f9-184">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="770f9-185">oprogramowanie pośredniczące OWIN Hello wywoła hello `Configuration(…)` metody podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="770f9-185">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="770f9-186">W naszym przykładzie możemy zmienić deklaracji klasy hello zbyt`public partial class Startup` i implementowane hello drugiej klasy hello w `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="770f9-186">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="770f9-187">Witaj wewnątrz `Configuration` metody dodaliśmy wywołanie za`ConfigureAuth`, który jest zdefiniowany w `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="770f9-187">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="770f9-188">Po modyfikacji hello `Startup.cs` wygląda jak poniżej hello:</span><span class="sxs-lookup"><span data-stu-id="770f9-188">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a><span data-ttu-id="770f9-189">Konfigurowanie oprogramowania pośredniczącego uwierzytelniania hello</span><span class="sxs-lookup"><span data-stu-id="770f9-189">Configure hello authentication middleware</span></span>

<span data-ttu-id="770f9-190">Witaj Otwórz plik `App_Start\Startup.Auth.cs` i wdrożenie hello `ConfigureAuth(...)` metody.</span><span class="sxs-lookup"><span data-stu-id="770f9-190">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="770f9-191">Witaj podane parametry `OpenIdConnectAuthenticationOptions` służyć jako współrzędne toocommunicate Twojej aplikacji w usłudze Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="770f9-191">hello parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="770f9-192">Jeśli nie określisz niektóre parametry, zostanie użyty hello wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="770f9-192">If you do not specify certain parameters, it will use hello default value.</span></span> <span data-ttu-id="770f9-193">Na przykład firma Microsoft nie określaj hello `ResponseType` w próbce hello, więc hello wartości domyślnej `code id_token` będzie używany w każdej tooAzure żądania wychodzącego AD B2C.</span><span class="sxs-lookup"><span data-stu-id="770f9-193">For example, we do not specify hello `ResponseType` in hello sample, so hello default value `code id_token` will be used in each outgoing request tooAzure AD B2C.</span></span>

<span data-ttu-id="770f9-194">Należy również tooset się uwierzytelniania plików cookie.</span><span class="sxs-lookup"><span data-stu-id="770f9-194">You also need tooset up cookie authentication.</span></span> <span data-ttu-id="770f9-195">oprogramowanie pośredniczące Hello OpenID Connect używa plików cookie sesji użytkownika toomaintain, między innymi.</span><span class="sxs-lookup"><span data-stu-id="770f9-195">hello OpenID Connect middleware uses cookies toomaintain user sessions, among other things.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

<span data-ttu-id="770f9-196">W `OpenIdConnectAuthenticationOptions` powyżej, definiujemy zestaw funkcji wywołania zwrotnego dla określonych powiadomień, które są odbierane przez oprogramowanie pośredniczące hello OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="770f9-196">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by hello OpenID Connect middleware.</span></span> <span data-ttu-id="770f9-197">Te zachowania są definiowane przy użyciu `OpenIdConnectAuthenticationNotifications` obiektu i przechowywane w hello `Notifications` zmiennej.</span><span class="sxs-lookup"><span data-stu-id="770f9-197">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into hello `Notifications` variable.</span></span> <span data-ttu-id="770f9-198">W naszym przykładzie definiujemy trzech różnych wywołań zwrotnych w zależności od hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="770f9-198">In our sample, we define three different callbacks depending on hello event.</span></span>

### <a name="using-different-policies"></a><span data-ttu-id="770f9-199">Przy użyciu różnych zasad</span><span class="sxs-lookup"><span data-stu-id="770f9-199">Using different policies</span></span>

<span data-ttu-id="770f9-200">Witaj `RedirectToIdentityProvider` powiadomień jest zawsze wyzwalane, gdy żądanie tooAzure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="770f9-200">hello `RedirectToIdentityProvider` notification is triggered whenever a request is made tooAzure AD B2C.</span></span> <span data-ttu-id="770f9-201">W funkcji wywołania zwrotnego hello `OnRedirectToIdentityProvider`, sprawdzamy w hello wychodzące połączenie, jeśli chcemy toouse inne zasady.</span><span class="sxs-lookup"><span data-stu-id="770f9-201">In hello callback function `OnRedirectToIdentityProvider`, we check in hello outgoing call if we want toouse a different policy.</span></span> <span data-ttu-id="770f9-202">W kolejności toodo hasła resetowania lub edytowanie profilu należy toouse hello odpowiednie zasady, takie jak zasady, zamiast hello domyślne "Rejestracji i logowania" zasady resetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="770f9-202">In order toodo a password reset or edit a profile, you need toouse hello corresponding policy such as hello password reset policy instead of hello default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="770f9-203">W naszym przykładzie gdy użytkownik chce tooreset hello haseł lub edytowanie profilu hello, dodamy zasad hello toouse możemy użyć w kontekście OWIN hello.</span><span class="sxs-lookup"><span data-stu-id="770f9-203">In our sample, when a user wants tooreset hello password or edit hello profile, we add hello policy we prefer toouse into hello OWIN context.</span></span> <span data-ttu-id="770f9-204">Który może odbywać się następujący hello:</span><span class="sxs-lookup"><span data-stu-id="770f9-204">That can be done by doing hello following:</span></span>

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="770f9-205">I można zaimplementować funkcja wywołania zwrotnego hello `OnRedirectToIdentityProvider` hello następujący:</span><span class="sxs-lookup"><span data-stu-id="770f9-205">And you can implement hello callback function `OnRedirectToIdentityProvider` by doing hello following:</span></span>

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a><span data-ttu-id="770f9-206">Obsługa kodów autoryzacji</span><span class="sxs-lookup"><span data-stu-id="770f9-206">Handling authorization codes</span></span>

<span data-ttu-id="770f9-207">Witaj `AuthorizationCodeReceived` powiadomień jest wyzwalane po odebraniu kod autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="770f9-207">hello `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="770f9-208">oprogramowanie pośredniczące Hello OpenID Connect nie obsługuje kodów wymianę tokenów dostępu.</span><span class="sxs-lookup"><span data-stu-id="770f9-208">hello OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="770f9-209">Należy ręcznie wymienić kod hello token hello w funkcji wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="770f9-209">You can manually exchange hello code for hello token in a callback function.</span></span> <span data-ttu-id="770f9-210">Aby uzyskać więcej informacji, zapoznaj się hello [dokumentacji](active-directory-b2c-devquickstarts-web-api-dotnet.md) objaśniający sposób.</span><span class="sxs-lookup"><span data-stu-id="770f9-210">For more information, please look at hello [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

### <a name="handling-errors"></a><span data-ttu-id="770f9-211">Obsługa błędów</span><span class="sxs-lookup"><span data-stu-id="770f9-211">Handling errors</span></span>

<span data-ttu-id="770f9-212">Witaj `AuthenticationFailed` powiadomień jest wyzwalane, gdy uwierzytelnianie nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="770f9-212">hello `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="770f9-213">Metody wywołania zwrotnego może obsługiwać błędy hello zgodnie z wymaganiami.</span><span class="sxs-lookup"><span data-stu-id="770f9-213">In its callback method, you can handle hello errors as you wish.</span></span> <span data-ttu-id="770f9-214">Należy jednak dodać wyboru dla kodu błędu hello `AADB2C90118`.</span><span class="sxs-lookup"><span data-stu-id="770f9-214">You should however add a check for hello error code `AADB2C90118`.</span></span> <span data-ttu-id="770f9-215">Podczas wykonywania hello zasad "Rejestracji i logowania" hello, użytkownik hello ma hello możliwości tooselect **nie pamiętasz hasła?** łącza.</span><span class="sxs-lookup"><span data-stu-id="770f9-215">During hello execution of hello "Sign-up or Sign-in" policy, hello user has hello opportunity tooselect a **Forgot your password?** link.</span></span> <span data-ttu-id="770f9-216">W takim przypadku usługi Azure AD B2C wysyła aplikacji, ten kod błędu wskazujący, czy aplikacji należy wysłać żądanie, zamiast zasady resetowania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="770f9-216">In this event, Azure AD B2C sends your app that error code indicating that your app should make a request using hello password reset policy instead.</span></span>

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a><span data-ttu-id="770f9-217">Wyślij tooAzure żądań uwierzytelniania AD</span><span class="sxs-lookup"><span data-stu-id="770f9-217">Send authentication requests tooAzure AD</span></span>

<span data-ttu-id="770f9-218">Aplikacja jest teraz toocommunicate poprawnie skonfigurowane w usłudze Azure AD B2C przy użyciu protokołu uwierzytelniania OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="770f9-218">Your app is now properly configured toocommunicate with Azure AD B2C by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="770f9-219">OWIN zarządza szczegóły hello obsługuje tworzenie komunikatów uwierzytelniania, sprawdzanie poprawności tokenów z usługi Azure AD B2C i podtrzymywanie sesji użytkowników.</span><span class="sxs-lookup"><span data-stu-id="770f9-219">OWIN manages hello details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="770f9-220">Wszystkie opcje, które pozostaje jest tooinitiate przepływu każdego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="770f9-220">All that remains is tooinitiate each user's flow.</span></span>

<span data-ttu-id="770f9-221">Gdy użytkownik wybierze **up logowania/logowania**, **edytowanie profilu**, lub **resetowania hasła** w aplikacji sieci web hello hello skojarzonych akcji jest wywoływana w `Controllers\AccountController.cs`:</span><span class="sxs-lookup"><span data-stu-id="770f9-221">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in hello web app, hello associated action is invoked in `Controllers\AccountController.cs`:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

<span data-ttu-id="770f9-222">Umożliwia także toosign OWIN limit hello użytkownika z aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="770f9-222">You can also use OWIN toosign out hello user from hello app.</span></span> <span data-ttu-id="770f9-223">W `Controllers\AccountController.cs` mamy:</span><span class="sxs-lookup"><span data-stu-id="770f9-223">In `Controllers\AccountController.cs` we have:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

<span data-ttu-id="770f9-224">W tooexplicitly dodanie wywoływanie zasad, można użyć `[Authorize]` tag w kontrolerach, który wykonuje zasadę, jeśli użytkownik hello nie jest zalogowany.</span><span class="sxs-lookup"><span data-stu-id="770f9-224">In addition tooexplicitly invoking a policy, you can use a `[Authorize]` tag in your controllers that executes a policy if hello user is not signed in.</span></span> <span data-ttu-id="770f9-225">Otwórz `Controllers\HomeController.cs` i Dodaj hello `[Authorize]` tag toohello oświadczeń kontrolera.</span><span class="sxs-lookup"><span data-stu-id="770f9-225">Open `Controllers\HomeController.cs` and add hello `[Authorize]` tag toohello claims controller.</span></span>  <span data-ttu-id="770f9-226">OWIN wybiera hello ostatnio zasady skonfigurowane podczas hello `[Authorize]` tag zostaje trafiony.</span><span class="sxs-lookup"><span data-stu-id="770f9-226">OWIN selects hello last policy configured when hello `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a><span data-ttu-id="770f9-227">Wyświetl informacje o użytkowniku</span><span class="sxs-lookup"><span data-stu-id="770f9-227">Display user information</span></span>

<span data-ttu-id="770f9-228">Podczas uwierzytelniania użytkowników za pomocą protokołu OpenID Connect, usługi Azure AD B2C zwraca identyfikator tokenu toohello aplikacja, która zawiera **oświadczeń**.</span><span class="sxs-lookup"><span data-stu-id="770f9-228">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token toohello app that contains **claims**.</span></span> <span data-ttu-id="770f9-229">Te są potwierdzeniami dotyczącymi hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="770f9-229">These are assertions about hello user.</span></span> <span data-ttu-id="770f9-230">Toopersonalize oświadczeń można użyć w swojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="770f9-230">You can use claims toopersonalize your app.</span></span>

<span data-ttu-id="770f9-231">Otwórz hello `Controllers\HomeController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="770f9-231">Open hello `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="770f9-232">Oświadczenia użytkowników są dostępne w kontrolerach za pośrednictwem hello `ClaimsPrincipal.Current` obiekt główny zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="770f9-232">You can access user claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

<span data-ttu-id="770f9-233">Są dostępne wszelkie oświadczenia, że aplikacja odbiera w hello sam sposób.</span><span class="sxs-lookup"><span data-stu-id="770f9-233">You can access any claim that your application receives in hello same way.</span></span>  <span data-ttu-id="770f9-234">Lista wszystkich oświadczeń hello odbiera aplikacji hello jest dostępne na powitania **oświadczeń** strony.</span><span class="sxs-lookup"><span data-stu-id="770f9-234">A list of all hello claims hello app receives is available for you on hello **Claims** page.</span></span>
