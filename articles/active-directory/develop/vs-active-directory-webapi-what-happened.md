---
title: "Projekt WebApi tooa aaaChanges wprowadzone po podłączeniu tooAzure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, co się dzieje tooyour WebApi projektu po podłączeniu tooAzure AD za pomocą programu Visual Studio"
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
ms.openlocfilehash: 1ea77b6c75b2dc273219fa6c43f02c7a7c5312ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="eceb4-103">Jakie wystąpiły toomy WebApi projektu (Visual Studio usługi Azure Active Directory połączenia usługi)</span><span class="sxs-lookup"><span data-stu-id="eceb4-103">What happened toomy WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eceb4-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="eceb4-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="eceb4-105">Co się stało</span><span class="sxs-lookup"><span data-stu-id="eceb4-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="eceb4-106">Odwołania zostały dodane</span><span class="sxs-lookup"><span data-stu-id="eceb4-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="eceb4-107">Odwołania do pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="eceb4-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="eceb4-108">Odwołania do .NET</span><span class="sxs-lookup"><span data-stu-id="eceb4-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="eceb4-109">Zmiany kodu</span><span class="sxs-lookup"><span data-stu-id="eceb4-109">Code changes</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="eceb4-110">Pliki kodu zostały dodane tooyour projektu</span><span class="sxs-lookup"><span data-stu-id="eceb4-110">Code files were added tooyour project</span></span>
<span data-ttu-id="eceb4-111">Klasa uruchamiania uwierzytelniania, **App_Start/Startup.Auth.cs** został dodany projekt tooyour zawierający Logika uruchamiania dla uwierzytelniania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eceb4-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="eceb4-112">Kod uruchomienia dodano tooyour projektu</span><span class="sxs-lookup"><span data-stu-id="eceb4-112">Startup code was added tooyour project</span></span>
<span data-ttu-id="eceb4-113">Jeśli użytkownik ma już klasy uruchamiania w projekcie, hello **konfiguracji** — metoda został zaktualizowany tooinclude wywołanie za`ConfigureAuth(app)`.</span><span class="sxs-lookup"><span data-stu-id="eceb4-113">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too`ConfigureAuth(app)`.</span></span> <span data-ttu-id="eceb4-114">W przeciwnym razie klasa uruchamiania dodano tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="eceb4-114">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="eceb4-115">Plik app.config lub web.config zawiera nowe wartości konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="eceb4-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="eceb4-116">Dodano Hello następujące pozycje konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="eceb4-116">hello following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="eceb4-117">Utworzono aplikację usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eceb4-117">An Azure AD App was created</span></span>
<span data-ttu-id="eceb4-118">Aplikacja Azure AD został utworzony w katalogu hello, które wybrano w Kreatorze hello.</span><span class="sxs-lookup"><span data-stu-id="eceb4-118">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

[<span data-ttu-id="eceb4-119">Dowiedz się więcej o usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eceb4-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="eceb4-120">Jeśli zaznaczone I *wyłączenie uwierzytelniania indywidualnych kont użytkowników*, dodatkowe zmiany wprowadzone toomy projektu?</span><span class="sxs-lookup"><span data-stu-id="eceb4-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="eceb4-121">Odwołania do pakietu NuGet zostały usunięte, a pliki zostały usunięte i kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="eceb4-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="eceb4-122">W zależności od stanu hello projektu może być toomanually Usuń dodatkowe informacje lub plików albo zmodyfikować kod zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="eceb4-122">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="eceb4-123">Odwołania do pakietu NuGet usunięte (dla tych obecny)</span><span class="sxs-lookup"><span data-stu-id="eceb4-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="eceb4-124">Pliki kodu kopii zapasowej i usunąć (dla tych obecny)</span><span class="sxs-lookup"><span data-stu-id="eceb4-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="eceb4-125">Każdej z następujących plików kopii zapasowej i usunięta z projektu hello.</span><span class="sxs-lookup"><span data-stu-id="eceb4-125">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="eceb4-126">Pliki kopii zapasowej znajdują się w folderze "Kopia zapasowa" w głównym katalogu projektu hello hello.</span><span class="sxs-lookup"><span data-stu-id="eceb4-126">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="eceb4-127">Pliki kodu kopii zapasowej (przez te obecny)</span><span class="sxs-lookup"><span data-stu-id="eceb4-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="eceb4-128">Każdy z następujących plików utworzono kopię zapasową przed figury geometrycznej.</span><span class="sxs-lookup"><span data-stu-id="eceb4-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="eceb4-129">Pliki kopii zapasowej znajdują się w folderze "Kopia zapasowa" w głównym katalogu projektu hello hello.</span><span class="sxs-lookup"><span data-stu-id="eceb4-129">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="eceb4-130">Jeśli zaznaczone I *odczytuj dane katalogu*, dodatkowe zmiany wprowadzone toomy projektu?</span><span class="sxs-lookup"><span data-stu-id="eceb4-130">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="eceb4-131">Wprowadzono dodatkowe zmiany, tooyour app.config lub web.config</span><span class="sxs-lookup"><span data-stu-id="eceb4-131">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="eceb4-132">Witaj następujące wpisy dodatkowe czynności konfiguracyjne zostały dodane.</span><span class="sxs-lookup"><span data-stu-id="eceb4-132">hello following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="eceb4-133">Zaktualizowano aplikację usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eceb4-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="eceb4-134">Aplikację usługi Azure Active Directory został zaktualizowany tooinclude hello *odczytuj dane katalogu* uprawnień i dodatkowego klucza została utworzona, który następnie została użyta jako hello *ida: hasło* w hello `web.config` pliku.</span><span class="sxs-lookup"><span data-stu-id="eceb4-134">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:Password* in hello `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eceb4-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eceb4-135">Next steps</span></span>
- [<span data-ttu-id="eceb4-136">Dowiedz się więcej o usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eceb4-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

