---
title: "Aplikacje, uprawnienia i zgody w usłudze Azure Active Directory. | Microsoft Docs"
description: "Program Azure AD Connect umożliwia integrowanie katalogów lokalnych z usługą Azure Active Directory. Dzięki temu tooprovide wspólną tożsamością dla usługi Office 365, Azure i aplikacji SaaS zintegrowanych z usługą Azure AD."
keywords: "wprowadzenie tooAzure AD, aplikacji, co to jest usługa Azure AD Connect, instalowania usługi active directory"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a>Aplikacje, uprawnienia i zgody w usłudze Azure Active Directory
W usłudze Azure Active Directory możesz dodać katalog tooyour aplikacji.  aplikacji Hello może się różnić w zależności od typu aplikacji hello.  aplikacje tooview w portalu klasycznym hello, wybierz katalog i wybierz aplikacje.

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule.

## <a name="types-of-apps"></a>Typy aplikacji

1. **Aplikacje z jedną dzierżawą** </br>
    - **Aplikacje pojedynczej dzierżawy** -często określany tooas aplikacji — biznesowych (LOB). Jest to hello wtedy, gdy ktoś z organizacji rozwija własnej aplikacji i chcesz użytkowników w stanie toosign toobe hello organizacji w toohello aplikacji.
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - **Aplikacje serwera Proxy aplikacji** — udostępnianie aplikacji lokalnych przy użyciu serwera Proxy aplikacji usługi AD platformy Azure, aplikacji pojedynczej dzierżawy jest zarejestrowany w dzierżawie (w toohello dodanie usługi serwera Proxy aplikacji). Ta aplikacja reprezentuje Twoją aplikację lokalną dla wszystkich interakcji w chmurze (na przykład na potrzeby uwierzytelniania). (Usługa Serwer proxy aplikacji wymaga usługi Azure AD w wersji Podstawowa lub wyższej).


2. **Aplikacje z wieloma dzierżawami**
    - **Wielodostępne aplikacji, które inne osoby mogą wyrazić zgodę na** — podobne zbyt "pojedynczej dzierżawy aplikacji, które organizacja rozwija". Podstawowa różnica Hello (oprócz hello logikę w samej aplikacji hello) polega na tym, że użytkownicy od pozostałych dzierżawców można również zgody tooand logowania aplikacji toohello.</br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - **Opracowane przez strony trzecie aplikacje z wieloma dzierżawami, na które może się zgodzić firma Contoso**. (W skrócie: „aplikacje, na które wyrażono zgodę”). Jest to po stronie Przerzucanie hello "wielodostępnych aplikacji, które rozwija organizacji". Gdy aplikacja wielodostępne innej organizacji, które zostały zaakceptowane, użytkownicy w organizacji można zgody toohello aplikacji i zaloguj tooit.
    - **Aplikacje firmy Microsoft** — aplikacje, które reprezentują usługi firmy Microsoft. Zgoda jest wymuszany przez fakt hello utworzysz hello usługi. Brak czasami specjalne UX i logiki dla niektórych aplikacji firmy, która jest często używana podczas ustanawiania zasady wokół aplikacji toohello dostępu.</br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - **Wstępnie zintegrowanych aplikacji** -aplikacji dostępnych w hello AD galerii aplikacji Azure, które można dodać tooyour katalogu tooprovide pojedynczego logowania jednokrotnego (i w niektórych przypadkach inicjowania obsługi administracyjnej) toopopular aplikacji SaaS.
    - **Logowanie jednokrotne w usłudze Azure AD**: „rzeczywiste” logowanie jednokrotne w aplikacjach, które można zintegrować z usługą Azure AD przy użyciu obsługiwanego protokołu logowania, takiego jak SAML 2.0 lub OpenID Connect. Kreator Hello przeprowadzi Cię przez proces konfigurowania go.
    - **Hasło logowania jednokrotnego**: usługi Azure AD bezpiecznie przechowuje poświadczenia użytkownika hello aplikacji hello, a poświadczenia hello są "wstrzykuje" hello logowania w formularzu przez hello rozszerzenia przeglądarki dostępu aplikacji usługi Azure AD. To działanie jest znane również jako „magazynowanie haseł”.

## <a name="permissions"></a>Uprawnienia

Podczas rejestrowania aplikacji hello użytkownika wykonującego hello rejestracji aplikacji (czyli hello developer) definiuje uprawnienia aplikacji hello musi mieć dostęp do i zasoby. (hello zasoby są, same zdefiniowany jako innych aplikacji). Ktoś tworzeniem aplikacji czytnika poczty, będzie na przykład stan czy aplikacji musi mieć uprawnienie "Dostęp do skrzynek pocztowych jako hello zalogowanego użytkownika" hello w hello "Office 365 usługi Exchange Online" zasobów:
    
![](media/active-directory-apps-permissions-consent/apps6.png)

Aby dla jednej aplikacji (powitania klienta) toorequest niektóre uprawnienia z innej aplikacji (hello zasobów) deweloperów hello hello zasobów aplikacji definiuje hello uprawnienia, które istnieją. W naszym przykładzie firmy Microsoft, właściciela hello hello "Office 365 usługi Exchange Online" zasobów aplikacji zdefiniowano uprawnień o nazwie "Dostęp do skrzynek pocztowych jako hello zalogowanego użytkownika".

Podczas definiowania uprawnień, hello Deweloper aplikacji musi definiować czy hello uprawnienia można zgodę na, czy wymaga zgody administratora. Dzięki temu deweloperzy tooallow tooconsent użytkowników na własnych tooapps żądanie tylko małej czułości uprawnień, ale wymagają administratorom tooconsent toomore poufnych uprawnienia. Na przykład Witaj aplikacji zasobu "Azure Active Directory", została zdefiniowana, dlatego użytkownicy mogą wyrazić zgodę tooapps, żądania z ograniczonymi uprawnieniami tylko do odczytu.  Jednak w przypadku pełnych uprawnień do odczytu i wszystkich uprawnień do zapisu jest wymagana zgoda administratora.

Ponieważ klienci natywni nie są uwierzytelniani, aplikacja zdefiniowana jako klient natywny może żądać jedynie uprawnień delegowanych. To znaczy, że w uzyskiwanie tokenu zawsze musi być zaangażowany rzeczywisty użytkownik. Podczas uzyskiwania tokenu dostępu aplikacje sieci Web i interfejsy API sieci Web (klienci poufni) zawsze muszą dokonywać uwierzytelniania za pomocą usługi Azure AD. Co oznacza mają również możliwość hello żąda uprawnienia tylko do aplikacji. Jeśli na przykład usługi zaplecza tooanother tooauthenticate wymaga jednej usługi zaplecza. Aplikacje żądające uprawnień dotyczących tylko aplikacji zawsze wymagają zgody administratora.

Podsumowując:



- Aplikacji (klienta) określają uprawnienia hello, które są niezbędne do innych aplikacji (zasoby).
- Aplikacja (zasobów) określają, jakie uprawnienia są uwidocznione tooother aplikacji (klienci).
- Uprawnienia mogą dotyczyć tylko aplikacji lub być uprawnieniami delegowanymi.
- Uprawnienia delegowane mogą być oznaczona jako wymagające zgody użytkownika lub wymagające zgody administratora.
- Aplikacja może zachowywać się jako klient (przez zadeklarowanie wymaga uprawnień tooa zasobów), jako zasób (przez zadeklarowanie uprawnienia, które udostępnia ona) lub obie.

## <a name="controls"></a>Kontrolki

Witaj poniżej znajduje się lista formantów inny administrator hello dostępne dla tego zachowania. Witaj, Administratorze przez formanty można uzyskać w portalu klasycznym hello na konfigurowanie hello katalogu.

![](media/active-directory-apps-permissions-consent/apps7.png)

W hello Azure portalu, w obszarze **zarządzanie**, **ustawienia użytkownika**.

![](media/active-directory-apps-permissions-consent/apps11.png)



- Można kontrolować, czy użytkownicy mogą wyrazić zgodę tooapps:

W portalu klasycznym hello, wybierz **użytkownicy mogą spowodować tooaccess uprawnienia aplikacji swoje dane.**
![](media/active-directory-apps-permissions-consent/apps8.png)

Hello portalu Azure, wybierz **użytkownicy mogą zezwolić aplikacji tooaccess swoje dane**.
![](media/active-directory-apps-permissions-consent/apps12.png)



- Można kontrolować, czy użytkownicy mogą zarejestrować swoje własne aplikacje BIZNESOWE pojedynczej dzierżawy: W klasycznym portalu wybierz hello **użytkownicy mogą dodawać zintegrowanych aplikacji.**
![](media/active-directory-apps-permissions-consent/apps9.png)

Hello portalu Azure, wybierz **użytkownicy mogą zezwolić aplikacji tooaccess swoje dane**.
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
>Nawet jeśli użytkownicy aplikacji biznesowych tooregister pojedynczej dzierżawy, istnieją limity toowhat mogą być rejestrowane.  
>Dotyczy to na przykład deweloperów, którzy nie są administratorami katalogów.
>
>- Z aplikacji z jedną dzierżawą użytkownicy nie mogą zrobić aplikacji z wieloma dzierżawami.
>- Podczas rejestrowania aplikacji biznesowych pojedynczej dzierżawy, użytkownicy nie może zażądać aplikacji tooother uprawnienia tylko do aplikacji.
>- Podczas rejestrowania aplikacji biznesowych pojedynczej dzierżawy, użytkownicy nie może zażądać aplikacji tooother delegowane uprawnienia, jeśli te uprawnienia Wymagaj zgody administratora.
>- Użytkownicy nie mogą podjąć tooapps zmiany, które nie są właścicielami.



- Można zdecydować, czy użytkownicy mogą samodzielnie dodawać wstępnie zintegrowane aplikacje korzystające z logowania jednokrotnego z użyciem hasła („magazynowania haseł”). ![](media/active-directory-apps-permissions-consent/apps10.png)



- Można zdecydować, w jakich warunkach jest możliwe uzyskanie dostępu do aplikacji (dostęp warunkowy). Należy pamiętać, że dotyczy to zarówno aplikacja klienta toohello i toohello zasobów aplikacji. Tak Załóżmy, że w ustawieniu zasad dostępu warunkowego, stwierdzający, że tej aplikacji "Office 365 usługi Exchange Online" hello jest możliwy tylko z komputerów, które są zgodne.  Ta zasada będzie również zaczną działać, gdy użytkownik próbuje toouse aplikacji klienckiej, która żąda uprawnienia tooExchange w trybie Online.



- Masz widoczność, w którym aplikacje zostały przyzwolenie tooand te, które są używane.

1.  Gdy użytkownik wyraża zgodę tooan aplikacji, tworzony jest obiekt ServicePrincipal w dzierżawie powitalnych. Tworzenie ServicePrincipal jest uwzględniona w raporcie inspekcji hello.
2.  Raporty dotyczące działań logowania użytkownika informujące użytkownika hello aplikacji, który loguje się do. 

## <a name="example"></a>Przykład

Na przykład Przyjrzyjmy aplikacji "FabrikamMail dla usługi Office 365" hello, która zaobserwowany się, że użytkownicy w Twojej dzierżawie się rejestruje. Aplikacja „FabrikamMail” to czytnik poczty e-mail dla systemu Android opublikowany przez firmę „Fabrikam, Inc.”. Znajduje się na powitania "aplikacje wielodostępne innych opracowanie, który Contoso można wyrazić zgodę na".

Jeśli użytkownicy mogą tooconsent, otrzymują zgody hello monitu o zalogowaniu po raz pierwszy:![](media/active-directory-apps-permissions-consent/apps14.png)

"Dostęp do skrzynek pocztowych" jest hello uwzględniającym działania użytkownika zgody ciąg uprawnienia "Dostęp do skrzynek pocztowych jako hello zalogowanego użytkownika" hello udostępnianych przez "Office 365 usługi Exchange Online" (czyli Exchange).

Widać uprawnienia hello wyszukując hello ServicePrincipal obiektu dla programu Exchange (hello zasobów), który zostało dodane po utworzeniu konta w usłudze Office 365. Obiekt ServicePrincipal hello "wystąpienia" hello aplikacji można traktować w dzierżawie, który służy do rejestrowania różnych opcjach i konfiguracji.  Zobacz ten przy użyciu hello `Get-AzureADServicePrincipal` w programie PowerShell.

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

Zgoda jest inicjowane, gdy hello użytkownik kliknie przycisk "Akceptuj". Najpierw tworzony jest obiekt ServicePrincipal dla "FabrikamMail dla usługi Office 365" w dzierżawie powitalnych. Witaj ServicePrincipal wygląda następująco:

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

Zgodę aplikacji tooan tworzy łącze Oauth2PermissionGrant hello następującego zakresu:
  
- Witaj obiektu użytkownika
- aplikacje klienta Hello ServicePrincipalName (SPN)
- aplikacje zasobów Hello ServicePrincipalName (SPN)
- uprawnienia w hello zasobów aplikacji.  

W przypadku hello FabrikamMail wygląda mniej więcej tak:

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

(**ClientId** jest identyfikator obiekt główny usługi przez FabrikamMail (hello, które utworzono właśnie), **PrincipalId** jest hello obiektu identyfikator użytkownika (hello użytkownika, który zgodę), **ResourceId**to usługa programu Exchange dla obiekt główny identyfikator zakresu jest hello uprawnień w programie Exchange, która została zgodę na).

Jeśli użytkownicy nie mogą tooconsent, zostanie wyświetlony ekran z informacją, że uprawnienie jest wymagane.

