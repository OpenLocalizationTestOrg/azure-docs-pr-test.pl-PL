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
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a>Jakie wystąpiły toomy WebApi projektu (Visual Studio usługi Azure Active Directory połączenia usługi)
> [!div class="op_single_selector"]
> * [Wprowadzenie](vs-active-directory-webapi-getting-started.md)
> * [Co się stało](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>Odwołania zostały dodane
### <a name="nuget-package-references"></a>Odwołania do pakietu NuGet
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a>Odwołania do .NET
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a>Zmiany kodu
### <a name="code-files-were-added-tooyour-project"></a>Pliki kodu zostały dodane tooyour projektu
Klasa uruchamiania uwierzytelniania, **App_Start/Startup.Auth.cs** został dodany projekt tooyour zawierający Logika uruchamiania dla uwierzytelniania usługi Azure AD.

### <a name="startup-code-was-added-tooyour-project"></a>Kod uruchomienia dodano tooyour projektu
Jeśli użytkownik ma już klasy uruchamiania w projekcie, hello **konfiguracji** — metoda został zaktualizowany tooinclude wywołanie za`ConfigureAuth(app)`. W przeciwnym razie klasa uruchamiania dodano tooyour projektu.

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a>Plik app.config lub web.config zawiera nowe wartości konfiguracji.
Dodano Hello następujące pozycje konfiguracji.

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a>Utworzono aplikację usługi Azure AD
Aplikacja Azure AD został utworzony w katalogu hello, które wybrano w Kreatorze hello.

[Dowiedz się więcej o usłudze Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>Jeśli zaznaczone I *wyłączenie uwierzytelniania indywidualnych kont użytkowników*, dodatkowe zmiany wprowadzone toomy projektu?
Odwołania do pakietu NuGet zostały usunięte, a pliki zostały usunięte i kopii zapasowej. W zależności od stanu hello projektu może być toomanually Usuń dodatkowe informacje lub plików albo zmodyfikować kod zależnie od potrzeb.

### <a name="nuget-package-references-removed-for-those-present"></a>Odwołania do pakietu NuGet usunięte (dla tych obecny)
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a>Pliki kodu kopii zapasowej i usunąć (dla tych obecny)
Każdej z następujących plików kopii zapasowej i usunięta z projektu hello. Pliki kopii zapasowej znajdują się w folderze "Kopia zapasowa" w głównym katalogu projektu hello hello.

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a>Pliki kodu kopii zapasowej (przez te obecny)
Każdy z następujących plików utworzono kopię zapasową przed figury geometrycznej. Pliki kopii zapasowej znajdują się w folderze "Kopia zapasowa" w głównym katalogu projektu hello hello.

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>Jeśli zaznaczone I *odczytuj dane katalogu*, dodatkowe zmiany wprowadzone toomy projektu?
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Wprowadzono dodatkowe zmiany, tooyour app.config lub web.config
Witaj następujące wpisy dodatkowe czynności konfiguracyjne zostały dodane.

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a>Zaktualizowano aplikację usługi Azure Active Directory
Aplikację usługi Azure Active Directory został zaktualizowany tooinclude hello *odczytuj dane katalogu* uprawnień i dodatkowego klucza została utworzona, który następnie została użyta jako hello *ida: hasło* w hello `web.config` pliku.

## <a name="next-steps"></a>Następne kroki
- [Dowiedz się więcej o usłudze Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

