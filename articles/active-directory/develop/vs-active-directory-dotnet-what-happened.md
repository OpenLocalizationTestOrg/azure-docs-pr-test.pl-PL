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
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a>Jakie wystąpiły toomy MVC projektu (Visual Studio usługi Azure Active Directory połączona usługa)?
> [!div class="op_single_selector"]
> * [Wprowadzenie](vs-active-directory-dotnet-getting-started.md)
> * [Co się stało](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>Odwołania zostały dodane
### <a name="nuget-package-references"></a>Odwołania do pakietu NuGet
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel.Tokens.Jwt**

### <a name="net-references"></a>Odwołania do .NET
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel**
* **System.IdentityModel.Tokens.Jwt**
* **System.Runtime.Serialization**

## <a name="code-has-been-added"></a>Kod został dodany.
### <a name="code-files-were-added-tooyour-project"></a>Pliki kodu zostały dodane tooyour projektu
Klasa uruchamiania uwierzytelniania, **App_Start/Startup.Auth.cs** został dodany projekt tooyour zawierający Logika uruchamiania dla uwierzytelniania usługi Azure AD. Klasy kontrolera, Controllers/AccountController.cs dodano również, który zawiera **SignIn()** i **SignOut()** metody. Na koniec widoku częściowego, **Views/Shared/_LoginPartial.cshtml** dodano zawierającej łącze akcji dla SignIn/SignOut.

### <a name="startup-code-was-added-tooyour-project"></a>Kod uruchomienia dodano tooyour projektu
Jeśli użytkownik ma już klasy uruchamiania w projekcie, hello **konfiguracji** — metoda został zaktualizowany tooinclude wywołanie za**ConfigureAuth(app)**. W przeciwnym razie klasa uruchamiania dodano tooyour projektu.

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a>Z pliku app.config lub web.config zawiera nowe wartości konfiguracji
Dodano Hello następujące pozycje konfiguracji.

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a>Utworzono aplikację usługi Azure Active Directory (AD)
Aplikacja Azure AD został utworzony w katalogu hello, które wybrano w Kreatorze hello.

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>Jeśli zaznaczone I *wyłączenie uwierzytelniania indywidualnych kont użytkowników*, dodatkowe zmiany wprowadzone toomy projektu?
Odwołania do pakietu NuGet zostały usunięte, a pliki zostały usunięte i kopii zapasowej. W zależności od stanu hello projektu może być toomanually Usuń dodatkowe informacje lub plików albo zmodyfikować kod zależnie od potrzeb.

### <a name="nuget-package-references-removed-for-those-present"></a>Odwołania do pakietu NuGet usunięte (dla tych obecny)
* **Microsoft.AspNet.Identity.Core**
* **Microsoft.AspNet.Identity.EntityFramework**
* **Microsoft.AspNet.Identity.Owin**

### <a name="code-files-backed-up-and-removed-for-those-present"></a>Pliki kodu kopii zapasowej i usunąć (dla tych obecny)
Każdej z następujących plików kopii zapasowej i usunięta z projektu hello. Pliki kopii zapasowej znajdują się w folderze "Kopia zapasowa" w głównym katalogu projektu hello hello.

* **App_Start\IdentityConfig.CS**
* **Controllers\ManageController.CS**
* **Models\IdentityModels.CS**
* **Models\ManageViewModels.CS**

### <a name="code-files-backed-up-for-those-present"></a>Pliki kodu kopii zapasowej (przez te obecny)
Każdy z następujących plików utworzono kopię zapasową przed figury geometrycznej. Pliki kopii zapasowej znajdują się w folderze "Kopia zapasowa" w głównym katalogu projektu hello hello.

* **Startup.CS**
* **App_Start\Startup.auth.CS**
* **Controllers\AccountController.CS**
* **Views\Shared\_LoginPartial.cshtml**

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>Jeśli zaznaczone I *odczytuj dane katalogu*, dodatkowe zmiany wprowadzone toomy projektu?
Dodano dodatkowe informacje.

### <a name="additional-nuget-package-references"></a>Dodatkowe informacje o pakiecie NuGet
* **EntityFramework**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **System.Spatial**

### <a name="additional-net-references"></a>Dodatkowe informacje o .NET
* **EntityFramework**
* **EntityFramework.SqlServer**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**
* **System.Spatial**

### <a name="additional-code-files-were-added-tooyour-project"></a>Dodatkowe pliki kodu zostały dodane tooyour projektu
Dwa pliki zostały dodane toosupport buforowaniem tokena: **Models\ADALTokenCache.cs** i **Models\ApplicationDbContext.cs**.  Dodatkowego kontrolera i widoku dodano tooillustrate uzyskiwanie dostępu do informacji profilu użytkownika przy użyciu wykresu Azure interfejsów API.  Te pliki są **Controllers\UserProfileController.cs** i **Views\UserProfile\Index.cshtml**.

### <a name="additional-startup-code-was-added-tooyour-project"></a>Kod uruchomienia dodatkowych dodano tooyour projektu
W hello **startup.auth.cs** pliku, nowe **OpenIdConnectAuthenticationNotifications** obiekt został dodany toohello **powiadomienia** członkiem hello  **OpenIdConnectAuthenticationOptions**.  Jest to tooenable otrzymywanie hello OAuth kodu i wymianę tokenu dostępu.

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Wprowadzono dodatkowe zmiany, tooyour app.config lub web.config
Witaj następujące wpisy dodatkowe czynności konfiguracyjne zostały dodane.

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

Witaj konfiguracji sekcje i parametry połączenia zostały dodane.

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


### <a name="your-azure-active-directory-app-was-updated"></a>Zaktualizowano aplikację usługi Azure Active Directory
Aplikację usługi Azure Active Directory został zaktualizowany tooinclude hello *odczytuj dane katalogu* uprawnień i dodatkowego klucza została utworzona, który następnie została użyta jako hello *ida: ClientSecret* w hello  **plik Web.config** pliku.

## <a name="next-steps"></a>Następne kroki
- [Dowiedz się więcej o usłudze Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

