---
title: 'Azure Active Directory B2C: rejestrowanie aplikacji | Microsoft Docs'
description: "Jak zarejestrować aplikację w usłudze Azure Active Directory B2C"
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
ms.openlocfilehash: 3d4fe2fa10d848c8b29e4d22d284c0d378f07ae0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a><span data-ttu-id="a0dc3-103">Azure Active Directory B2C: rejestrowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="a0dc3-103">Azure Active Directory B2C: Register your application</span></span>

<span data-ttu-id="a0dc3-104">Ten samouczek szybkiego startu pomaga zarejestrować aplikację w dzierżawie usługi Microsoft Azure Active Directory (Azure AD) B2C w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="a0dc3-105">Kiedy skończysz, Twoja aplikacja będzie zarejestrowana do użycia w dzierżawie usługi Azure B2C.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-105">When you're finished, your application is registered for use in the Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0dc3-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a0dc3-106">Prerequisites</span></span>

<span data-ttu-id="a0dc3-107">Aby utworzyć aplikację, która akceptuje tworzenie kont i logowanie użytkowników, musisz najpierw zarejestrować aplikację w dzierżawie usługi Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-107">To build an application that accepts consumer sign-up and sign-in, you first need to register the application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="a0dc3-108">Aby utworzyć własną dzierżawę, wykonaj kroki opisane w temacie [Tworzenie dzierżawy usługi Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a0dc3-108">Get your own tenant by using the steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="a0dc3-109">Aplikacje utworzone w bloku Azure AD B2C w witrynie Azure Portal muszą być zarządzane z tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-109">Applications created from the Azure AD B2C blade in the Azure portal must be managed from the same location.</span></span> <span data-ttu-id="a0dc3-110">Jeśli edytujesz aplikacje B2C przy użyciu programu PowerShell lub innego portalu, stają się one nieobsługiwane i przestają działać w usłudze Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-110">If you edit the B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="a0dc3-111">Szczegóły możesz znaleźć w sekcji [Uszkodzone aplikacje](#faulted-apps).</span><span class="sxs-lookup"><span data-stu-id="a0dc3-111">See details in the [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-to-b2c-settings"></a><span data-ttu-id="a0dc3-112">Przechodzenie do ustawień usługi B2C</span><span class="sxs-lookup"><span data-stu-id="a0dc3-112">Navigate to B2C settings</span></span>

<span data-ttu-id="a0dc3-113">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/) jako administrator globalny dzierżawy usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-113">Log in to the [Azure portal](https://portal.azure.com/) as the Global Administrator of the B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="a0dc3-114">Wybierz następne kroki na podstawie rejestrowanego typu aplikacji:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-114">Choose next steps based on the application type you are registering:</span></span>

* [<span data-ttu-id="a0dc3-115">Rejestrowanie aplikacji internetowej</span><span class="sxs-lookup"><span data-stu-id="a0dc3-115">Register a web application</span></span>](#register-a-web-app)
* [<span data-ttu-id="a0dc3-116">Rejestrowanie internetowego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a0dc3-116">Register a web API</span></span>](#register-a-web-api)
* [<span data-ttu-id="a0dc3-117">Rejestrowanie aplikacji mobilnej lub natywnej</span><span class="sxs-lookup"><span data-stu-id="a0dc3-117">Register a mobile or native application</span></span>](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a><span data-ttu-id="a0dc3-118">Rejestrowanie aplikacji internetowej</span><span class="sxs-lookup"><span data-stu-id="a0dc3-118">Register a web app</span></span>

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

<span data-ttu-id="a0dc3-119">Jeśli Twoja aplikacja internetowa wywołuje internetowy interfejs API zabezpieczony przez usługę Azure AD B2C, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-119">If your web application calls a web API secured by Azure AD B2C, perform these steps:</span></span>
   1. <span data-ttu-id="a0dc3-120">Utwórz wpis tajny aplikacji, przechodząc do bloku **Klucze** i klikając przycisk **Wygeneruj klucz**.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-120">Create an application secret by going to the **Keys** blade and clicking the **Generate Key** button.</span></span> <span data-ttu-id="a0dc3-121">Zanotuj wartość pola **Klucz aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-121">Make note of the **App key** value.</span></span> <span data-ttu-id="a0dc3-122">Użyj tej wartości jako wpisu tajnego aplikacji w kodzie Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-122">You use the value as the application secret in your application's code.</span></span>
   2. <span data-ttu-id="a0dc3-123">Kliknij pozycję **Dostęp do interfejsu API**, kliknij pozycję **Dodaj** i wybierz swój internetowy interfejs API oraz zakresy (uprawnienia).</span><span class="sxs-lookup"><span data-stu-id="a0dc3-123">Click **API Access**, click **Add**, and select your web API and scopes (permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="a0dc3-124">**Klucz tajny aplikacji** jest ważnym poświadczeniem zabezpieczeń i powinien być odpowiednio zabezpieczony.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-124">An **Application Secret** is an important security credential, and should be secured appropriately.</span></span>
> 

[<span data-ttu-id="a0dc3-125">Przejdź do **następnych kroków**</span><span class="sxs-lookup"><span data-stu-id="a0dc3-125">Jump to **next steps**</span></span>](#next-steps)

## <a name="register-a-web-api"></a><span data-ttu-id="a0dc3-126">Rejestrowanie internetowego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a0dc3-126">Register a web API</span></span>

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

<span data-ttu-id="a0dc3-127">Kliknij przycisk **Opublikowane zakresy**, aby w razie potrzeby dodać więcej zakresów.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-127">Click **Published scopes** to add more scopes as necessary.</span></span> <span data-ttu-id="a0dc3-128">Domyślnie jest definiowany zakres „user_impersonation”.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-128">By default, the "user_impersonation" scope is defined.</span></span> <span data-ttu-id="a0dc3-129">Zakres user_impersonation daje innym aplikacjom możliwość dostępu do tego interfejsu API w imieniu zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-129">The user_impersonation scope gives other applications the ability to access this api on behalf of the signed-in user.</span></span> <span data-ttu-id="a0dc3-130">Jeśli chcesz, możesz usunąć zakres user_impersonation.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-130">If you wish, the user_impersonation scope can be removed.</span></span>

[<span data-ttu-id="a0dc3-131">Przejdź do **następnych kroków**</span><span class="sxs-lookup"><span data-stu-id="a0dc3-131">Jump to **next steps**</span></span>](#next-steps)

## <a name="register-a-mobile-or-native-app"></a><span data-ttu-id="a0dc3-132">Rejestrowanie aplikacji mobilnej lub natywnej</span><span class="sxs-lookup"><span data-stu-id="a0dc3-132">Register a mobile or native app</span></span>

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[<span data-ttu-id="a0dc3-133">Przejdź do **następnych kroków**</span><span class="sxs-lookup"><span data-stu-id="a0dc3-133">Jump to **next steps**</span></span>](#next-steps)

## <a name="limitations"></a><span data-ttu-id="a0dc3-134">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="a0dc3-134">Limitations</span></span>

### <a name="choosing-a-web-app-or-api-reply-url"></a><span data-ttu-id="a0dc3-135">Wybieranie aplikacji internetowej lub adresu URL odpowiedzi interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a0dc3-135">Choosing a web app or api reply URL</span></span>

<span data-ttu-id="a0dc3-136">Obecnie aplikacje, które są zarejestrowane w usłudze Azure AD B2C, mają wartości adresów URL odpowiedzi ograniczone do określonego zestawu.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-136">Currently, apps that are registered with Azure AD B2C are restricted to a limited set of reply URL values.</span></span> <span data-ttu-id="a0dc3-137">Adres URL odpowiedzi dla aplikacji i usług internetowych musi zaczynać się od schematu `https` i wartości wszystkich adresów URL odpowiedzi muszą współużytkować jedną domenę DNS.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-137">The reply URL for web apps and services must begin with the scheme `https`, and all reply URL values must share a single DNS domain.</span></span> <span data-ttu-id="a0dc3-138">Na przykład nie można zarejestrować aplikacji internetowej z jednym z następujących adresów URL odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-138">For example, you cannot register a web app that has one of these reply URLs:</span></span>

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="a0dc3-139">System rejestracji porównuje całą nazwę DNS istniejącego adresu URL odpowiedzi z nazwą DNS dodawanego adresu URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-139">The registration system compares the whole DNS name of the existing reply URL to the DNS name of the reply URL that you are adding.</span></span> <span data-ttu-id="a0dc3-140">Żądanie dodania nazwy DNS zakończy się niepowodzeniem, jeśli będzie spełniony jeden z następujących warunków:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-140">The request to add the DNS name fails if either of the following conditions is true:</span></span>

* <span data-ttu-id="a0dc3-141">Cała nazwa DNS nowego adresu URL odpowiedzi nie będzie zgodna z nazwą DNS istniejącego adresu URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-141">The whole DNS name of the new reply URL does not match the DNS name of the existing reply URL.</span></span>
* <span data-ttu-id="a0dc3-142">Cała nazwa DNS nowego adresu URL odpowiedzi nie jest poddomeną istniejącego adresu URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-142">The whole DNS name of the new reply URL is not a subdomain of the existing reply URL.</span></span>

<span data-ttu-id="a0dc3-143">Na przykład jeśli aplikacja ma następujący adres URL odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-143">For example, if the app has this reply URL:</span></span>

`https://login.contoso.com`

<span data-ttu-id="a0dc3-144">Można dodać do niego adres w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-144">You can add to it, like this:</span></span>

`https://login.contoso.com/new`

<span data-ttu-id="a0dc3-145">W takim przypadku nazwa DNS jest idealnie zgodna.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-145">In this case, the DNS name matches exactly.</span></span> <span data-ttu-id="a0dc3-146">Można też zrobić tak:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-146">Or, you can do this:</span></span>

`https://new.login.contoso.com`

<span data-ttu-id="a0dc3-147">W takim przypadku przywoływana jest poddomena DNS domeny login.contoso.com. Jeśli chcesz mieć aplikację z adresami URL odpowiedzi login-east.contoso.com i login-west.contoso.com, musisz dodać następujące adresy URL w podanej kolejności:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-147">In this case, you're referring to a DNS subdomain of login.contoso.com. If you want to have an app that has login-east.contoso.com and login-west.contoso.com as reply URLs, you must add those reply URLs in this order:</span></span>

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="a0dc3-148">Dwa ostatnie adresy można dodać, ponieważ są poddomenami pierwszego adresu URL odpowiedzi, contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-148">You can add the latter two because they are subdomains of the first reply URL, contoso.com.</span></span>

### <a name="choosing-a-native-app-redirect-uri"></a><span data-ttu-id="a0dc3-149">Wybieranie identyfikatora URI przekierowania aplikacji natywnej</span><span class="sxs-lookup"><span data-stu-id="a0dc3-149">Choosing a native app redirect URI</span></span>

<span data-ttu-id="a0dc3-150">Istnieją dwie ważne kwestie, które należy wziąć pod uwagę podczas wybierania identyfikatora URI przekierowania dla aplikacji mobilych/natywnych:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-150">There are two important considerations when choosing a redirect URI for mobile/native applications:</span></span>

* <span data-ttu-id="a0dc3-151">**Unikatowość**: schemat identyfikatora URI przekierowania powinien być unikatowy dla każdej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-151">**Unique**: The scheme of the redirect URI should be unique for every application.</span></span> <span data-ttu-id="a0dc3-152">W naszym przykładzie (com.onmicrosoft.contoso.appname://przekierowanie/ścieżka) schematem jest fragment com.onmicrosoft.contoso.appname.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-152">In our example (com.onmicrosoft.contoso.appname://redirect/path), we use com.onmicrosoft.contoso.appname as the scheme.</span></span> <span data-ttu-id="a0dc3-153">Zalecamy stosowanie się do tego wzorca.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-153">We recommend following this pattern.</span></span> <span data-ttu-id="a0dc3-154">Jeśli dwie aplikacje mają ten sam schemat, użytkownik zobaczy okno dialogowe „Wybór aplikacji”.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-154">If two applications share the same scheme, the user sees a "choose app" dialog.</span></span> <span data-ttu-id="a0dc3-155">Jeśli użytkownik dokona nieprawidłowego wyboru, logowanie nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-155">If the user makes an incorrect choice, the login fails.</span></span>
* <span data-ttu-id="a0dc3-156">**Kompletność**: identyfikator URI przekierowania musi mieć schemat i ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-156">**Complete**: Redirect URI must have a scheme and a path.</span></span> <span data-ttu-id="a0dc3-157">Ścieżka musi zawierać co najmniej jeden ukośnik po nazwie domeny (na przykład identyfikator //contoso/ jest prawidłowy, ale identyfikator //contoso jest błędny).</span><span class="sxs-lookup"><span data-stu-id="a0dc3-157">The path must contain at least one forward slash after the domain (for example, //contoso/ works and //contoso fails).</span></span>

<span data-ttu-id="a0dc3-158">Upewnij się, że w identyfikatorze URI przekierowywania nie ma żadnych znaków specjalnych, takich jak podkreślenia.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-158">Ensure there are no special characters like underscores in the redirect uri.</span></span>

### <a name="faulted-apps"></a><span data-ttu-id="a0dc3-159">Uszkodzone aplikacje</span><span class="sxs-lookup"><span data-stu-id="a0dc3-159">Faulted apps</span></span>

<span data-ttu-id="a0dc3-160">NIE NALEŻY edytować aplikacji B2C:</span><span class="sxs-lookup"><span data-stu-id="a0dc3-160">B2C applications should NOT be edited:</span></span>

* <span data-ttu-id="a0dc3-161">W innych portalach zarządzania aplikacjami, takich jak [klasyczna witryna Azure Portal](https://manage.windowsazure.com/) i [portal rejestracji aplikacji](https://apps.dev.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="a0dc3-161">On other application management portals such as the [Azure classic portal](https://manage.windowsazure.com/) & the [Application Registration Portal](https://apps.dev.microsoft.com/).</span></span>
* <span data-ttu-id="a0dc3-162">Korzystanie z interfejsu API programu Graph lub programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0dc3-162">Using Graph API or PowerShell</span></span>

<span data-ttu-id="a0dc3-163">Jeśli poddasz edycji aplikację B2C w sposób opisany powyżej i spróbujesz ponownie edytować ją w bloku funkcji usługi Azure AD B2C w witrynie Azure Portal, stanie się ona uszkodzoną aplikacją i nie będzie można z niej korzystać w usłudze Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-163">If you edit the B2C application as described above and try to edit it again in the Azure AD B2C features blade on the Azure portal, it becomes a faulted app, and your application is no longer usable with Azure AD B2C.</span></span> <span data-ttu-id="a0dc3-164">Musisz usunąć taką aplikację i utworzyć ją ponownie.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-164">You have to delete the application and create it again.</span></span>

<span data-ttu-id="a0dc3-165">Aby usunąć aplikację, przejdź do [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/) i usuń ją tam.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-165">To delete the app, go to the [Application Registration Portal](https://apps.dev.microsoft.com/) and delete the application there.</span></span> <span data-ttu-id="a0dc3-166">Aby aplikacja była widoczna, musisz być jej właścicielem (a nie tylko administratorem dzierżawy).</span><span class="sxs-lookup"><span data-stu-id="a0dc3-166">In order for the application to be visible, you need to be the owner of the application (and not just an admin of the tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0dc3-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a0dc3-167">Next steps</span></span>

<span data-ttu-id="a0dc3-168">Po zarejestrowaniu aplikacji w usłudze Azure AD B2C możesz wykonać czynności opisane w jednym z [naszych samouczków szybkiego startu](active-directory-b2c-overview.md#get-started), aby rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="a0dc3-168">Now that you have an application registered with Azure AD B2C, you can complete one of [our quick-start tutorials](active-directory-b2c-overview.md#get-started) to get up and running.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a0dc3-169">Tworzenie aplikacji internetowej platformy ASP.NET z rejestrowaniem, logowaniem i resetowaniem hasła</span><span class="sxs-lookup"><span data-stu-id="a0dc3-169">Create an ASP.NET web app with sign-up, sign-in, and password reset</span></span>](active-directory-b2c-devquickstarts-web-dotnet-susi.md)