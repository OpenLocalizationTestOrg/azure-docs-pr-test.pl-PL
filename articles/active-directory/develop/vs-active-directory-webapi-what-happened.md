---
title: "Zmiany wprowadzone do projektu WebApi podczas łączenia z usługą Azure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, co się dzieje z projektu WebApi podczas łączenia z usługą Azure AD za pomocą programu Visual Studio"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 57630aee-26a2-4326-9dbb-ea2a66daa8b0
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 086e5a9622cad681cd282345d97e0c28ee7de2fa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="34846-103">Co się stało z projektu WebApi (Visual Studio usługi Azure Active Directory połączenia usługi)</span><span class="sxs-lookup"><span data-stu-id="34846-103">What happened to my WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="34846-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="34846-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="34846-105">Co się stało</span><span class="sxs-lookup"><span data-stu-id="34846-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="34846-106">Odwołania zostały dodane</span><span class="sxs-lookup"><span data-stu-id="34846-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="34846-107">Odwołania do pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="34846-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="34846-108">Odwołania do .NET</span><span class="sxs-lookup"><span data-stu-id="34846-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="34846-109">Zmiany kodu</span><span class="sxs-lookup"><span data-stu-id="34846-109">Code changes</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="34846-110">Pliki kodu zostały dodane do projektu</span><span class="sxs-lookup"><span data-stu-id="34846-110">Code files were added to your project</span></span>
<span data-ttu-id="34846-111">Klasa uruchamiania uwierzytelniania, **App_Start/Startup.Auth.cs** został dodany do projektu zawierającego Logika uruchamiania dla uwierzytelniania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34846-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="34846-112">Kod uruchomienia został dodany do projektu</span><span class="sxs-lookup"><span data-stu-id="34846-112">Startup code was added to your project</span></span>
<span data-ttu-id="34846-113">Jeśli użytkownik ma już klasy uruchamiania w projekcie, **konfiguracji** metoda została zaktualizowana na obejmują wywołania `ConfigureAuth(app)`.</span><span class="sxs-lookup"><span data-stu-id="34846-113">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to `ConfigureAuth(app)`.</span></span> <span data-ttu-id="34846-114">W przeciwnym razie klasa uruchamiania został dodany do projektu.</span><span class="sxs-lookup"><span data-stu-id="34846-114">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="34846-115">Plik app.config lub web.config zawiera nowe wartości konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="34846-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="34846-116">Dodano następujące pozycje konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="34846-116">The following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="The App ID Uri from the wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="34846-117">Utworzono aplikację usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="34846-117">An Azure AD App was created</span></span>
<span data-ttu-id="34846-118">Aplikacja Azure AD został utworzony w katalogu, który wybrano w kreatorze.</span><span class="sxs-lookup"><span data-stu-id="34846-118">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

[<span data-ttu-id="34846-119">Dowiedz się więcej o usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34846-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="34846-120">Jeśli zaznaczone I *wyłączenie uwierzytelniania indywidualnych kont użytkowników*, dodatkowe zmiany wprowadzone do projektu?</span><span class="sxs-lookup"><span data-stu-id="34846-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="34846-121">Odwołania do pakietu NuGet zostały usunięte, a pliki zostały usunięte i kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="34846-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="34846-122">W zależności od stanu projektu może być konieczne ręczne usunięcie dodatkowe informacje lub pliki, lub zmodyfikuj kod zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="34846-122">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="34846-123">Odwołania do pakietu NuGet usunięte (dla tych obecny)</span><span class="sxs-lookup"><span data-stu-id="34846-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="34846-124">Pliki kodu kopii zapasowej i usunąć (dla tych obecny)</span><span class="sxs-lookup"><span data-stu-id="34846-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="34846-125">Każdy z następujących plików został kopii zapasowej i usunięte z projektu.</span><span class="sxs-lookup"><span data-stu-id="34846-125">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="34846-126">Pliki kopii zapasowej znajdują się w folderze "Kopia zapasowa" w głównym katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="34846-126">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="34846-127">Pliki kodu kopii zapasowej (przez te obecny)</span><span class="sxs-lookup"><span data-stu-id="34846-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="34846-128">Każdy z następujących plików utworzono kopię zapasową przed figury geometrycznej.</span><span class="sxs-lookup"><span data-stu-id="34846-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="34846-129">Pliki kopii zapasowej znajdują się w folderze "Kopia zapasowa" w głównym katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="34846-129">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="34846-130">Jeśli zaznaczone I *odczytuj dane katalogu*, dodatkowe zmiany wprowadzone do projektu?</span><span class="sxs-lookup"><span data-stu-id="34846-130">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="34846-131">Dodatkowe zmian do pliku web.config lub app.config</span><span class="sxs-lookup"><span data-stu-id="34846-131">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="34846-132">Dodano następujące wpisy dodatkowe czynności konfiguracyjne.</span><span class="sxs-lookup"><span data-stu-id="34846-132">The following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="34846-133">Zaktualizowano aplikację usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34846-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="34846-134">Zaktualizowano aplikację usługi Azure Active Directory do uwzględnienia *odczytuj dane katalogu* uprawnień i dodatkowe klucz został utworzony, który następnie została użyta jako *ida: hasło* w `web.config` pliku.</span><span class="sxs-lookup"><span data-stu-id="34846-134">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:Password* in the `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34846-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="34846-135">Next steps</span></span>
- [<span data-ttu-id="34846-136">Dowiedz się więcej o usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34846-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

