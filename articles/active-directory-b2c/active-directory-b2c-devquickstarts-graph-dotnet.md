---
title: "Usługi Azure Active Directory B2C: Interfejs API Graph użycia | Dokumentacja firmy Microsoft"
description: "Sposób wywołania interfejsu API programu Graph dla dzierżawy B2C przy użyciu tożsamości aplikacji aby zautomatyzować proces."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: c838fcad21875c4f813159ad78d4c87129a40a86
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-use-the-graph-api"></a><span data-ttu-id="cbcbd-103">Usługi Azure AD B2C: Interfejs API Graph użycia</span><span class="sxs-lookup"><span data-stu-id="cbcbd-103">Azure AD B2C: Use the Graph API</span></span>
<span data-ttu-id="cbcbd-104">Dzierżaw usługi Azure Active Directory (Azure AD) B2C zazwyczaj bardzo duże.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-104">Azure Active Directory (Azure AD) B2C tenants tend to be very large.</span></span> <span data-ttu-id="cbcbd-105">Oznacza to, że wiele typowych zadań zarządzania dzierżawy należy wykonać programowo.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-105">This means that many common tenant management tasks need to be performed programmatically.</span></span> <span data-ttu-id="cbcbd-106">Podstawowy przykład to zarządzanie użytkownikami.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-106">A primary example is user management.</span></span> <span data-ttu-id="cbcbd-107">Konieczne może być migrację istniejącego magazynu użytkownika do dzierżawy B2C.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-107">You might need to migrate an existing user store to a B2C tenant.</span></span> <span data-ttu-id="cbcbd-108">Możesz udostępniać rejestracja użytkownika na stronie i tworzenia kont użytkowników w katalogu usługi Azure AD B2C w tle.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-108">You may want to host user registration on your own page and create user accounts in your Azure AD B2C directory behind the scenes.</span></span> <span data-ttu-id="cbcbd-109">Te typy zadań muszą mieć możliwość tworzenia, odczytu, aktualizacji i usuwania kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-109">These types of tasks require the ability to create, read, update, and delete user accounts.</span></span> <span data-ttu-id="cbcbd-110">Można wykonywać te zadania przy użyciu interfejsu API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-110">You can do these tasks by using the Azure AD Graph API.</span></span>

<span data-ttu-id="cbcbd-111">Dla dzierżawcy usługi B2C istnieją dwa tryby głównej komunikowania się z interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-111">For B2C tenants, there are two primary modes of communicating with the Graph API.</span></span>

* <span data-ttu-id="cbcbd-112">Interaktywny, jednokrotnego uruchamiania zadań powinny działać jako konto administratora w dzierżawie usługi B2C należy wykonać zadania.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-112">For interactive, run-once tasks, you should act as an administrator account in the B2C tenant when you perform the tasks.</span></span> <span data-ttu-id="cbcbd-113">Ten tryb wymaga administratorem, aby zalogować się przy użyciu poświadczeń, zanim które administrator może wykonać wszelkie wywołania interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-113">This mode requires an administrator to sign in with credentials before that admin can perform any calls to the Graph API.</span></span>
* <span data-ttu-id="cbcbd-114">Zautomatyzowane, ciągłe zadania należy używać pewien typ konta usługi, które dostarczają niezbędne uprawnienia do wykonywania zadań zarządzania.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-114">For automated, continuous tasks, you should use some type of service account that you provide with the necessary privileges to perform management tasks.</span></span> <span data-ttu-id="cbcbd-115">W usłudze Azure AD możesz to zrobić, rejestrowanie aplikacji i uwierzytelniania w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-115">In Azure AD, you can do this by registering an application and authenticating to Azure AD.</span></span> <span data-ttu-id="cbcbd-116">Jest to zrobić za pomocą **identyfikator aplikacji** używającą [przyznania poświadczeń klienta OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="cbcbd-116">This is done by using an **Application ID** that uses the [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="cbcbd-117">W takim przypadku aplikacja działa jako sam nie jako użytkownik, do wywołania interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-117">In this case, the application acts as itself, not as a user, to call the Graph API.</span></span>

<span data-ttu-id="cbcbd-118">W tym artykule omówiono sposób wykonywania przypadek użycia automatycznego.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-118">In this article, we'll discuss how to perform the automated-use case.</span></span> <span data-ttu-id="cbcbd-119">Aby zademonstrować, możemy utworzyć .NET 4.5 `B2CGraphClient` wykonująca użytkownika tworzenia, odczytu, aktualizacji i usuwania (CRUD) operacji.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-119">To demonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="cbcbd-120">Klient ma interfejs wiersza polecenia systemu Windows (CLI) umożliwiający różne metody invoke.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-120">The client will have a Windows command-line interface (CLI) that allows you to invoke various methods.</span></span> <span data-ttu-id="cbcbd-121">Jednak kod jest zapisywany zachowują się w sposób nieinteraktywne, automatycznej.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-121">However, the code is written to behave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="cbcbd-122">Uzyskiwanie dzierżawy usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="cbcbd-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="cbcbd-123">Przed tworzenia aplikacji lub użytkowników lub w ogóle interakcję z usługą Azure AD, konieczne będzie dzierżawy usługi Azure AD B2C i konto administratora globalnego w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in the tenant.</span></span> <span data-ttu-id="cbcbd-124">Jeśli nie masz już, dzierżawcy [wprowadzenie do usługi Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cbcbd-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="cbcbd-125">Zarejestrować aplikację w dzierżawie</span><span class="sxs-lookup"><span data-stu-id="cbcbd-125">Register your application in your tenant</span></span>
<span data-ttu-id="cbcbd-126">Po umieszczeniu dzierżawy B2C, należy zarejestrować aplikację za pośrednictwem [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cbcbd-126">After you have a B2C tenant, you need to register your application via the [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbcbd-127">Aby używać interfejsu API programu Graph z dzierżawy usługi B2C, należy zarejestrować dedykowanej aplikacji przy użyciu ogólnych *rejestracji aplikacji* bloku w portalu Azure **nie** usługi Azure AD B2C  *Aplikacje* bloku.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-127">To use the Graph API with your B2C tenant, you will need to register a dedicated application by using the generic *App Registrations* blade in the Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="cbcbd-128">Nie można użyć ponownie już istniejących aplikacji B2C, zarejestrowanych w usłudze Azure AD B2C *aplikacji* bloku.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-128">You can't reuse the already-existing B2C applications that you registered in the Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="cbcbd-129">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cbcbd-129">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cbcbd-130">Wybierz dzierżawy usługi Azure AD B2C, wybierając konto w prawym górnym rogu strony.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-130">Choose your Azure AD B2C tenant by selecting your account in the top right corner of the page.</span></span>
3. <span data-ttu-id="cbcbd-131">W okienku nawigacji po lewej stronie wybierz **więcej usług**, kliknij przycisk **rejestracji aplikacji**i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-131">In the left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="cbcbd-132">Postępuj zgodnie z monitami i utwórz nową aplikację.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-132">Follow the prompts and create a new application.</span></span> 
    1. <span data-ttu-id="cbcbd-133">Wybierz **aplikacji w sieci Web / interfejs API** jako typ aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-133">Select **Web App / API** as the Application Type.</span></span>    
    2. <span data-ttu-id="cbcbd-134">Podaj **żadnego identyfikator URI przekierowania** (np. https://B2CGraphAPI), ponieważ nie jest to potrzebne w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="cbcbd-135">Aplikacja zostanie teraz zostanie wyświetlona lista aplikacji, kliknij przycisk w celu uzyskania **identyfikator aplikacji** (znanej także jako identyfikator klienta).</span><span class="sxs-lookup"><span data-stu-id="cbcbd-135">The application will now show up in the list of applications, click on it to obtain the **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="cbcbd-136">Skopiuj go, ponieważ będzie on potrzebny w dalszej części artykułu.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="cbcbd-137">W bloku ustawienia kliknij **klucze** i Dodaj nowy klucz (znanej także jako klucz tajny klienta).</span><span class="sxs-lookup"><span data-stu-id="cbcbd-137">In the Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="cbcbd-138">Jest on również kopiowany do użycia w dalszej części artykułu.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="cbcbd-139">Skonfiguruj tworzenie, odczytywanie i aktualizowanie uprawnień dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="cbcbd-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="cbcbd-140">Teraz musisz skonfigurować aplikację, aby pobrać wszystkie wymagane uprawnienia do tworzenia, odczytu, aktualizacji i usuwania użytkowników.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-140">Now you need to configure your application to get all the required permissions to create, read, update and delete users.</span></span>

1. <span data-ttu-id="cbcbd-141">Kontynuowanie w bloku rejestracji aplikacji w portalu Azure, wybierz aplikację.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-141">Continuing in the Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="cbcbd-142">W bloku ustawienia kliknij **wymagane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-142">In the Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="cbcbd-143">W bloku wymaganych uprawnień, kliknij na **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-143">In the Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="cbcbd-144">W bloku Włącz dostęp wybierz **Odczyt i zapis danych katalogu** zgody **uprawnienia aplikacji** i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-144">In the Enable Access  blade, select the **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="cbcbd-145">Ponadto w bloku wymaganych uprawnień, kliknij na **udzielanie uprawnień** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-145">Finally, back in the Required permissions blade, click on the **Grant Permissions** button.</span></span>

<span data-ttu-id="cbcbd-146">Teraz masz aplikację, która ma uprawnienia do tworzenia, odczytu i aktualizacji użytkowników z dzierżawy usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-146">You now have an application that has permission to create, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="cbcbd-147">Skonfiguruj uprawnienia do usuwania aplikacji</span><span class="sxs-lookup"><span data-stu-id="cbcbd-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="cbcbd-148">Obecnie *Odczyt i zapis danych katalogu* uprawnienie jest **nie** obejmują możliwość czy żadnych usunięć, takich jak usuwanie użytkowników.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-148">Currently, the *Read and write directory data* permission does **NOT** include the ability to do any deletions such as deleting users.</span></span> <span data-ttu-id="cbcbd-149">Jeśli chcesz nadać aplikacji możliwość usunięcia użytkowników, należy wykonać te dodatkowe kroki, które wymagają programu PowerShell, w przeciwnym razie możesz przejść do następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-149">If you want to give your application the ability to delete users, you'll need to do these extra steps that involve PowerShell, otherwise, you can skip to the next section.</span></span>

<span data-ttu-id="cbcbd-150">Najpierw należy pobrać i zainstalować [Microsoft Online Services Asystenta logowania](http://go.microsoft.com/fwlink/?LinkID=286152).</span><span class="sxs-lookup"><span data-stu-id="cbcbd-150">First, download and install the [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="cbcbd-151">Następnie Pobierz i zainstaluj [64-bitowy moduł usługi Azure Active Directory dla środowiska Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="cbcbd-151">Then download and install the [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="cbcbd-152">Po zainstalowaniu modułu programu PowerShell, Otwórz program PowerShell i połącz się dzierżawy usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-152">After you install the PowerShell module, open PowerShell and connect to your B2C tenant.</span></span> <span data-ttu-id="cbcbd-153">Po uruchomieniu `Get-Credential`, zostanie wyświetlony monit dla nazwy użytkownika i hasła, wprowadź nazwę użytkownika i hasło konta administratora dzierżawy B2C.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter the user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbcbd-154">Należy użyć konta administratora dzierżawy B2C, która jest **lokalnego** do dzierżawy B2C.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-154">You need to use a B2C tenant administrator account that is **local** to the B2C tenant.</span></span> <span data-ttu-id="cbcbd-155">Te konta wyglądać następująco: myusername@myb2ctenant.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="cbcbd-156">Teraz użyjemy **identyfikator aplikacji** w skrypcie poniżej, aby przypisać tę aplikację z rolą administratora konta użytkownika, która pozwoli na usuwanie użytkowników.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-156">Now we'll use the **Application ID** in the script below to assign the application the user account administrator role which will allow it to delete users.</span></span> <span data-ttu-id="cbcbd-157">Te role mają dobrze znane identyfikatory, więc wszystko co należy zrobić danych wejściowych użytkownika **identyfikator aplikacji** w poniższym skrypcie.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-157">These roles have well-known identifiers, so all you need to do is input your **Application ID** in the script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="cbcbd-158">Teraz aplikacja ma również uprawnienia do usuwania użytkowników z dzierżawy usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-158">Your application now also has permissions to delete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-the-sample-code"></a><span data-ttu-id="cbcbd-159">Pobrać, skonfigurować i utworzyć przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="cbcbd-159">Download, configure, and build the sample code</span></span>
<span data-ttu-id="cbcbd-160">Najpierw należy pobrać przykładowy kod i będzie działać.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-160">First, download the sample code and get it running.</span></span> <span data-ttu-id="cbcbd-161">Następnie firma Microsoft podejmie bliższe spojrzenie na go.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="cbcbd-162">Możesz [pobrać przykładowy kod w pliku .zip](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="cbcbd-162">You can [download the sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="cbcbd-163">Można również sklonować go w wybranym katalogu:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="cbcbd-164">Otwórz `B2CGraphClient\B2CGraphClient.sln` rozwiązania Visual Studio w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-164">Open the `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="cbcbd-165">W `B2CGraphClient` projekt, otwórz plik `App.config`.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-165">In the `B2CGraphClient` project, open the file `App.config`.</span></span> <span data-ttu-id="cbcbd-166">Zastąp ustawienia aplikacji trzy własne wartości:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-166">Replace the three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{The ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{The Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="cbcbd-167">Następnie kliknij prawym przyciskiem myszy `B2CGraphClient` rozwiązania i skompiluj ponownie próbki.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-167">Next, right-click on the `B2CGraphClient` solution and rebuild the sample.</span></span> <span data-ttu-id="cbcbd-168">W przypadku pomyślnego, po wykonaniu `B2C.exe` plik wykonywalny znajduje się w `B2CGraphClient\bin\Debug`.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-the-graph-api"></a><span data-ttu-id="cbcbd-169">Tworzenie operacji CRUD użytkownika przy użyciu interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="cbcbd-169">Build user CRUD operations by using the Graph API</span></span>
<span data-ttu-id="cbcbd-170">Aby użyć B2CGraphClient, otwórz `cmd` poleceń systemu Windows, w wierszu polecenia i zmień katalog na `Debug` katalogu.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-170">To use the B2CGraphClient, open a `cmd` Windows command prompt and change your directory to the `Debug` directory.</span></span> <span data-ttu-id="cbcbd-171">Następnie uruchom `B2C Help` polecenia.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-171">Then run the `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="cbcbd-172">Spowoduje to wyświetlenie krótki opis każdego polecenia.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-172">This will display a brief description of each command.</span></span> <span data-ttu-id="cbcbd-173">Zawsze jednego z tych poleceń, wywołaj `B2CGraphClient` zgłasza żądanie do interfejsu API programu Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request to the Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="cbcbd-174">Pobranie tokenu dostępu</span><span class="sxs-lookup"><span data-stu-id="cbcbd-174">Get an access token</span></span>
<span data-ttu-id="cbcbd-175">Wszystkie żądania interfejsu API programu Graph wymaga tokenu dostępu do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-175">Any request to the Graph API requires an access token for authentication.</span></span> <span data-ttu-id="cbcbd-176">`B2CGraphClient`korzysta open source Active Directory Authentication Library (ADAL), aby uzyskać tokeny dostępu.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-176">`B2CGraphClient` uses the open-source Active Directory Authentication Library (ADAL) to help acquire access tokens.</span></span> <span data-ttu-id="cbcbd-177">Biblioteka ADAL ułatwia tokenu nabycia, zapewniając prostych interfejsu API i Dbamy o pewne ważne informacje, takie jak buforowanie tokenów dostępu.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="cbcbd-178">Nie masz uzyskać tokenów, jednak przy użyciu biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-178">You don't have to use ADAL to get tokens, though.</span></span> <span data-ttu-id="cbcbd-179">Można również uzyskać tokeny przez obsługuje tworzenie żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="cbcbd-180">Ten przykład kodu wykorzystuje ADAL w wersji 2, aby komunikować się z interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-180">This code sample uses ADAL v2 in order to communicate with the Graph API.</span></span>  <span data-ttu-id="cbcbd-181">Aby uzyskać tokenów dostępu, które mogą być używane z interfejsem API usługi Azure AD Graph, należy użyć ADAL w wersji 2 lub 3.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-181">You must use ADAL v2 or v3 in order to get access tokens which can be used with the Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="cbcbd-182">Gdy `B2CGraphClient` uruchomieniu tworzy wystąpienie `B2CGraphClient` klasy.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-182">When `B2CGraphClient` runs, it creates an instance of the `B2CGraphClient` class.</span></span> <span data-ttu-id="cbcbd-183">Ustawia konstruktora dla tej klasy szkieletów uwierzytelniania ADAL:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-183">The constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // The client_id, client_secret, and tenant are provided in Program.cs, which pulls the values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // The AuthenticationContext is ADAL's primary class, in which you indicate the tenant to use.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // The ClientCredential is where you pass in your client_id and client_secret, which are
    // provided to Azure AD in order to receive an access_token by using the app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="cbcbd-184">Użyjemy `B2C Get-User` polecenie jako przykład.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-184">We'll use the `B2C Get-User` command as an example.</span></span> <span data-ttu-id="cbcbd-185">Gdy `B2C Get-User` jest wywoływana bez żadnych dodatkowych danych wejściowych, wywołania interfejsu wiersza polecenia `B2CGraphClient.GetAllUsers(...)` metody.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-185">When `B2C Get-User` is invoked without any additional inputs, the CLI calls the `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="cbcbd-186">Ta metoda wywołuje `B2CGraphClient.SendGraphGetRequest(...)`, który przesyła żądanie HTTP GET do interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request to the Graph API.</span></span> <span data-ttu-id="cbcbd-187">Przed `B2CGraphClient.SendGraphGetRequest(...)` wysyła żądanie GET, należy go najpierw pobiera token dostępu za pomocą biblioteki ADAL:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends the GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL to acquire a token by using the app's identity (the credential)
    // The first parameter is the resource we want an access_token for; in this case, the Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="cbcbd-188">Możesz też uzyskać dostęp do tokenu interfejsu API programu Graph przez wywołanie metody z biblioteki ADAL `AuthenticationContext.AcquireToken(...)` metody.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-188">You can get an access token for the Graph API by calling the ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="cbcbd-189">Zwraca ADAL `access_token` reprezentujący tożsamości aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-189">ADAL then returns an `access_token` that represents the application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="cbcbd-190">Przeczytaj użytkowników</span><span class="sxs-lookup"><span data-stu-id="cbcbd-190">Read users</span></span>
<span data-ttu-id="cbcbd-191">Jeśli chcesz uzyskać listę użytkowników lub pobrać danego użytkownika z interfejsu API programu Graph, możesz wysłać HTTP `GET` żądanie `/users` punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-191">When you want to get a list of users or get a particular user from the Graph API, you can send an HTTP `GET` request to the `/users` endpoint.</span></span> <span data-ttu-id="cbcbd-192">Żądanie dla wszystkich użytkowników w dzierżawie wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-192">A request for all of the users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="cbcbd-193">Aby wyświetlić to żądanie, uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-193">To see this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="cbcbd-194">Istnieją dwa ważnych rzeczy do uwzględnienia:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-194">There are two important things to note:</span></span>

* <span data-ttu-id="cbcbd-195">Token dostępu nabyte za pomocą biblioteki ADAL zostanie dodany do `Authorization` nagłówka przy użyciu `Bearer` schematu.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-195">The access token acquired via ADAL is added to the `Authorization` header by using the `Bearer` scheme.</span></span>
* <span data-ttu-id="cbcbd-196">Dla dzierżawcy usługi B2C, należy użyć parametru zapytania `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-196">For B2C tenants, you must use the query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="cbcbd-197">Oba te informacje są obsługiwane w `B2CGraphClient.SendGraphGetRequest(...)` metody:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-197">Both of these details are handled in the `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure to use the 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append the access token for the Graph API to the Authorization header of the request by using the Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="cbcbd-198">Tworzenie konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="cbcbd-198">Create consumer user accounts</span></span>
<span data-ttu-id="cbcbd-199">Podczas tworzenia kont użytkowników w dzierżawie usługi B2C, możesz wysłać HTTP `POST` żądanie `/users` punktu końcowego:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request to the `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required to create consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier the user uses to sign in to the account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set to 'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying to the end user
    "mailNickname": "joec",                        // an email alias for the user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set to false
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="cbcbd-200">Większość tych właściwości w tym żądaniu są wymagane do utworzenia konsumentów.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-200">Most of these properties in this request are required to create consumer users.</span></span> <span data-ttu-id="cbcbd-201">Aby dowiedzieć się więcej, kliknij przycisk [tutaj](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span><span class="sxs-lookup"><span data-stu-id="cbcbd-201">To learn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="cbcbd-202">Należy pamiętać, że `//` komentarze zostały włączone na ilustracji.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-202">Note that the `//` comments have been included for illustration.</span></span> <span data-ttu-id="cbcbd-203">Nie należy wprowadzać ich w rzeczywistego żądania.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="cbcbd-204">Aby wyświetlić żądanie, uruchom jedno z następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-204">To see the request, run one of the following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="cbcbd-205">`Create-User` Polecenie przyjmuje jako parametr wejściowy plik JSON.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-205">The `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="cbcbd-206">Zawiera reprezentacja JSON obiektu user.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="cbcbd-207">Istnieją dwa przykładowe pliki JSON w przykładowym kodzie: `usertemplate-email.json` i `usertemplate-username.json`.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-207">There are two sample .json files in the sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="cbcbd-208">Można zmodyfikować te pliki, w zależności od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-208">You can modify these files to suit your needs.</span></span> <span data-ttu-id="cbcbd-209">Oprócz wymaganych pól powyżej kilka opcjonalne pola, które można użyć znajdują się w tych plikach.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-209">In addition to the required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="cbcbd-210">Szczegółowe informacje o opcjonalne pola znajdują się w [odwołania do jednostki interfejsu API usługi Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span><span class="sxs-lookup"><span data-stu-id="cbcbd-210">Details on the optional fields can be found in the [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="cbcbd-211">Widać, jak żądania POST jest tworzony w `B2CGraphClient.SendGraphPostRequest(...)`.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-211">You can see how the POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="cbcbd-212">Dołącza token dostępu do `Authorization` nagłówka żądania.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-212">It attaches an access token to the `Authorization` header of the request.</span></span>
* <span data-ttu-id="cbcbd-213">Ustawia `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="cbcbd-214">Obejmuje on obiektu użytkownika w formacie JSON w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-214">It includes the JSON user object in the body of the request.</span></span>

> [!NOTE]
> <span data-ttu-id="cbcbd-215">Jeśli konta, które chcesz przeprowadzić migrację z istniejącym magazynem użytkownika ma niższe siły hasła niż [siły silne hasło, wymuszane przez usługę Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), można wyłączyć przy użyciu wymaganie silne hasło `DisableStrongPassword` wartość w `passwordPolicies` właściwości.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-215">If the accounts that you want to migrate from an existing user store has lower password strength than the [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable the strong password requirement using the `DisableStrongPassword` value in the `passwordPolicies` property.</span></span> <span data-ttu-id="cbcbd-216">Na przykład można zmodyfikować żądanie użytkownika utworzenia podanego powyżej w następujący sposób: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-216">For instance, you can modify the create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="cbcbd-217">Aktualizowanie kont użytkownika klienta</span><span class="sxs-lookup"><span data-stu-id="cbcbd-217">Update consumer user accounts</span></span>
<span data-ttu-id="cbcbd-218">Podczas aktualizowania obiektów użytkowników, proces jest podobny do tego, który służy do tworzenia obiektów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-218">When you update user objects, the process is similar to the one you use to create user objects.</span></span> <span data-ttu-id="cbcbd-219">Ten proces korzysta z protokołu HTTP, ale `PATCH` metody:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-219">But this process uses the HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only the user's displayName
}
```

<span data-ttu-id="cbcbd-220">Spróbuj zaktualizować użytkownika aktualizując nowych danych plików JSON.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-220">Try to update a user by updating your JSON files with new data.</span></span> <span data-ttu-id="cbcbd-221">Następnie można użyć `B2CGraphClient` na jeden z tych poleceń:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-221">You can then use `B2CGraphClient` to run one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="cbcbd-222">Sprawdź `B2CGraphClient.SendGraphPatchRequest(...)` metody, aby uzyskać szczegółowe informacje dotyczące sposobu wysyłania tego żądania.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-222">Inspect the `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how to send this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="cbcbd-223">Wyszukiwania użytkowników</span><span class="sxs-lookup"><span data-stu-id="cbcbd-223">Search users</span></span>
<span data-ttu-id="cbcbd-224">Możesz wyszukać użytkowników w dzierżawie usługi B2C na kilka sposobów.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="cbcbd-225">Obiekt go przy użyciu użytkownika Identyfikatora lub dwóch przy użyciu identyfikatora logowania użytkownika (tj. `signInNames` właściwości).</span><span class="sxs-lookup"><span data-stu-id="cbcbd-225">One, using the user's object ID or two, using the user's sign-in identifer (i.e., the `signInNames` property).</span></span>

<span data-ttu-id="cbcbd-226">Uruchom jedno z poniższych poleceń, aby wyszukać określonego użytkownika:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-226">Run one of the following commands to search for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="cbcbd-227">Oto kilka przykładów:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="cbcbd-228">Usuwanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="cbcbd-228">Delete users</span></span>
<span data-ttu-id="cbcbd-229">Proces związanych z usuwaniem użytkowników jest prosta.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-229">The process for deleting a user is straightforward.</span></span> <span data-ttu-id="cbcbd-230">Korzystanie z protokołu HTTP `DELETE` — metoda i konstrukcja do adresu URL poprawny identyfikator obiektu:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-230">Use the HTTP `DELETE` method and construct the URL with the correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="cbcbd-231">Na przykład, wprowadź następujące polecenie i wyświetlić żądanie usunięcia, używanego do konsoli:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-231">To see an example, enter this command and view the delete request that is printed to the console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="cbcbd-232">Sprawdź `B2CGraphClient.SendGraphDeleteRequest(...)` metody, aby uzyskać szczegółowe informacje dotyczące sposobu wysyłania tego żądania.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-232">Inspect the `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how to send this request.</span></span>

<span data-ttu-id="cbcbd-233">Można wykonywać wiele akcji przy użyciu interfejsu API Azure AD Graph oprócz Zarządzanie użytkownikami.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-233">You can perform many other actions with the Azure AD Graph API in addition to user management.</span></span> <span data-ttu-id="cbcbd-234">[Dokumentacja interfejsu API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) podano szczegółowe informacje dotyczące każdej akcji, wraz z próbki żądań.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="cbcbd-235">Używanie atrybutów niestandardowych</span><span class="sxs-lookup"><span data-stu-id="cbcbd-235">Use custom attributes</span></span>
<span data-ttu-id="cbcbd-236">Większość aplikacji klienta należy przechowywać pewien typ informacji o profilu użytkownika niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-236">Most consumer applications need to store some type of custom user profile information.</span></span> <span data-ttu-id="cbcbd-237">Można to zrobić jednym ze sposobów jest zdefiniuj atrybut niestandardowy w dzierżawie usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-237">One way you can do this is to define a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="cbcbd-238">Ten atrybut można następnie traktować ten sam sposób traktować innych właściwości dla obiektu user.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-238">You can then treat that attribute the same way you treat any other property on a user object.</span></span> <span data-ttu-id="cbcbd-239">Można zaktualizować atrybutu, usuń atrybut, zapytania za pomocą atrybutu, wysyłanie atrybut jako oświadczenia w tokeny logowania i inne.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-239">You can update the attribute, delete the attribute, query by the attribute, send the attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="cbcbd-240">Aby zdefiniować atrybutu niestandardowego w dzierżawie usługi B2C, zobacz [odwołanie do atrybutu niestandardowego B2C](active-directory-b2c-reference-custom-attr.md).</span><span class="sxs-lookup"><span data-stu-id="cbcbd-240">To define a custom attribute in your B2C tenant, see the [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="cbcbd-241">Możesz wyświetlić atrybuty niestandardowe zdefiniowane w dzierżawie usługi B2C przy użyciu `B2CGraphClient`:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-241">You can view the custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="cbcbd-242">Dane wyjściowe z tych funkcji ujawnia szczegóły każdego z atrybutów niestandardowych, takich jak:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-242">The output of these functions reveals the details of each custom attribute, such as:</span></span>

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

<span data-ttu-id="cbcbd-243">Można użyć pełnej nazwy, takie jak `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, jako właściwość obiektów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-243">You can use the full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="cbcbd-244">Zaktualizuj plik JSON o nowej właściwości i wartości dla właściwości, a następnie uruchom:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-244">Update your .json file with the new property and a value for the property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="cbcbd-245">Za pomocą `B2CGraphClient`, masz aplikacji usługi, który można programowo zarządzać użytkownicy dzierżawy B2C.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="cbcbd-246">`B2CGraphClient`używa jego tożsamość aplikacji do uwierzytelniania interfejsu API programu Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-246">`B2CGraphClient` uses its own application identity to authenticate to the Azure AD Graph API.</span></span> <span data-ttu-id="cbcbd-247">Uzyskuje on również tokenów przy użyciu klucza tajnego klienta.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="cbcbd-248">Ponieważ ta funkcja jest dołączyć do aplikacji, należy pamiętać o kilka najważniejszych dla aplikacji B2C:</span><span class="sxs-lookup"><span data-stu-id="cbcbd-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="cbcbd-249">Należy przyznać odpowiednie uprawnienia w dzierżawie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-249">You need to grant the application the proper permissions in the tenant.</span></span>
* <span data-ttu-id="cbcbd-250">Na razie należy użyć biblioteki ADAL (nie MSAL) można uzyskać tokeny dostępu.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-250">For now, you need to use ADAL (not MSAL) to get access tokens.</span></span> <span data-ttu-id="cbcbd-251">(Możesz również wysłać wiadomości protokołu bezpośrednio, bez korzystania z biblioteki.)</span><span class="sxs-lookup"><span data-stu-id="cbcbd-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="cbcbd-252">Po wywołaniu interfejsu API programu Graph, użyj `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-252">When you call the Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="cbcbd-253">Podczas tworzenia i aktualizowania użytkowników konsumenta, kilka właściwości są wymagane, zgodnie z powyższym opisem.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="cbcbd-254">Jeśli masz pytania lub żądań dla akcji się, że chcesz przeprowadzić przy użyciu interfejsu API programu Graph na dzierżawę B2C, zostaw komentarz w tym artykule, lub plików problemu w repozytorium GitHub przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="cbcbd-254">If you have any questions or requests for actions you would like to perform by using the Graph API on your B2C tenant, leave a comment on this article or file an issue in the GitHub code sample repository.</span></span>

