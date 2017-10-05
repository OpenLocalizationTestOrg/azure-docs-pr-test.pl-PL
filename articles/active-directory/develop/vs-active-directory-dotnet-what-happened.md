---
title: "Zmiany wprowadzone do projektu MVC podczas łączenia z usługą Azure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, co się dzieje z projektu MVC podczas łączenia z usługą Azure AD za pomocą usługi Visual Studio połączone"
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
ms.openlocfilehash: 095411a7fc854f4dce11921adb0f57c5389a8e13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="0011d-103">Co się stało z projektu MVC (usługa Visual Studio usługi Azure Active Directory połączono)?</span><span class="sxs-lookup"><span data-stu-id="0011d-103">What happened to my MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0011d-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="0011d-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="0011d-105">Co się stało</span><span class="sxs-lookup"><span data-stu-id="0011d-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="0011d-106">Odwołania zostały dodane</span><span class="sxs-lookup"><span data-stu-id="0011d-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="0011d-107">Odwołania do pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="0011d-107">NuGet package references</span></span>
* <span data-ttu-id="0011d-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="0011d-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="0011d-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="0011d-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="0011d-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="0011d-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="0011d-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="0011d-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="0011d-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="0011d-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="0011d-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="0011d-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="0011d-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="0011d-114">**Owin**</span></span>
* <span data-ttu-id="0011d-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="0011d-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="0011d-116">Odwołania do .NET</span><span class="sxs-lookup"><span data-stu-id="0011d-116">.NET references</span></span>
* <span data-ttu-id="0011d-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="0011d-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="0011d-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="0011d-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="0011d-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="0011d-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="0011d-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="0011d-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="0011d-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="0011d-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="0011d-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="0011d-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="0011d-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="0011d-123">**Owin**</span></span>
* <span data-ttu-id="0011d-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="0011d-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="0011d-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="0011d-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="0011d-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="0011d-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="0011d-127">Kod został dodany.</span><span class="sxs-lookup"><span data-stu-id="0011d-127">Code has been added</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="0011d-128">Pliki kodu zostały dodane do projektu</span><span class="sxs-lookup"><span data-stu-id="0011d-128">Code files were added to your project</span></span>
<span data-ttu-id="0011d-129">Klasa uruchamiania uwierzytelniania, **App_Start/Startup.Auth.cs** został dodany do projektu zawierającego Logika uruchamiania dla uwierzytelniania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0011d-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="0011d-130">Klasy kontrolera, Controllers/AccountController.cs dodano również, który zawiera **SignIn()** i **SignOut()** metody.</span><span class="sxs-lookup"><span data-stu-id="0011d-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="0011d-131">Na koniec widoku częściowego, **Views/Shared/_LoginPartial.cshtml** dodano zawierającej łącze akcji dla SignIn/SignOut.</span><span class="sxs-lookup"><span data-stu-id="0011d-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="0011d-132">Kod uruchomienia został dodany do projektu</span><span class="sxs-lookup"><span data-stu-id="0011d-132">Startup code was added to your project</span></span>
<span data-ttu-id="0011d-133">Jeśli użytkownik ma już klasy uruchamiania w projekcie, **konfiguracji** metoda została zaktualizowana na obejmują wywołania **ConfigureAuth(app)**.</span><span class="sxs-lookup"><span data-stu-id="0011d-133">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to **ConfigureAuth(app)**.</span></span> <span data-ttu-id="0011d-134">W przeciwnym razie klasa uruchamiania został dodany do projektu.</span><span class="sxs-lookup"><span data-stu-id="0011d-134">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="0011d-135">Z pliku app.config lub web.config zawiera nowe wartości konfiguracji</span><span class="sxs-lookup"><span data-stu-id="0011d-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="0011d-136">Dodano następujące pozycje konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0011d-136">The following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="The selected Azure AD Domain" />
        <add key="ida:TenantId" value="The Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="0011d-137">Utworzono aplikację usługi Azure Active Directory (AD)</span><span class="sxs-lookup"><span data-stu-id="0011d-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="0011d-138">Aplikacja Azure AD został utworzony w katalogu, który wybrano w kreatorze.</span><span class="sxs-lookup"><span data-stu-id="0011d-138">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="0011d-139">Jeśli zaznaczone I *wyłączenie uwierzytelniania indywidualnych kont użytkowników*, dodatkowe zmiany wprowadzone do projektu?</span><span class="sxs-lookup"><span data-stu-id="0011d-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="0011d-140">Odwołania do pakietu NuGet zostały usunięte, a pliki zostały usunięte i kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="0011d-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="0011d-141">W zależności od stanu projektu może być konieczne ręczne usunięcie dodatkowe informacje lub pliki, lub zmodyfikuj kod zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="0011d-141">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="0011d-142">Odwołania do pakietu NuGet usunięte (dla tych obecny)</span><span class="sxs-lookup"><span data-stu-id="0011d-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="0011d-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="0011d-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="0011d-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="0011d-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="0011d-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="0011d-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="0011d-146">Pliki kodu kopii zapasowej i usunąć (dla tych obecny)</span><span class="sxs-lookup"><span data-stu-id="0011d-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="0011d-147">Każdy z następujących plików został kopii zapasowej i usunięte z projektu.</span><span class="sxs-lookup"><span data-stu-id="0011d-147">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="0011d-148">Pliki kopii zapasowej znajdują się w folderze "Kopia zapasowa" w głównym katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="0011d-148">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="0011d-149">**App_Start\IdentityConfig.CS**</span><span class="sxs-lookup"><span data-stu-id="0011d-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="0011d-150">**Controllers\ManageController.CS**</span><span class="sxs-lookup"><span data-stu-id="0011d-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="0011d-151">**Models\IdentityModels.CS**</span><span class="sxs-lookup"><span data-stu-id="0011d-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="0011d-152">**Models\ManageViewModels.CS**</span><span class="sxs-lookup"><span data-stu-id="0011d-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="0011d-153">Pliki kodu kopii zapasowej (przez te obecny)</span><span class="sxs-lookup"><span data-stu-id="0011d-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="0011d-154">Każdy z następujących plików utworzono kopię zapasową przed figury geometrycznej.</span><span class="sxs-lookup"><span data-stu-id="0011d-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="0011d-155">Pliki kopii zapasowej znajdują się w folderze "Kopia zapasowa" w głównym katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="0011d-155">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="0011d-156">**Startup.CS**</span><span class="sxs-lookup"><span data-stu-id="0011d-156">**Startup.cs**</span></span>
* <span data-ttu-id="0011d-157">**App_Start\Startup.auth.CS**</span><span class="sxs-lookup"><span data-stu-id="0011d-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="0011d-158">**Controllers\AccountController.CS**</span><span class="sxs-lookup"><span data-stu-id="0011d-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="0011d-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="0011d-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="0011d-160">Jeśli zaznaczone I *odczytuj dane katalogu*, dodatkowe zmiany wprowadzone do projektu?</span><span class="sxs-lookup"><span data-stu-id="0011d-160">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
<span data-ttu-id="0011d-161">Dodano dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="0011d-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="0011d-162">Dodatkowe informacje o pakiecie NuGet</span><span class="sxs-lookup"><span data-stu-id="0011d-162">Additional NuGet package references</span></span>
* <span data-ttu-id="0011d-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="0011d-163">**EntityFramework**</span></span>
* <span data-ttu-id="0011d-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="0011d-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="0011d-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="0011d-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="0011d-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="0011d-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="0011d-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="0011d-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="0011d-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="0011d-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="0011d-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="0011d-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="0011d-170">Dodatkowe informacje o .NET</span><span class="sxs-lookup"><span data-stu-id="0011d-170">Additional .NET references</span></span>
* <span data-ttu-id="0011d-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="0011d-171">**EntityFramework**</span></span>
* <span data-ttu-id="0011d-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="0011d-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="0011d-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="0011d-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="0011d-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="0011d-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="0011d-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="0011d-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="0011d-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="0011d-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="0011d-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="0011d-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="0011d-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="0011d-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="0011d-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="0011d-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-to-your-project"></a><span data-ttu-id="0011d-180">Dodatkowe pliki kodu zostały dodane do projektu</span><span class="sxs-lookup"><span data-stu-id="0011d-180">Additional Code files were added to your project</span></span>
<span data-ttu-id="0011d-181">Dwa pliki zostały dodane do obsługi buforowania tokenu: **Models\ADALTokenCache.cs** i **Models\ApplicationDbContext.cs**.</span><span class="sxs-lookup"><span data-stu-id="0011d-181">Two files were added to support token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="0011d-182">Aby zilustrować podczas uzyskiwania dostępu do informacji profilu użytkownika przy użyciu wykresu Azure API dodano dodatkowego kontrolera i widoku.</span><span class="sxs-lookup"><span data-stu-id="0011d-182">An additional controller and view were added to illustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="0011d-183">Te pliki są **Controllers\UserProfileController.cs** i **Views\UserProfile\Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="0011d-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-to-your-project"></a><span data-ttu-id="0011d-184">Dodatkowy kod startowy został dodany do projektu</span><span class="sxs-lookup"><span data-stu-id="0011d-184">Additional Startup code was added to your project</span></span>
<span data-ttu-id="0011d-185">W **startup.auth.cs** pliku, nowe **OpenIdConnectAuthenticationNotifications** obiekt został dodany do **powiadomienia** członek  **OpenIdConnectAuthenticationOptions**.</span><span class="sxs-lookup"><span data-stu-id="0011d-185">In the **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added to the **Notifications** member of the **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="0011d-186">To jest umożliwienie otrzymywanie kodu OAuth i wymianę tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="0011d-186">This is to enable receiving the OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="0011d-187">Dodatkowe zmian do pliku web.config lub app.config</span><span class="sxs-lookup"><span data-stu-id="0011d-187">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="0011d-188">Dodano następujące wpisy dodatkowe czynności konfiguracyjne.</span><span class="sxs-lookup"><span data-stu-id="0011d-188">The following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="0011d-189">Dodano konfiguracji sekcje i parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="0011d-189">The following configuration sections and connection string have been added.</span></span>

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


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="0011d-190">Zaktualizowano aplikację usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0011d-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="0011d-191">Zaktualizowano aplikację usługi Azure Active Directory do uwzględnienia *odczytuj dane katalogu* uprawnień i dodatkowe klucz został utworzony, który następnie została użyta jako *ida: ClientSecret* w  **plik Web.config** pliku.</span><span class="sxs-lookup"><span data-stu-id="0011d-191">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:ClientSecret* in the **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0011d-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0011d-192">Next steps</span></span>
- [<span data-ttu-id="0011d-193">Dowiedz się więcej o usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0011d-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

