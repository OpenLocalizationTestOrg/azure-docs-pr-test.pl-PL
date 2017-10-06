---
title: "aaaApplications i przeglądarki, które używały zasady dostępu warunkowego w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Z kontroli dostępu warunkowego usługi Azure Active Directory sprawdza określonych warunków podczas uwierzytelniania użytkownika hello i tooallow dostęp do aplikacji."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 62349fba-3cc0-4ab5-babe-372b3389eff6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ca20853bb9f4b22d0b88ddd2f051d658e0d88cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="applications-and-browsers-that-use-conditional-access-rules-in-azure-active-directory"></a>Aplikacje i przeglądarki, które używały zasady dostępu warunkowego w usłudze Azure Active Directory

Zasady dostępu warunkowego są obsługiwane w usłudze Azure Active Directory (Azure AD)-połączony wniosków, wstępnie zintegrowane federacyjnych oprogramowanie jako usługa (SaaS), aplikacje używające hasło rejestracji jednokrotnej (SSO), aplikacji biznesowych z i aplikacje, które używają serwera Proxy aplikacji usługi Azure AD. Aby uzyskać szczegółową listę aplikacji, dla których można użyć dostępu warunkowego, zobacz [włączyć usługi z dostępem warunkowym](active-directory-conditional-access-technical-reference.md). Dostęp warunkowy działa zarówno z aplikacji mobilnych i klasycznych, które używają nowoczesnego uwierzytelniania. W tym artykule opisano firma Microsoft, sposobie działania dostępu warunkowego w aplikacji mobilnych i klasycznych.

W aplikacjach korzystających z nowoczesnego uwierzytelniania, można użyć strony logowania usługi Azure AD. Ze strony logowania użytkownik jest monitowany w usłudze Multi-Factor authentication. Komunikat jest wyświetlany, jeśli użytkownik hello dostęp będzie zablokowany. Nowoczesnego uwierzytelniania jest wymagany dla hello tooauthenticate urządzenia z usługą Azure AD, dzięki czemu są analizowane zasady dostępu warunkowego opartego na urządzeniu.

Jest ważne tooknow aplikacji, które można użyć zasad dostępu warunkowego i hello kroki mogą konieczność tootake toosecure inne punkty wejścia aplikacji.

## <a name="applications-that-use-modern-authentication"></a>Aplikacje używające nowoczesnego uwierzytelniania
> [!NOTE]
> Jeśli zasady dostępu warunkowego w usłudze Azure AD, która zawiera odpowiednika w usłudze Office 365, należy skonfigurować obie zasady dostępu warunkowego. Ma to zastosowanie, na przykład tooconditional zasady dostępu dla usługi Exchange Online lub SharePoint Online.
>
>

Witaj następujące aplikacje obsługują dostępu warunkowego dla usługi Office 365 i innych aplikacji usługi Azure AD, połączony:


| Usługa docelowa| Platforma| Aplikacja |
| --- | --- | --- |
| Moje aplikacje usługi aplikacji| Android i iOS| Zasady MFA i lokalizację dla aplikacji. Urządzenia, na podstawie zasad nie są obsługiwane.|
| Usługa Azure RemoteApp| Windows 10, Windows 8.1, Windows 7, iOS, Android i Mac OS X| Usługa Azure RemoteApp|
| Dynamics CRM| Windows 10, Windows 8.1, Windows 7, iOS i Android| Aplikacji programu Dynamics CRM|
| Microsoft Teams| Windows 10, Windows 8.1, Windows 7, Android/z systemem iOS i MAC OS x| Usługi zespoły firmy Microsoft — kontroluje do wszystkich usług, które obsługują Teams firmy Microsoft i jej aplikacji klienta - pulpitu systemu Windows, MAC OS X, iOS, Android, WP i klienta sieci web|
| Office 365 Exchange Online| Windows 10| Osoby-mail/kalendarza aplikacji Outlook 2016, Outlook 2013 (z nowoczesnego uwierzytelniania), usługi Skype dla firm (z nowoczesnego uwierzytelniania)|
| Office 365 Exchange Online| Windows 8.1, Windows 7| Outlook 2016, Outlook 2013 (z nowoczesnego uwierzytelniania), usługi Skype dla firm (z nowoczesnego uwierzytelniania)|
| Office 365 Exchange Online| iOS| Outlook aplikacji mobilnej|
| Office 365 Exchange Online| Mac OS X| Outlook 2016 (Urząd macOS)|
| Usługi Office 365 SharePoint Online| Windows 10| Aplikacje pakietu Office 2016, Office uniwersalnych aplikacji, Office 2013 (z nowoczesnego uwierzytelniania), klient synchronizacji usługi OneDrive (zobacz [uwagi](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e)), zaplanowane dla przyszłych hello Obsługa grupy usługi Office, obsługi aplikacji programu SharePoint zaplanowane dla przyszłych hello|
| Usługi Office 365 SharePoint Online| Windows 8.1, Windows 7| Aplikacje pakietu Office 2016, Office 2013 (z nowoczesnego uwierzytelniania), usługi OneDrive Synchronizowanie klienta (zobacz [uwagi](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))|
| Usługi Office 365 SharePoint Online| iOS i Android| Aplikacje mobilne pakietu Office|
| Usługi Office 365 SharePoint Online| Mac OS X| Pakiet Office 2016 dla macOS (Word, Excel, PowerPoint, tylko w programie OneNote). OneDrive dla firm Obsługa planowanych do przyszłych hello|
| Yammer usługi Office 365| Windows 10, iOS, Android| Aplikacja usługi Yammer pakietu Office|
| Usługa Power BI| Windows 10, Windows 8.1, Windows 7 i iOS| Aplikacja usługi Power BI. Witaj aplikacji Power BI dla systemu Android nie obsługuje obecnie dostępu warunkowego opartego na urządzeniu.|
| Visual Studio Team Services| Windows 10, Windows 8.1, Windows 7, iOS i Android| Visual Studio Team Services aplikacji|








## <a name="applications-that-do-not-use-modern-authentication"></a>Aplikacje, które nie używają nowoczesnego uwierzytelniania
Obecnie należy użyć innych tooapps dostępu tooblock metod nie używają nowoczesnego uwierzytelniania. Reguły dostępu dla aplikacji używających nowoczesnego uwierzytelniania nie są wymuszane przez funkcję dostępu warunkowego. Jest to przede wszystkim jest brany pod uwagę, aby uzyskać dostęp do programu Exchange i SharePoint. Większość wcześniejszych wersji aplikacji użyj starszych protokołów kontroli dostępu.

### <a name="control-access-in-office-365-sharepoint-online"></a>Kontroli dostępu w usłudze SharePoint Online pakietu Office 365
Starszy protokół do dostępu do programu SharePoint można wyłączyć za pomocą polecenia cmdlet hello SPOTenant zestawu. Użyj tego polecenia cmdlet tooprevent Office klientów, którzy używają nienowoczesne protokoły dostęp do zasobów usługi SharePoint Online.

**Przykładowe polecenie**:`Set-SPOTenant -LegacyAuthProtocolsEnabled $false`

### <a name="control-access-in-office-365-exchange-online"></a>Kontrola dostępu w usłudze Exchange Online pakietu Office 365
Exchange oferuje dwie główne kategorie protokołów. Przejrzyj hello następujące opcje, a następnie wybierz hello zasad, które jest odpowiednie dla Twojej organizacji.

* **Program Exchange ActiveSync**. Domyślnie zasady dostępu warunkowego dla usługi Multi-Factor authentication i lokalizacji nie są wymuszane dla programu Exchange ActiveSync. Należy tooprotect dostępu toothese usług, konfigurując zasady programu Exchange ActiveSync bezpośrednio lub przez blokowanie programu Exchange ActiveSync przy użyciu reguł usługi Active Directory Federation Services (AD FS).
* **Starszy protokół**. Możesz zablokować starszych protokołów z usługami AD FS. To blokuje dostęp tooolder Office klientów, takich jak pakiet Office 2013 bez nowoczesnego uwierzytelniania, włączona i starszych wersji pakietu Office.

### <a name="use-ad-fs-tooblock-legacy-protocol"></a>Używanie protokołu starszych tooblock usług AD FS
Możesz użyć powitania po przykład wystawiania autoryzacji reguły tooblock starsza wersja protokołu dostęp na poziomie hello usług AD FS. Wybierz spośród dwóch typowych konfiguracji.

#### <a name="option-1-allow-exchange-activesync-and-allow-legacy-apps-but-only-on-hello-intranet"></a>Opcja 1: Zezwalaj na program Exchange ActiveSync i Zezwalaj aplikacjom starszej wersji, ale tylko w intranecie hello
Stosując następujące trzy toohello reguły hello jednostki zależnej w usługach AD FS zaufania dla platformą tożsamości Microsoft Office 365, ruch protokołu Exchange ActiveSync i przeglądarki i ruchu nowoczesnego uwierzytelniania dostęp. Starsze aplikacje są blokowane hello ekstranetu.

##### <a name="rule-1"></a>Reguła 1
    @RuleName = "Allow all intranet traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-2"></a>Reguła 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-3"></a>Reguła 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

#### <a name="option-2-allow-exchange-activesync-and-block-legacy-apps"></a>Opcja 2: Zezwalaj na program Exchange ActiveSync i blokowania starsze aplikacje
Stosując następujące trzy toohello reguły hello jednostki zależnej w usługach AD FS zaufania dla platformą tożsamości Microsoft Office 365, ruch protokołu Exchange ActiveSync i przeglądarki i ruchu nowoczesnego uwierzytelniania dostęp. Starsze aplikacje są zablokowane z dowolnego miejsca.

##### <a name="rule-1"></a>Reguła 1
    @RuleName = "Allow all intranet traffic only for browser and modern authentication clients"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-2"></a>Reguła 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-3"></a>Reguła 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


## <a name="supported-browsers-for-device-based-policies"></a>Obsługiwane przeglądarki dla urządzeń, na podstawie zasad 

Tylko można uzyskać dostępu do urządzenia, na podstawie zasad, które Sprawdź zgodności urządzenia i przyłączanie do domeny po usługi Azure AD można identyfikację i uwierzytelnienie hello urządzenia. Podczas kontroli większości, takie jak lokalizacja i pracy uwierzytelniania Wieloskładnikowego na większości urządzeń i przeglądarki zasady urządzeń wymagają wersji hello systemu operacyjnego i przeglądarek wymienionych poniżej. Dostęp będzie zablokowany dla użytkowników w nieobsługiwanych przeglądarkach hello systemach operacyjnych czy w przypadku zasad urządzenia w miejscu. 

| System operacyjny                     | Przeglądarki                 | Pomoc techniczna     |
| :--                    | :--                      | :-:         |
| Windows 10                 | IE krawędzi                 | ![Zaznacz][1] |
| Windows 10                 | Chrome                   | Wersja zapoznawcza     |
| Windows 8 / 8.1            | IE Chrome               | ![Zaznacz][1] |
| Windows 7                  | IE Chrome               | ![Zaznacz][1] |
| iOS                    | Safari                   | ![Zaznacz][1] |
| Android                | Chrome                   | ![Zaznacz][1] |
| Windows Phone          | IE krawędzi                 | ![Zaznacz][1] |
| Windows Server 2016    | IE krawędzi                 | ![Zaznacz][1] |
| Windows Server 2016    | Chrome                   | Wkrótce |
| Windows Server 2012 R2 | IE Chrome               | ![Zaznacz][1] |
| Windows Server 2008 R2 | IE Chrome               | ![Zaznacz][1] |
| Mac OS                 | Safari                   | ![Zaznacz][1] |
| Mac OS                 | Chrome                   | Wkrótce |

> [!NOTE]
> Obsługę Chrome, należy korzystać z systemu Windows 10 twórców aktualizacji i instalacji rozszerzenia hello znaleziono [tutaj](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji).
>
>

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji, zobacz [dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access.md)




<!--Image references-->
[1]: ./media/active-directory-conditional-access-supported-apps/ic195031.png


