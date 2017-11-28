---
title: "Usługa Azure Active Directory B2C: Hello Użyj interfejsu API programu Graph | Dokumentacja firmy Microsoft"
description: "Jak toocall hello interfejsu API programu Graph dla dzierżawy B2C przy użyciu procesu hello tooautomate tożsamości aplikacji."
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
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a><span data-ttu-id="674e1-103">Usługa Azure AD B2C: Użyj hello interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="674e1-103">Azure AD B2C: Use hello Graph API</span></span>
<span data-ttu-id="674e1-104">Dzierżaw usługi Azure Active Directory (Azure AD) B2C zwykle toobe bardzo duże.</span><span class="sxs-lookup"><span data-stu-id="674e1-104">Azure Active Directory (Azure AD) B2C tenants tend toobe very large.</span></span> <span data-ttu-id="674e1-105">Oznacza to, że wiele typowych zadań zarządzania dzierżawy musi wykonać programowo toobe.</span><span class="sxs-lookup"><span data-stu-id="674e1-105">This means that many common tenant management tasks need toobe performed programmatically.</span></span> <span data-ttu-id="674e1-106">Podstawowy przykład to zarządzanie użytkownikami.</span><span class="sxs-lookup"><span data-stu-id="674e1-106">A primary example is user management.</span></span> <span data-ttu-id="674e1-107">Może być konieczne toomigrate istniejącej dzierżawy B2C tooa magazynu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="674e1-107">You might need toomigrate an existing user store tooa B2C tenant.</span></span> <span data-ttu-id="674e1-108">Może mają toohost rejestracja użytkownika na stronie i tworzenia kont użytkowników w katalogu usługi Azure AD B2C w tle hello.</span><span class="sxs-lookup"><span data-stu-id="674e1-108">You may want toohost user registration on your own page and create user accounts in your Azure AD B2C directory behind hello scenes.</span></span> <span data-ttu-id="674e1-109">Tego rodzaju zadania wymagają toocreate możliwości hello, odczytu, aktualizacji i usuwać konta użytkowników.</span><span class="sxs-lookup"><span data-stu-id="674e1-109">These types of tasks require hello ability toocreate, read, update, and delete user accounts.</span></span> <span data-ttu-id="674e1-110">Można wykonywać te zadania przy użyciu interfejsu API Azure AD Graph hello.</span><span class="sxs-lookup"><span data-stu-id="674e1-110">You can do these tasks by using hello Azure AD Graph API.</span></span>

<span data-ttu-id="674e1-111">Dla dzierżawcy usługi B2C istnieją dwa tryby głównej komunikowania się z hello interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="674e1-111">For B2C tenants, there are two primary modes of communicating with hello Graph API.</span></span>

* <span data-ttu-id="674e1-112">Interaktywny, jednokrotnego uruchamiania zadań powinny działać jako konto administratora w dzierżawy B2C hello zadań hello.</span><span class="sxs-lookup"><span data-stu-id="674e1-112">For interactive, run-once tasks, you should act as an administrator account in hello B2C tenant when you perform hello tasks.</span></span> <span data-ttu-id="674e1-113">Ten tryb wymaga toosign administratora przy użyciu poświadczeń tego administratora mogą wykonywać wszystkie toohello wywołania interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="674e1-113">This mode requires an administrator toosign in with credentials before that admin can perform any calls toohello Graph API.</span></span>
* <span data-ttu-id="674e1-114">Zautomatyzowane, ciągłe zadania należy używać pewien typ konta usługi, który podasz z zadaniami zarządzania tooperform niezbędne uprawnienia hello.</span><span class="sxs-lookup"><span data-stu-id="674e1-114">For automated, continuous tasks, you should use some type of service account that you provide with hello necessary privileges tooperform management tasks.</span></span> <span data-ttu-id="674e1-115">W usłudze Azure AD możesz to zrobić, rejestrowanie aplikacji i uwierzytelnianie tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="674e1-115">In Azure AD, you can do this by registering an application and authenticating tooAzure AD.</span></span> <span data-ttu-id="674e1-116">Jest to zrobić za pomocą **identyfikator aplikacji** używającą hello [przyznania poświadczeń klienta OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="674e1-116">This is done by using an **Application ID** that uses hello [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="674e1-117">W takim przypadku aplikacji hello działa jako sam nie jako użytkownik, hello toocall interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="674e1-117">In this case, hello application acts as itself, not as a user, toocall hello Graph API.</span></span>

<span data-ttu-id="674e1-118">W tym artykule omówiono sposób tooperform hello przypadku użycia automatycznego.</span><span class="sxs-lookup"><span data-stu-id="674e1-118">In this article, we'll discuss how tooperform hello automated-use case.</span></span> <span data-ttu-id="674e1-119">toodemonstrate, firma Microsoft będzie kompilacji platformy .NET 4.5 `B2CGraphClient` wykonująca użytkownika tworzenia, odczytu, aktualizacji i usuwania (CRUD) operacji.</span><span class="sxs-lookup"><span data-stu-id="674e1-119">toodemonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="674e1-120">powitania klienta będzie mieć interfejsu wiersza polecenia systemu Windows (CLI), która pozwala tooinvoke różnych metod.</span><span class="sxs-lookup"><span data-stu-id="674e1-120">hello client will have a Windows command-line interface (CLI) that allows you tooinvoke various methods.</span></span> <span data-ttu-id="674e1-121">Jednak kod hello są zapisywane toobehave w sposób nieinteraktywne, automatycznej.</span><span class="sxs-lookup"><span data-stu-id="674e1-121">However, hello code is written toobehave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="674e1-122">Uzyskiwanie dzierżawy usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="674e1-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="674e1-123">Przed tworzenia aplikacji lub użytkowników lub w ogóle interakcję z usługą Azure AD, konieczne będzie dzierżawy usługi Azure AD B2C i konto administratora globalnego w dzierżawie powitalnych.</span><span class="sxs-lookup"><span data-stu-id="674e1-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in hello tenant.</span></span> <span data-ttu-id="674e1-124">Jeśli nie masz już, dzierżawcy [wprowadzenie do usługi Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="674e1-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="674e1-125">Zarejestrować aplikację w dzierżawie</span><span class="sxs-lookup"><span data-stu-id="674e1-125">Register your application in your tenant</span></span>
<span data-ttu-id="674e1-126">Po utworzeniu dzierżawy B2C należy tooregister aplikację za pośrednictwem hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="674e1-126">After you have a B2C tenant, you need tooregister your application via hello [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="674e1-127">toouse hello interfejsu API programu Graph z dzierżawy usługi B2C, trzeba będzie tooregister dedykowanej aplikacji przy użyciu zwykłego hello *rejestracji aplikacji* bloku w hello portalu Azure, **nie** usługi Azure AD B2C  *Aplikacje* bloku.</span><span class="sxs-lookup"><span data-stu-id="674e1-127">toouse hello Graph API with your B2C tenant, you will need tooregister a dedicated application by using hello generic *App Registrations* blade in hello Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="674e1-128">Nie można użyć ponownie hello już istniejących B2C aplikacji, które zarejestrowano w hello Azure AD B2C *aplikacji* bloku.</span><span class="sxs-lookup"><span data-stu-id="674e1-128">You can't reuse hello already-existing B2C applications that you registered in hello Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="674e1-129">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="674e1-129">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="674e1-130">Wybierz dzierżawy usługi Azure AD B2C, wybierając konto w hello prawym górnym rogu strony hello.</span><span class="sxs-lookup"><span data-stu-id="674e1-130">Choose your Azure AD B2C tenant by selecting your account in hello top right corner of hello page.</span></span>
3. <span data-ttu-id="674e1-131">W okienku nawigacji po lewej stronie powitania, wybierz **więcej usług**, kliknij przycisk **rejestracji aplikacji**i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="674e1-131">In hello left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="674e1-132">Postępuj zgodnie z monitami hello i utworzyć nową aplikację.</span><span class="sxs-lookup"><span data-stu-id="674e1-132">Follow hello prompts and create a new application.</span></span> 
    1. <span data-ttu-id="674e1-133">Wybierz **aplikacji sieci Web / interfejs API** jako hello typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="674e1-133">Select **Web App / API** as hello Application Type.</span></span>    
    2. <span data-ttu-id="674e1-134">Podaj **żadnego identyfikator URI przekierowania** (np. https://B2CGraphAPI), ponieważ nie jest to potrzebne w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="674e1-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="674e1-135">Witaj aplikacji będą teraz wyświetlane w hello listę aplikacji, kliknij go tooobtain hello **identyfikator aplikacji** (znanej także jako identyfikator klienta).</span><span class="sxs-lookup"><span data-stu-id="674e1-135">hello application will now show up in hello list of applications, click on it tooobtain hello **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="674e1-136">Skopiuj go, ponieważ będzie on potrzebny w dalszej części artykułu.</span><span class="sxs-lookup"><span data-stu-id="674e1-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="674e1-137">W bloku ustawień powitania kliknij **klucze** i Dodaj nowy klucz (znanej także jako klucz tajny klienta).</span><span class="sxs-lookup"><span data-stu-id="674e1-137">In hello Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="674e1-138">Jest on również kopiowany do użycia w dalszej części artykułu.</span><span class="sxs-lookup"><span data-stu-id="674e1-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="674e1-139">Skonfiguruj tworzenie, odczytywanie i aktualizowanie uprawnień dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="674e1-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="674e1-140">Teraz należy tooconfigure tooget Twojej aplikacji, które hello wszystkie wymagane uprawnienia toocreate, odczytu, aktualizacji i usuwania użytkowników.</span><span class="sxs-lookup"><span data-stu-id="674e1-140">Now you need tooconfigure your application tooget all hello required permissions toocreate, read, update and delete users.</span></span>

1. <span data-ttu-id="674e1-141">Kontynuowanie w hello bloku rejestracji aplikacji w portalu Azure, wybierz aplikację.</span><span class="sxs-lookup"><span data-stu-id="674e1-141">Continuing in hello Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="674e1-142">W bloku ustawień powitania kliknij **wymagane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="674e1-142">In hello Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="674e1-143">W bloku wymaganych uprawnień powitania kliknij **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="674e1-143">In hello Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="674e1-144">W bloku Włącz dostęp hello, wybierz hello **Odczyt i zapis danych katalogu** zgody **uprawnienia aplikacji** i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="674e1-144">In hello Enable Access  blade, select hello **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="674e1-145">Ponadto w hello bloku wymaganych uprawnień, kliknij na powitania **udzielanie uprawnień** przycisku.</span><span class="sxs-lookup"><span data-stu-id="674e1-145">Finally, back in hello Required permissions blade, click on hello **Grant Permissions** button.</span></span>

<span data-ttu-id="674e1-146">Masz teraz aplikacja, która ma uprawnienia toocreate, Odczyt i aktualizacja użytkowników z dzierżawy usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="674e1-146">You now have an application that has permission toocreate, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="674e1-147">Skonfiguruj uprawnienia do usuwania aplikacji</span><span class="sxs-lookup"><span data-stu-id="674e1-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="674e1-148">Obecnie hello *Odczyt i zapis danych katalogu* uprawnienie jest **nie** obejmują toodo możliwości hello żadnych usunięć, takich jak usuwanie użytkowników.</span><span class="sxs-lookup"><span data-stu-id="674e1-148">Currently, hello *Read and write directory data* permission does **NOT** include hello ability toodo any deletions such as deleting users.</span></span> <span data-ttu-id="674e1-149">Jeśli chcesz toogive aplikacji hello możliwości toodelete użytkowników, będziesz potrzebować toodo te dodatkowe kroki, które wymagają programu PowerShell, w przeciwnym razie można pominąć toohello następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="674e1-149">If you want toogive your application hello ability toodelete users, you'll need toodo these extra steps that involve PowerShell, otherwise, you can skip toohello next section.</span></span>

<span data-ttu-id="674e1-150">Najpierw należy pobrać i zainstalować hello [Microsoft Online Services Asystenta logowania](http://go.microsoft.com/fwlink/?LinkID=286152).</span><span class="sxs-lookup"><span data-stu-id="674e1-150">First, download and install hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="674e1-151">Następnie Pobierz i zainstaluj hello [64-bitowy moduł usługi Azure Active Directory dla środowiska Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="674e1-151">Then download and install hello [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="674e1-152">Po zainstalowaniu modułu PowerShell hello, Otwórz program PowerShell i połączyć tooyour dzierżawy B2C.</span><span class="sxs-lookup"><span data-stu-id="674e1-152">After you install hello PowerShell module, open PowerShell and connect tooyour B2C tenant.</span></span> <span data-ttu-id="674e1-153">Po uruchomieniu `Get-Credential`, zostanie wyświetlony monit dla nazwy użytkownika i hasła, wprowadź nazwę użytkownika hello i hasło konta administratora dzierżawy B2C.</span><span class="sxs-lookup"><span data-stu-id="674e1-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter hello user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="674e1-154">Należy toouse B2C konta administratora dzierżawy, który jest **lokalnego** toohello B2C dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="674e1-154">You need toouse a B2C tenant administrator account that is **local** toohello B2C tenant.</span></span> <span data-ttu-id="674e1-155">Te konta wyglądać następująco: myusername@myb2ctenant.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="674e1-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="674e1-156">Teraz użyjemy hello **identyfikator aplikacji** w skrypcie hello poniżej tooassign hello aplikacji hello konta administrator roli użytkownika, który umożliwi użytkownikom toodelete.</span><span class="sxs-lookup"><span data-stu-id="674e1-156">Now we'll use hello **Application ID** in hello script below tooassign hello application hello user account administrator role which will allow it toodelete users.</span></span> <span data-ttu-id="674e1-157">Te role mają dobrze znane identyfikatory, więc wszystko, czego potrzebujesz toodo danych wejściowych użytkownika **identyfikator aplikacji** w poniższym skrypcie hello.</span><span class="sxs-lookup"><span data-stu-id="674e1-157">These roles have well-known identifiers, so all you need toodo is input your **Application ID** in hello script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="674e1-158">Teraz aplikacja ma również uprawnienia toodelete użytkowników z dzierżawy usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="674e1-158">Your application now also has permissions toodelete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-hello-sample-code"></a><span data-ttu-id="674e1-159">Pobierz, konfigurowanie i tworzenie hello przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="674e1-159">Download, configure, and build hello sample code</span></span>
<span data-ttu-id="674e1-160">Najpierw należy pobrać hello przykładowy kod i będzie działać.</span><span class="sxs-lookup"><span data-stu-id="674e1-160">First, download hello sample code and get it running.</span></span> <span data-ttu-id="674e1-161">Następnie firma Microsoft podejmie bliższe spojrzenie na go.</span><span class="sxs-lookup"><span data-stu-id="674e1-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="674e1-162">Możesz [Pobierz hello przykładowy kod w pliku .zip](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="674e1-162">You can [download hello sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="674e1-163">Można również sklonować go w wybranym katalogu:</span><span class="sxs-lookup"><span data-stu-id="674e1-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="674e1-164">Otwórz hello `B2CGraphClient\B2CGraphClient.sln` rozwiązania Visual Studio w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="674e1-164">Open hello `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="674e1-165">W hello `B2CGraphClient` projektu, hello Otwórz plik `App.config`.</span><span class="sxs-lookup"><span data-stu-id="674e1-165">In hello `B2CGraphClient` project, open hello file `App.config`.</span></span> <span data-ttu-id="674e1-166">Zastąp trzy ustawienia aplikacji hello własne wartości:</span><span class="sxs-lookup"><span data-stu-id="674e1-166">Replace hello three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="674e1-167">Następnie kliknij prawym przyciskiem myszy hello `B2CGraphClient` próbki hello rozwiązania i skompiluj ponownie.</span><span class="sxs-lookup"><span data-stu-id="674e1-167">Next, right-click on hello `B2CGraphClient` solution and rebuild hello sample.</span></span> <span data-ttu-id="674e1-168">W przypadku pomyślnego, po wykonaniu `B2C.exe` plik wykonywalny znajduje się w `B2CGraphClient\bin\Debug`.</span><span class="sxs-lookup"><span data-stu-id="674e1-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a><span data-ttu-id="674e1-169">Tworzenie operacji CRUD użytkownika przy użyciu interfejsu API programu Graph hello</span><span class="sxs-lookup"><span data-stu-id="674e1-169">Build user CRUD operations by using hello Graph API</span></span>
<span data-ttu-id="674e1-170">Otwórz hello toouse B2CGraphClient, `cmd` poleceń systemu Windows, w wierszu polecenia i zmień toohello Twojego katalogu `Debug` katalogu.</span><span class="sxs-lookup"><span data-stu-id="674e1-170">toouse hello B2CGraphClient, open a `cmd` Windows command prompt and change your directory toohello `Debug` directory.</span></span> <span data-ttu-id="674e1-171">Następnie uruchom hello `B2C Help` polecenia.</span><span class="sxs-lookup"><span data-stu-id="674e1-171">Then run hello `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="674e1-172">Spowoduje to wyświetlenie krótki opis każdego polecenia.</span><span class="sxs-lookup"><span data-stu-id="674e1-172">This will display a brief description of each command.</span></span> <span data-ttu-id="674e1-173">Zawsze jednego z tych poleceń, wywołaj `B2CGraphClient` sprawia, że toohello żądania interfejsu API usługi Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="674e1-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request toohello Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="674e1-174">Pobranie tokenu dostępu</span><span class="sxs-lookup"><span data-stu-id="674e1-174">Get an access token</span></span>
<span data-ttu-id="674e1-175">Wszelkie toohello żądania interfejsu API programu Graph wymaga tokenu dostępu do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="674e1-175">Any request toohello Graph API requires an access token for authentication.</span></span> <span data-ttu-id="674e1-176">`B2CGraphClient`używa hello open source Active Directory Authentication Library (ADAL) toohelp uzyskać tokeny dostępu.</span><span class="sxs-lookup"><span data-stu-id="674e1-176">`B2CGraphClient` uses hello open-source Active Directory Authentication Library (ADAL) toohelp acquire access tokens.</span></span> <span data-ttu-id="674e1-177">Biblioteka ADAL ułatwia tokenu nabycia, zapewniając prostych interfejsu API i Dbamy o pewne ważne informacje, takie jak buforowanie tokenów dostępu.</span><span class="sxs-lookup"><span data-stu-id="674e1-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="674e1-178">Nie masz toouse ADAL tooget tokenów, jednak.</span><span class="sxs-lookup"><span data-stu-id="674e1-178">You don't have toouse ADAL tooget tokens, though.</span></span> <span data-ttu-id="674e1-179">Można również uzyskać tokeny przez obsługuje tworzenie żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="674e1-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="674e1-180">Ten przykładowy kod używa biblioteki ADAL v2 w kolejności toocommunicate z hello interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="674e1-180">This code sample uses ADAL v2 in order toocommunicate with hello Graph API.</span></span>  <span data-ttu-id="674e1-181">Należy użyć ADAL w wersji 2 lub 3 w kolejności tokenów dostępu tooget, które mogą być używane z hello interfejsu API usługi Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="674e1-181">You must use ADAL v2 or v3 in order tooget access tokens which can be used with hello Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="674e1-182">Gdy `B2CGraphClient` uruchomieniu tworzy wystąpienie hello `B2CGraphClient` klasy.</span><span class="sxs-lookup"><span data-stu-id="674e1-182">When `B2CGraphClient` runs, it creates an instance of hello `B2CGraphClient` class.</span></span> <span data-ttu-id="674e1-183">Witaj konstruktorze tej klasy konfiguruje szkieletów uwierzytelniania ADAL:</span><span class="sxs-lookup"><span data-stu-id="674e1-183">hello constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="674e1-184">Użyjemy hello `B2C Get-User` polecenie jako przykład.</span><span class="sxs-lookup"><span data-stu-id="674e1-184">We'll use hello `B2C Get-User` command as an example.</span></span> <span data-ttu-id="674e1-185">Gdy `B2C Get-User` jest wywoływana bez żadnych dodatkowych danych wejściowych hello hello wywołania interfejsu wiersza polecenia `B2CGraphClient.GetAllUsers(...)` metody.</span><span class="sxs-lookup"><span data-stu-id="674e1-185">When `B2C Get-User` is invoked without any additional inputs, hello CLI calls hello `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="674e1-186">Ta metoda wywołuje `B2CGraphClient.SendGraphGetRequest(...)`, który przesyła toohello żądania HTTP GET interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="674e1-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request toohello Graph API.</span></span> <span data-ttu-id="674e1-187">Przed `B2CGraphClient.SendGraphGetRequest(...)` wysyła hello żądania GET, należy go najpierw pobiera token dostępu za pomocą biblioteki ADAL:</span><span class="sxs-lookup"><span data-stu-id="674e1-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends hello GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="674e1-188">Możesz też uzyskać dostęp do tokenu hello interfejsu API programu Graph przez wywołanie hello ADAL `AuthenticationContext.AcquireToken(...)` metody.</span><span class="sxs-lookup"><span data-stu-id="674e1-188">You can get an access token for hello Graph API by calling hello ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="674e1-189">Zwraca ADAL `access_token` reprezentujący tożsamość aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="674e1-189">ADAL then returns an `access_token` that represents hello application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="674e1-190">Przeczytaj użytkowników</span><span class="sxs-lookup"><span data-stu-id="674e1-190">Read users</span></span>
<span data-ttu-id="674e1-191">Gdy ma tooget listę użytkowników lub uzyskać danego użytkownika z interfejsu API programu Graph hello, możesz wysłać HTTP `GET` żądania toohello `/users` punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="674e1-191">When you want tooget a list of users or get a particular user from hello Graph API, you can send an HTTP `GET` request toohello `/users` endpoint.</span></span> <span data-ttu-id="674e1-192">Żądanie dla wszystkich użytkowników hello w dzierżawie wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="674e1-192">A request for all of hello users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="674e1-193">toosee to żądanie, uruchom:</span><span class="sxs-lookup"><span data-stu-id="674e1-193">toosee this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="674e1-194">Istnieją dwa toonote ważnych rzeczy:</span><span class="sxs-lookup"><span data-stu-id="674e1-194">There are two important things toonote:</span></span>

* <span data-ttu-id="674e1-195">Witaj tokenu dostępu nabyte za pomocą biblioteki ADAL zostanie dodany toohello `Authorization` nagłówka przy użyciu hello `Bearer` schematu.</span><span class="sxs-lookup"><span data-stu-id="674e1-195">hello access token acquired via ADAL is added toohello `Authorization` header by using hello `Bearer` scheme.</span></span>
* <span data-ttu-id="674e1-196">Dla dzierżawcy usługi B2C, należy użyć parametru zapytania hello `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="674e1-196">For B2C tenants, you must use hello query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="674e1-197">Oba te informacje są obsługiwane w hello `B2CGraphClient.SendGraphGetRequest(...)` metody:</span><span class="sxs-lookup"><span data-stu-id="674e1-197">Both of these details are handled in hello `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="674e1-198">Tworzenie konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="674e1-198">Create consumer user accounts</span></span>
<span data-ttu-id="674e1-199">Podczas tworzenia kont użytkowników w dzierżawie usługi B2C, możesz wysłać HTTP `POST` żądania toohello `/users` punktu końcowego:</span><span class="sxs-lookup"><span data-stu-id="674e1-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request toohello `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="674e1-200">Większość tych właściwości w tym żądaniu są wymagane toocreate konsumentów.</span><span class="sxs-lookup"><span data-stu-id="674e1-200">Most of these properties in this request are required toocreate consumer users.</span></span> <span data-ttu-id="674e1-201">więcej, kliknij przycisk toolearn [tutaj](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span><span class="sxs-lookup"><span data-stu-id="674e1-201">toolearn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="674e1-202">Należy pamiętać, że hello `//` komentarze zostały włączone na ilustracji.</span><span class="sxs-lookup"><span data-stu-id="674e1-202">Note that hello `//` comments have been included for illustration.</span></span> <span data-ttu-id="674e1-203">Nie należy wprowadzać ich w rzeczywistego żądania.</span><span class="sxs-lookup"><span data-stu-id="674e1-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="674e1-204">Żądanie hello toosee, uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="674e1-204">toosee hello request, run one of hello following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="674e1-205">Witaj `Create-User` polecenie przyjmuje jako parametr wejściowy plik JSON.</span><span class="sxs-lookup"><span data-stu-id="674e1-205">hello `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="674e1-206">Zawiera reprezentacja JSON obiektu user.</span><span class="sxs-lookup"><span data-stu-id="674e1-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="674e1-207">Istnieją dwa przykładowe pliki JSON w hello przykładowy kod: `usertemplate-email.json` i `usertemplate-username.json`.</span><span class="sxs-lookup"><span data-stu-id="674e1-207">There are two sample .json files in hello sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="674e1-208">Można zmodyfikować te pliki toosuit potrzeb.</span><span class="sxs-lookup"><span data-stu-id="674e1-208">You can modify these files toosuit your needs.</span></span> <span data-ttu-id="674e1-209">Ponadto toohello wymagane pola powyżej, kilka opcjonalne pola, które można użyć znajdują się w tych plikach.</span><span class="sxs-lookup"><span data-stu-id="674e1-209">In addition toohello required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="674e1-210">Szczegółowe informacje o hello opcjonalne pola znajdują się w hello [odwołania do jednostki interfejsu API usługi Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span><span class="sxs-lookup"><span data-stu-id="674e1-210">Details on hello optional fields can be found in hello [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="674e1-211">Widać, jak żądania POST hello jest tworzony w `B2CGraphClient.SendGraphPostRequest(...)`.</span><span class="sxs-lookup"><span data-stu-id="674e1-211">You can see how hello POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="674e1-212">Dołącza toohello tokenu dostępu `Authorization` nagłówka żądania hello.</span><span class="sxs-lookup"><span data-stu-id="674e1-212">It attaches an access token toohello `Authorization` header of hello request.</span></span>
* <span data-ttu-id="674e1-213">Ustawia `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="674e1-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="674e1-214">Zawiera obiekt użytkownika JSON hello hello treści żądania hello.</span><span class="sxs-lookup"><span data-stu-id="674e1-214">It includes hello JSON user object in hello body of hello request.</span></span>

> [!NOTE]
> <span data-ttu-id="674e1-215">Jeśli hello kont, które mają toomigrate z istniejącym magazynem użytkownika ma niższe siły hasła niż hello [siły silne hasło, wymuszane przez usługę Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), można wyłączyć przy użyciu hello Wymaganiesilnehasłohello`DisableStrongPassword`wartość hello `passwordPolicies` właściwości.</span><span class="sxs-lookup"><span data-stu-id="674e1-215">If hello accounts that you want toomigrate from an existing user store has lower password strength than hello [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable hello strong password requirement using hello `DisableStrongPassword` value in hello `passwordPolicies` property.</span></span> <span data-ttu-id="674e1-216">Na przykład można zmodyfikować hello Utwórz żądanie użytkownika podanego powyżej w następujący sposób: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span><span class="sxs-lookup"><span data-stu-id="674e1-216">For instance, you can modify hello create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="674e1-217">Aktualizowanie kont użytkownika klienta</span><span class="sxs-lookup"><span data-stu-id="674e1-217">Update consumer user accounts</span></span>
<span data-ttu-id="674e1-218">Podczas aktualizowania obiektów użytkowników procesu hello jest podobne toohello, jednej z nich toocreate obiekty użytkownika.</span><span class="sxs-lookup"><span data-stu-id="674e1-218">When you update user objects, hello process is similar toohello one you use toocreate user objects.</span></span> <span data-ttu-id="674e1-219">Ten proces wykorzystuje hello HTTP, ale `PATCH` metody:</span><span class="sxs-lookup"><span data-stu-id="674e1-219">But this process uses hello HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

<span data-ttu-id="674e1-220">Spróbuj tooupdate użytkownika, aktualizując nowych danych plików JSON.</span><span class="sxs-lookup"><span data-stu-id="674e1-220">Try tooupdate a user by updating your JSON files with new data.</span></span> <span data-ttu-id="674e1-221">Następnie można użyć `B2CGraphClient` toorun jednego z tych poleceń:</span><span class="sxs-lookup"><span data-stu-id="674e1-221">You can then use `B2CGraphClient` toorun one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="674e1-222">Sprawdź hello `B2CGraphClient.SendGraphPatchRequest(...)` metody, aby uzyskać więcej informacji na temat toosend tego żądania.</span><span class="sxs-lookup"><span data-stu-id="674e1-222">Inspect hello `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how toosend this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="674e1-223">Wyszukiwania użytkowników</span><span class="sxs-lookup"><span data-stu-id="674e1-223">Search users</span></span>
<span data-ttu-id="674e1-224">Możesz wyszukać użytkowników w dzierżawie usługi B2C na kilka sposobów.</span><span class="sxs-lookup"><span data-stu-id="674e1-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="674e1-225">Jeden, za pomocą obiektu o identyfikatorze lub dwóch przy użyciu identyfikatora logowania użytkownika hello hello użytkownika (tj. hello `signInNames` właściwości).</span><span class="sxs-lookup"><span data-stu-id="674e1-225">One, using hello user's object ID or two, using hello user's sign-in identifer (i.e., hello `signInNames` property).</span></span>

<span data-ttu-id="674e1-226">Uruchom jedno z powitania po toosearch poleceń dla określonego użytkownika:</span><span class="sxs-lookup"><span data-stu-id="674e1-226">Run one of hello following commands toosearch for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="674e1-227">Oto kilka przykładów:</span><span class="sxs-lookup"><span data-stu-id="674e1-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="674e1-228">Usuwanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="674e1-228">Delete users</span></span>
<span data-ttu-id="674e1-229">proces Hello związanych z usuwaniem użytkowników jest prosta.</span><span class="sxs-lookup"><span data-stu-id="674e1-229">hello process for deleting a user is straightforward.</span></span> <span data-ttu-id="674e1-230">Użyj hello HTTP `DELETE` metody konstrukcji hello adresu URL i z hello Popraw identyfikator obiektu:</span><span class="sxs-lookup"><span data-stu-id="674e1-230">Use hello HTTP `DELETE` method and construct hello URL with hello correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="674e1-231">toosee przykład, wprowadź tego polecenia i widoku hello delete żądania wydruku toohello konsoli:</span><span class="sxs-lookup"><span data-stu-id="674e1-231">toosee an example, enter this command and view hello delete request that is printed toohello console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="674e1-232">Sprawdź hello `B2CGraphClient.SendGraphDeleteRequest(...)` metody, aby uzyskać więcej informacji na temat toosend tego żądania.</span><span class="sxs-lookup"><span data-stu-id="674e1-232">Inspect hello `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how toosend this request.</span></span>

<span data-ttu-id="674e1-233">W przystawce Zarządzanie toouser dodanie można wykonywać wiele innych działania hello Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="674e1-233">You can perform many other actions with hello Azure AD Graph API in addition toouser management.</span></span> <span data-ttu-id="674e1-234">[Dokumentacja interfejsu API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) podano szczegółowe informacje dotyczące każdej akcji, wraz z próbki żądań.</span><span class="sxs-lookup"><span data-stu-id="674e1-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="674e1-235">Używanie atrybutów niestandardowych</span><span class="sxs-lookup"><span data-stu-id="674e1-235">Use custom attributes</span></span>
<span data-ttu-id="674e1-236">Większość aplikacji klienta należy toostore pewien typ informacji o profilu użytkownika niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="674e1-236">Most consumer applications need toostore some type of custom user profile information.</span></span> <span data-ttu-id="674e1-237">Można to zrobić jednym ze sposobów jest toodefine atrybutu niestandardowego w dzierżawie usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="674e1-237">One way you can do this is toodefine a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="674e1-238">Następnie można traktować tego atrybutu hello samo Traktuj innych właściwości dla obiektu user.</span><span class="sxs-lookup"><span data-stu-id="674e1-238">You can then treat that attribute hello same way you treat any other property on a user object.</span></span> <span data-ttu-id="674e1-239">Można zaktualizować atrybutu hello, usuń atrybut hello, zapytania przy użyciu atrybutu hello, wysyłanie atrybutu hello jako oświadczenia w tokeny logowania i inne.</span><span class="sxs-lookup"><span data-stu-id="674e1-239">You can update hello attribute, delete hello attribute, query by hello attribute, send hello attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="674e1-240">toodefine atrybutu niestandardowego w dzierżawie usługi B2C, zobacz hello [odwołanie do atrybutu niestandardowego B2C](active-directory-b2c-reference-custom-attr.md).</span><span class="sxs-lookup"><span data-stu-id="674e1-240">toodefine a custom attribute in your B2C tenant, see hello [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="674e1-241">Możesz wyświetlić hello atrybuty niestandardowe zdefiniowane w dzierżawie usługi B2C przy użyciu `B2CGraphClient`:</span><span class="sxs-lookup"><span data-stu-id="674e1-241">You can view hello custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="674e1-242">dane wyjściowe Hello tych funkcji ujawnia hello szczegóły każdego z atrybutów niestandardowych, takich jak:</span><span class="sxs-lookup"><span data-stu-id="674e1-242">hello output of these functions reveals hello details of each custom attribute, such as:</span></span>

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

<span data-ttu-id="674e1-243">Można użyć hello Pełna nazwa, takich jak `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, jako właściwość obiektów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="674e1-243">You can use hello full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="674e1-244">Zaktualizuj plik JSON o hello nowej właściwości i wartości dla właściwości hello, a następnie uruchom:</span><span class="sxs-lookup"><span data-stu-id="674e1-244">Update your .json file with hello new property and a value for hello property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="674e1-245">Za pomocą `B2CGraphClient`, masz aplikacji usługi, który można programowo zarządzać użytkownicy dzierżawy B2C.</span><span class="sxs-lookup"><span data-stu-id="674e1-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="674e1-246">`B2CGraphClient`używa własnego toohello tooauthenticate tożsamości aplikacji interfejsu API usługi Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="674e1-246">`B2CGraphClient` uses its own application identity tooauthenticate toohello Azure AD Graph API.</span></span> <span data-ttu-id="674e1-247">Uzyskuje on również tokenów przy użyciu klucza tajnego klienta.</span><span class="sxs-lookup"><span data-stu-id="674e1-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="674e1-248">Ponieważ ta funkcja jest dołączyć do aplikacji, należy pamiętać o kilka najważniejszych dla aplikacji B2C:</span><span class="sxs-lookup"><span data-stu-id="674e1-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="674e1-249">Należy toogrant hello aplikacji hello odpowiednie uprawnienia w dzierżawie powitalnych.</span><span class="sxs-lookup"><span data-stu-id="674e1-249">You need toogrant hello application hello proper permissions in hello tenant.</span></span>
* <span data-ttu-id="674e1-250">Teraz należy tokenów dostępu tooget ADAL (nie MSAL) toouse.</span><span class="sxs-lookup"><span data-stu-id="674e1-250">For now, you need toouse ADAL (not MSAL) tooget access tokens.</span></span> <span data-ttu-id="674e1-251">(Możesz również wysłać wiadomości protokołu bezpośrednio, bez korzystania z biblioteki.)</span><span class="sxs-lookup"><span data-stu-id="674e1-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="674e1-252">Po wywołaniu interfejsu API programu Graph hello użyj `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="674e1-252">When you call hello Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="674e1-253">Podczas tworzenia i aktualizowania użytkowników konsumenta, kilka właściwości są wymagane, zgodnie z powyższym opisem.</span><span class="sxs-lookup"><span data-stu-id="674e1-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="674e1-254">Jeśli masz pytania lub żądań dla akcji, którą chcesz tooperform przy użyciu interfejsu API programu Graph hello na dzierżawę B2C, zostaw komentarz w tym artykule lub plików problemu w repozytorium przykładowy kod GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="674e1-254">If you have any questions or requests for actions you would like tooperform by using hello Graph API on your B2C tenant, leave a comment on this article or file an issue in hello GitHub code sample repository.</span></span>

