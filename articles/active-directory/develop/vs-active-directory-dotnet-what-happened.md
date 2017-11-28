---
title: "tooa aaaChanges wprowadzone MVC projektu po podłączeniu tooAzure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, co się stanie projektu MVC tooyour po podłączeniu tooAzure AD za pomocą usługi Visual Studio połączone"
services: active-directory
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 8b24adde-547e-4ffe-824a-2029ba210216
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 5e6d4ce5331eacca5fc83429017ae454fadcc8e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="23f71-103">Jakie wystąpiły toomy MVC projektu (Visual Studio usługi Azure Active Directory połączona usługa)?</span><span class="sxs-lookup"><span data-stu-id="23f71-103">What happened toomy MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="23f71-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="23f71-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="23f71-105">Co się stało</span><span class="sxs-lookup"><span data-stu-id="23f71-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="23f71-106">Odwołania zostały dodane</span><span class="sxs-lookup"><span data-stu-id="23f71-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="23f71-107">Odwołania do pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="23f71-107">NuGet package references</span></span>
* <span data-ttu-id="23f71-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="23f71-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="23f71-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="23f71-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="23f71-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="23f71-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="23f71-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="23f71-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="23f71-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="23f71-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="23f71-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="23f71-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="23f71-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="23f71-114">**Owin**</span></span>
* <span data-ttu-id="23f71-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="23f71-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="23f71-116">Odwołania do .NET</span><span class="sxs-lookup"><span data-stu-id="23f71-116">.NET references</span></span>
* <span data-ttu-id="23f71-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="23f71-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="23f71-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="23f71-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="23f71-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="23f71-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="23f71-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="23f71-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="23f71-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="23f71-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="23f71-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="23f71-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="23f71-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="23f71-123">**Owin**</span></span>
* <span data-ttu-id="23f71-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="23f71-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="23f71-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="23f71-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="23f71-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="23f71-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="23f71-127">Kod został dodany.</span><span class="sxs-lookup"><span data-stu-id="23f71-127">Code has been added</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="23f71-128">Pliki kodu zostały dodane tooyour projektu</span><span class="sxs-lookup"><span data-stu-id="23f71-128">Code files were added tooyour project</span></span>
<span data-ttu-id="23f71-129">Klasa uruchamiania uwierzytelniania, **App_Start/Startup.Auth.cs** został dodany projekt tooyour zawierający Logika uruchamiania dla uwierzytelniania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23f71-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="23f71-130">Klasy kontrolera, Controllers/AccountController.cs dodano również, który zawiera **SignIn()** i **SignOut()** metody.</span><span class="sxs-lookup"><span data-stu-id="23f71-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="23f71-131">Na koniec widoku częściowego, **Views/Shared/_LoginPartial.cshtml** dodano zawierającej łącze akcji dla SignIn/SignOut.</span><span class="sxs-lookup"><span data-stu-id="23f71-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="23f71-132">Kod uruchomienia dodano tooyour projektu</span><span class="sxs-lookup"><span data-stu-id="23f71-132">Startup code was added tooyour project</span></span>
<span data-ttu-id="23f71-133">Jeśli użytkownik ma już klasy uruchamiania w projekcie, hello **konfiguracji** — metoda został zaktualizowany tooinclude wywołanie za**ConfigureAuth(app)**.</span><span class="sxs-lookup"><span data-stu-id="23f71-133">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too**ConfigureAuth(app)**.</span></span> <span data-ttu-id="23f71-134">W przeciwnym razie klasa uruchamiania dodano tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="23f71-134">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="23f71-135">Z pliku app.config lub web.config zawiera nowe wartości konfiguracji</span><span class="sxs-lookup"><span data-stu-id="23f71-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="23f71-136">Dodano Hello następujące pozycje konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="23f71-136">hello following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="23f71-137">Utworzono aplikację usługi Azure Active Directory (AD)</span><span class="sxs-lookup"><span data-stu-id="23f71-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="23f71-138">Aplikacja Azure AD został utworzony w katalogu hello, które wybrano w Kreatorze hello.</span><span class="sxs-lookup"><span data-stu-id="23f71-138">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="23f71-139">Jeśli zaznaczone I *wyłączenie uwierzytelniania indywidualnych kont użytkowników*, dodatkowe zmiany wprowadzone toomy projektu?</span><span class="sxs-lookup"><span data-stu-id="23f71-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="23f71-140">Odwołania do pakietu NuGet zostały usunięte, a pliki zostały usunięte i kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="23f71-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="23f71-141">W zależności od stanu hello projektu może być toomanually Usuń dodatkowe informacje lub plików albo zmodyfikować kod zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="23f71-141">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="23f71-142">Odwołania do pakietu NuGet usunięte (dla tych obecny)</span><span class="sxs-lookup"><span data-stu-id="23f71-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="23f71-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="23f71-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="23f71-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="23f71-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="23f71-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="23f71-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="23f71-146">Pliki kodu kopii zapasowej i usunąć (dla tych obecny)</span><span class="sxs-lookup"><span data-stu-id="23f71-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="23f71-147">Każdej z następujących plików kopii zapasowej i usunięta z projektu hello.</span><span class="sxs-lookup"><span data-stu-id="23f71-147">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="23f71-148">Pliki kopii zapasowej znajdują się w folderze "Kopia zapasowa" w głównym katalogu projektu hello hello.</span><span class="sxs-lookup"><span data-stu-id="23f71-148">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="23f71-149">**App_Start\IdentityConfig.CS**</span><span class="sxs-lookup"><span data-stu-id="23f71-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="23f71-150">**Controllers\ManageController.CS**</span><span class="sxs-lookup"><span data-stu-id="23f71-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="23f71-151">**Models\IdentityModels.CS**</span><span class="sxs-lookup"><span data-stu-id="23f71-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="23f71-152">**Models\ManageViewModels.CS**</span><span class="sxs-lookup"><span data-stu-id="23f71-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="23f71-153">Pliki kodu kopii zapasowej (przez te obecny)</span><span class="sxs-lookup"><span data-stu-id="23f71-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="23f71-154">Każdy z następujących plików utworzono kopię zapasową przed figury geometrycznej.</span><span class="sxs-lookup"><span data-stu-id="23f71-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="23f71-155">Pliki kopii zapasowej znajdują się w folderze "Kopia zapasowa" w głównym katalogu projektu hello hello.</span><span class="sxs-lookup"><span data-stu-id="23f71-155">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="23f71-156">**Startup.CS**</span><span class="sxs-lookup"><span data-stu-id="23f71-156">**Startup.cs**</span></span>
* <span data-ttu-id="23f71-157">**App_Start\Startup.auth.CS**</span><span class="sxs-lookup"><span data-stu-id="23f71-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="23f71-158">**Controllers\AccountController.CS**</span><span class="sxs-lookup"><span data-stu-id="23f71-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="23f71-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="23f71-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="23f71-160">Jeśli zaznaczone I *odczytuj dane katalogu*, dodatkowe zmiany wprowadzone toomy projektu?</span><span class="sxs-lookup"><span data-stu-id="23f71-160">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="23f71-161">Dodano dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="23f71-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="23f71-162">Dodatkowe informacje o pakiecie NuGet</span><span class="sxs-lookup"><span data-stu-id="23f71-162">Additional NuGet package references</span></span>
* <span data-ttu-id="23f71-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="23f71-163">**EntityFramework**</span></span>
* <span data-ttu-id="23f71-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="23f71-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="23f71-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="23f71-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="23f71-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="23f71-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="23f71-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="23f71-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="23f71-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="23f71-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="23f71-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="23f71-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="23f71-170">Dodatkowe informacje o .NET</span><span class="sxs-lookup"><span data-stu-id="23f71-170">Additional .NET references</span></span>
* <span data-ttu-id="23f71-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="23f71-171">**EntityFramework**</span></span>
* <span data-ttu-id="23f71-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="23f71-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="23f71-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="23f71-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="23f71-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="23f71-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="23f71-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="23f71-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="23f71-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="23f71-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="23f71-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="23f71-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="23f71-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="23f71-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="23f71-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="23f71-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-tooyour-project"></a><span data-ttu-id="23f71-180">Dodatkowe pliki kodu zostały dodane tooyour projektu</span><span class="sxs-lookup"><span data-stu-id="23f71-180">Additional Code files were added tooyour project</span></span>
<span data-ttu-id="23f71-181">Dwa pliki zostały dodane toosupport buforowaniem tokena: **Models\ADALTokenCache.cs** i **Models\ApplicationDbContext.cs**.</span><span class="sxs-lookup"><span data-stu-id="23f71-181">Two files were added toosupport token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="23f71-182">Dodatkowego kontrolera i widoku dodano tooillustrate uzyskiwanie dostępu do informacji profilu użytkownika przy użyciu wykresu Azure interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="23f71-182">An additional controller and view were added tooillustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="23f71-183">Te pliki są **Controllers\UserProfileController.cs** i **Views\UserProfile\Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="23f71-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-tooyour-project"></a><span data-ttu-id="23f71-184">Kod uruchomienia dodatkowych dodano tooyour projektu</span><span class="sxs-lookup"><span data-stu-id="23f71-184">Additional Startup code was added tooyour project</span></span>
<span data-ttu-id="23f71-185">W hello **startup.auth.cs** pliku, nowe **OpenIdConnectAuthenticationNotifications** obiekt został dodany toohello **powiadomienia** członkiem hello  **OpenIdConnectAuthenticationOptions**.</span><span class="sxs-lookup"><span data-stu-id="23f71-185">In hello **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added toohello **Notifications** member of hello **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="23f71-186">Jest to tooenable otrzymywanie hello OAuth kodu i wymianę tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="23f71-186">This is tooenable receiving hello OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="23f71-187">Wprowadzono dodatkowe zmiany, tooyour app.config lub web.config</span><span class="sxs-lookup"><span data-stu-id="23f71-187">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="23f71-188">Witaj następujące wpisy dodatkowe czynności konfiguracyjne zostały dodane.</span><span class="sxs-lookup"><span data-stu-id="23f71-188">hello following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="23f71-189">Witaj konfiguracji sekcje i parametry połączenia zostały dodane.</span><span class="sxs-lookup"><span data-stu-id="23f71-189">hello following configuration sections and connection string have been added.</span></span>

    <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
    </configSections>
    <connectionStrings>
        <add name="DefaultConnection" connectionString="Data Source=(localdb)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\aspnet-[AppName + Generated Id].mdf;Initial Catalog=aspnet-[AppName + Generated Id];Integrated Security=True" providerName="System.Data.SqlClient" />
    </connectionStrings>
    <entityFramework>
        <defaultConnectionFactory type="System.Data.Entity.Infrastructure.LocalDbConnectionFactory, EntityFramework">
          <parameters>
            <parameter value="mssqllocaldb" />
          </parameters>
        </defaultConnectionFactory>
        <providers>
          <provider invariantName="System.Data.SqlClient" type="System.Data.Entity.SqlServer.SqlProviderServices, EntityFramework.SqlServer" />
        </providers>
    </entityFramework>


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="23f71-190">Zaktualizowano aplikację usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="23f71-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="23f71-191">Aplikację usługi Azure Active Directory został zaktualizowany tooinclude hello *odczytuj dane katalogu* uprawnień i dodatkowego klucza została utworzona, który następnie została użyta jako hello *ida: ClientSecret* w hello  **plik Web.config** pliku.</span><span class="sxs-lookup"><span data-stu-id="23f71-191">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:ClientSecret* in hello **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23f71-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="23f71-192">Next steps</span></span>
- [<span data-ttu-id="23f71-193">Dowiedz się więcej o usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="23f71-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

