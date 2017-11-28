---
title: 'Azure Active Directory B2C: rejestrowanie aplikacji | Microsoft Docs'
description: "Jak tooregister aplikacji przy użyciu usługi Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a><span data-ttu-id="08182-103">Azure Active Directory B2C: rejestrowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="08182-103">Azure Active Directory B2C: Register your application</span></span>

<span data-ttu-id="08182-104">Ten samouczek szybkiego startu pomaga zarejestrować aplikację w dzierżawie usługi Microsoft Azure Active Directory (Azure AD) B2C w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="08182-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="08182-105">Po zakończeniu aplikacji są rejestrowane w dzierżawie powitalnych Azure B2C.</span><span class="sxs-lookup"><span data-stu-id="08182-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08182-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="08182-106">Prerequisites</span></span>

<span data-ttu-id="08182-107">toobuild aplikację, która akceptuje konsumenta rejestracji i logowania, należy najpierw aplikacji hello tooregister z dzierżawy usługi Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="08182-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="08182-108">Utworzyć własną dzierżawę za pomocą hello czynności opisane w temacie [tworzenie dzierżawy usługi Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="08182-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="08182-109">Musi być zarządzane aplikacje utworzone za pomocą bloku hello Azure AD B2C w portalu Azure hello z hello tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="08182-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="08182-110">Po zmodyfikowaniu aplikacji B2C hello przy użyciu programu PowerShell lub innego portalu stają się nieobsługiwane i nie działają usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="08182-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="08182-111">Zobacz szczegóły w hello [wystąpił błąd aplikacji](#faulted-apps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="08182-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="08182-112">Przejdź do ustawień tooB2C</span><span class="sxs-lookup"><span data-stu-id="08182-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="08182-113">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/) jako Administrator globalny dzierżawy hello B2C hello.</span><span class="sxs-lookup"><span data-stu-id="08182-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="08182-114">Wybierz następne kroki na podstawie typu aplikacji hello, rejestrowany:</span><span class="sxs-lookup"><span data-stu-id="08182-114">Choose next steps based on hello application type you are registering:</span></span>

* [<span data-ttu-id="08182-115">Rejestrowanie aplikacji internetowej</span><span class="sxs-lookup"><span data-stu-id="08182-115">Register a web application</span></span>](#register-a-web-app)
* [<span data-ttu-id="08182-116">Rejestrowanie internetowego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="08182-116">Register a web API</span></span>](#register-a-web-api)
* [<span data-ttu-id="08182-117">Rejestrowanie aplikacji mobilnej lub natywnej</span><span class="sxs-lookup"><span data-stu-id="08182-117">Register a mobile or native application</span></span>](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a><span data-ttu-id="08182-118">Rejestrowanie aplikacji internetowej</span><span class="sxs-lookup"><span data-stu-id="08182-118">Register a web app</span></span>

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

<span data-ttu-id="08182-119">Jeśli Twoja aplikacja internetowa wywołuje internetowy interfejs API zabezpieczony przez usługę Azure AD B2C, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="08182-119">If your web application calls a web API secured by Azure AD B2C, perform these steps:</span></span>
   1. <span data-ttu-id="08182-120">Utwórz klucz tajny aplikacji przez przejście toohello **klucze** bloku i klikając hello **Wygeneruj klucz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="08182-120">Create an application secret by going toohello **Keys** blade and clicking hello **Generate Key** button.</span></span> <span data-ttu-id="08182-121">Zwróć uwagę na powitania **klucz aplikacji** wartość.</span><span class="sxs-lookup"><span data-stu-id="08182-121">Make note of hello **App key** value.</span></span> <span data-ttu-id="08182-122">Wartość hello są używane jako klucz tajny aplikacji hello w kodzie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08182-122">You use hello value as hello application secret in your application's code.</span></span>
   2. <span data-ttu-id="08182-123">Kliknij pozycję **Dostęp do interfejsu API**, kliknij pozycję **Dodaj** i wybierz swój internetowy interfejs API oraz zakresy (uprawnienia).</span><span class="sxs-lookup"><span data-stu-id="08182-123">Click **API Access**, click **Add**, and select your web API and scopes (permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="08182-124">**Klucz tajny aplikacji** jest ważnym poświadczeniem zabezpieczeń i powinien być odpowiednio zabezpieczony.</span><span class="sxs-lookup"><span data-stu-id="08182-124">An **Application Secret** is an important security credential, and should be secured appropriately.</span></span>
> 

[<span data-ttu-id="08182-125">Przeskocz zbyt**następne kroki**</span><span class="sxs-lookup"><span data-stu-id="08182-125">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-web-api"></a><span data-ttu-id="08182-126">Rejestrowanie internetowego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="08182-126">Register a web API</span></span>

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

<span data-ttu-id="08182-127">Kliknij przycisk **opublikowane zakresy** tooadd więcej zakresów niezbędne.</span><span class="sxs-lookup"><span data-stu-id="08182-127">Click **Published scopes** tooadd more scopes as necessary.</span></span> <span data-ttu-id="08182-128">Domyślnie zakresu "user_impersonation" hello jest zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="08182-128">By default, hello "user_impersonation" scope is defined.</span></span> <span data-ttu-id="08182-129">zakres user_impersonation Hello daje innych aplikacji hello możliwości tooaccess ten interfejs api imieniu hello zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="08182-129">hello user_impersonation scope gives other applications hello ability tooaccess this api on behalf of hello signed-in user.</span></span> <span data-ttu-id="08182-130">Jeśli chcesz, można usunąć hello user_impersonation zakresu.</span><span class="sxs-lookup"><span data-stu-id="08182-130">If you wish, hello user_impersonation scope can be removed.</span></span>

[<span data-ttu-id="08182-131">Przeskocz zbyt**następne kroki**</span><span class="sxs-lookup"><span data-stu-id="08182-131">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-mobile-or-native-app"></a><span data-ttu-id="08182-132">Rejestrowanie aplikacji mobilnej lub natywnej</span><span class="sxs-lookup"><span data-stu-id="08182-132">Register a mobile or native app</span></span>

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[<span data-ttu-id="08182-133">Przeskocz zbyt**następne kroki**</span><span class="sxs-lookup"><span data-stu-id="08182-133">Jump too**next steps**</span></span>](#next-steps)

## <a name="limitations"></a><span data-ttu-id="08182-134">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="08182-134">Limitations</span></span>

### <a name="choosing-a-web-app-or-api-reply-url"></a><span data-ttu-id="08182-135">Wybieranie aplikacji internetowej lub adresu URL odpowiedzi interfejsu API</span><span class="sxs-lookup"><span data-stu-id="08182-135">Choosing a web app or api reply URL</span></span>

<span data-ttu-id="08182-136">Obecnie aplikacje, które są zarejestrowane w usłudze Azure AD B2C są ograniczone tooa ograniczony zestaw wartości adresu URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="08182-136">Currently, apps that are registered with Azure AD B2C are restricted tooa limited set of reply URL values.</span></span> <span data-ttu-id="08182-137">Witaj odpowiedzi z adresu URL dla usług i aplikacji sieci web musi rozpoczynać się od schematu hello `https`, i wszystkich odpowiedzi wartości adres URL musi współdzielenie jednej domeny DNS.</span><span class="sxs-lookup"><span data-stu-id="08182-137">hello reply URL for web apps and services must begin with hello scheme `https`, and all reply URL values must share a single DNS domain.</span></span> <span data-ttu-id="08182-138">Na przykład nie można zarejestrować aplikacji internetowej z jednym z następujących adresów URL odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="08182-138">For example, you cannot register a web app that has one of these reply URLs:</span></span>

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="08182-139">system rejestracji Hello porównuje hello całego nazwę DNS hello istniejących odpowiedzi adresu URL toohello nazwy DNS hello adresu URL odpowiedzi, który dodajesz.</span><span class="sxs-lookup"><span data-stu-id="08182-139">hello registration system compares hello whole DNS name of hello existing reply URL toohello DNS name of hello reply URL that you are adding.</span></span> <span data-ttu-id="08182-140">Witaj żądania tooadd Witaj nazwy DNS zakończy się niepowodzeniem, jeśli jest spełniony dowolny z hello następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="08182-140">hello request tooadd hello DNS name fails if either of hello following conditions is true:</span></span>

* <span data-ttu-id="08182-141">Hello całą nazwę DNS hello nowy adres URL odpowiedzi jest niezgodny z nazwą DNS hello hello istniejący adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="08182-141">hello whole DNS name of hello new reply URL does not match hello DNS name of hello existing reply URL.</span></span>
* <span data-ttu-id="08182-142">Hello całą nazwę DNS hello nowy adres URL odpowiedzi nie jest poddomeną hello istniejący adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="08182-142">hello whole DNS name of hello new reply URL is not a subdomain of hello existing reply URL.</span></span>

<span data-ttu-id="08182-143">Na przykład jeśli hello aplikacji ma ten adres URL odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="08182-143">For example, if hello app has this reply URL:</span></span>

`https://login.contoso.com`

<span data-ttu-id="08182-144">Można dodać tooit w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="08182-144">You can add tooit, like this:</span></span>

`https://login.contoso.com/new`

<span data-ttu-id="08182-145">W takim przypadku nazwa DNS hello są dokładnie.</span><span class="sxs-lookup"><span data-stu-id="08182-145">In this case, hello DNS name matches exactly.</span></span> <span data-ttu-id="08182-146">Można też zrobić tak:</span><span class="sxs-lookup"><span data-stu-id="08182-146">Or, you can do this:</span></span>

`https://new.login.contoso.com`

<span data-ttu-id="08182-147">W takim przypadku odwołujesz poddomenie DNS tooa login.contoso.com. Jeśli chcesz toohave aplikację, która ma logowania east.contoso.com i west.contoso.com logowania jako adresy URL odpowiedzi, należy dodać te adresy URL odpowiedzi w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="08182-147">In this case, you're referring tooa DNS subdomain of login.contoso.com. If you want toohave an app that has login-east.contoso.com and login-west.contoso.com as reply URLs, you must add those reply URLs in this order:</span></span>

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="08182-148">Ponieważ są one poddomen hello pierwszy adres URL odpowiedzi, można dodać hello tych dwóch contoso.com.</span><span class="sxs-lookup"><span data-stu-id="08182-148">You can add hello latter two because they are subdomains of hello first reply URL, contoso.com.</span></span>

### <a name="choosing-a-native-app-redirect-uri"></a><span data-ttu-id="08182-149">Wybieranie identyfikatora URI przekierowania aplikacji natywnej</span><span class="sxs-lookup"><span data-stu-id="08182-149">Choosing a native app redirect URI</span></span>

<span data-ttu-id="08182-150">Istnieją dwie ważne kwestie, które należy wziąć pod uwagę podczas wybierania identyfikatora URI przekierowania dla aplikacji mobilych/natywnych:</span><span class="sxs-lookup"><span data-stu-id="08182-150">There are two important considerations when choosing a redirect URI for mobile/native applications:</span></span>

* <span data-ttu-id="08182-151">**Unikatowy**: hello schemat identyfikatora URI przekierowania hello powinna być unikatowa dla każdej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08182-151">**Unique**: hello scheme of hello redirect URI should be unique for every application.</span></span> <span data-ttu-id="08182-152">W naszym przykładzie (com.onmicrosoft.contoso.appname://redirect/path) używamy com.onmicrosoft.contoso.appname hello schemat.</span><span class="sxs-lookup"><span data-stu-id="08182-152">In our example (com.onmicrosoft.contoso.appname://redirect/path), we use com.onmicrosoft.contoso.appname as hello scheme.</span></span> <span data-ttu-id="08182-153">Zalecamy stosowanie się do tego wzorca.</span><span class="sxs-lookup"><span data-stu-id="08182-153">We recommend following this pattern.</span></span> <span data-ttu-id="08182-154">Jeśli dwie aplikacje korzystają hello sam schemat, hello użytkownik widzi okna dialogowego "Wybierz aplikacji".</span><span class="sxs-lookup"><span data-stu-id="08182-154">If two applications share hello same scheme, hello user sees a "choose app" dialog.</span></span> <span data-ttu-id="08182-155">Użytkownik hello dokonuje nieprawidłowego wyboru, hello logowania nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="08182-155">If hello user makes an incorrect choice, hello login fails.</span></span>
* <span data-ttu-id="08182-156">**Kompletność**: identyfikator URI przekierowania musi mieć schemat i ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="08182-156">**Complete**: Redirect URI must have a scheme and a path.</span></span> <span data-ttu-id="08182-157">Ścieżka Hello musi zawierać co najmniej jeden ukośnik po hello domeny (na przykład działa //contoso/ i //contoso kończy się niepowodzeniem).</span><span class="sxs-lookup"><span data-stu-id="08182-157">hello path must contain at least one forward slash after hello domain (for example, //contoso/ works and //contoso fails).</span></span>

<span data-ttu-id="08182-158">Upewnij się, czy nie ma żadnych znaków specjalnych, takich jak identyfikator uri przekierowania podkreślenia w hello.</span><span class="sxs-lookup"><span data-stu-id="08182-158">Ensure there are no special characters like underscores in hello redirect uri.</span></span>

### <a name="faulted-apps"></a><span data-ttu-id="08182-159">Uszkodzone aplikacje</span><span class="sxs-lookup"><span data-stu-id="08182-159">Faulted apps</span></span>

<span data-ttu-id="08182-160">NIE NALEŻY edytować aplikacji B2C:</span><span class="sxs-lookup"><span data-stu-id="08182-160">B2C applications should NOT be edited:</span></span>

* <span data-ttu-id="08182-161">W innych portalach zarządzania aplikacjami, takich jak [klasyczna witryna Azure Portal](https://manage.windowsazure.com/) i [portal rejestracji aplikacji](https://apps.dev.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="08182-161">On other application management portals such as the [Azure classic portal](https://manage.windowsazure.com/) & the [Application Registration Portal](https://apps.dev.microsoft.com/).</span></span>
* <span data-ttu-id="08182-162">Korzystanie z interfejsu API programu Graph lub programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="08182-162">Using Graph API or PowerShell</span></span>

<span data-ttu-id="08182-163">Jeśli Edycja aplikacji hello B2C opisane powyżej, a następnie spróbuj tooedit hello go ponownie w bloku funkcji hello Azure AD B2C w portalu Azure, staje się błędnej aplikacji i aplikacja nie jest już możliwe z usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="08182-163">If you edit hello B2C application as described above and try tooedit it again in hello Azure AD B2C features blade on hello Azure portal, it becomes a faulted app, and your application is no longer usable with Azure AD B2C.</span></span> <span data-ttu-id="08182-164">Aplikacja hello toodelete i utwórz go ponownie.</span><span class="sxs-lookup"><span data-stu-id="08182-164">You have toodelete hello application and create it again.</span></span>

<span data-ttu-id="08182-165">Aplikacja hello toodelete, przejdź toohello [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/) i usuwania aplikacji hello istnieje.</span><span class="sxs-lookup"><span data-stu-id="08182-165">toodelete hello app, go toohello [Application Registration Portal](https://apps.dev.microsoft.com/) and delete hello application there.</span></span> <span data-ttu-id="08182-166">Aby toobe aplikacji hello jest widoczna należy toobe hello właściciel aplikacji hello (i nie tylko administrator dzierżawcy hello).</span><span class="sxs-lookup"><span data-stu-id="08182-166">In order for hello application toobe visible, you need toobe hello owner of hello application (and not just an admin of hello tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="08182-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="08182-167">Next steps</span></span>

<span data-ttu-id="08182-168">Teraz, po zarejestrowaniu aplikacji w usłudze Azure AD B2C można wykonać jedną z [naszych samouczków szybkiego startu](active-directory-b2c-overview.md#get-started) tooget do pracy.</span><span class="sxs-lookup"><span data-stu-id="08182-168">Now that you have an application registered with Azure AD B2C, you can complete one of [our quick-start tutorials](active-directory-b2c-overview.md#get-started) tooget up and running.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="08182-169">Tworzenie aplikacji internetowej platformy ASP.NET z rejestrowaniem, logowaniem i resetowaniem hasła</span><span class="sxs-lookup"><span data-stu-id="08182-169">Create an ASP.NET web app with sign-up, sign-in, and password reset</span></span>](active-directory-b2c-devquickstarts-web-dotnet-susi.md)