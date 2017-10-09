---
title: "Atrybuty są synchronizowane przy użyciu usługi Azure AD Connect | Dokumentacja firmy Microsoft"
description: "Atrybuty hello list, które są synchronizowane tooAzure usługi Active Directory."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c2bb36e0-5205-454c-b9b6-f4990bcedf51
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 2fe5b944a7fc832f245631416c265fb82eedeb15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-attributes-synchronized-tooazure-active-directory"></a>Synchronizacja programu Azure AD Connect: atrybuty synchronizowane tooAzure usługi Active Directory
W tym temacie wymieniono hello atrybuty, które są synchronizowane przez synchronizacja programu Azure AD Connect.  
Hello atrybuty są pogrupowane według hello powiązanych aplikacji usługi Azure AD.

## <a name="attributes-toosynchronize"></a>Atrybuty toosynchronize
Często zadawane pytania jest *co to jest lista hello toosynchronize atrybuty minimalnej*. Witaj domyślnym i zalecanym podejściem jest tookeep hello domyślne atrybuty, pełne usługi GAL (globalna lista adresów) może być skonstruowany w hello chmury i tooget wszystkich funkcji w zadaniami usługi Office 365. W niektórych przypadkach są niektóre atrybuty, że organizacji nie być zsynchronizowane toohello chmury zawierać te atrybuty poufnych lub dane osobowe () danych osobowych, takich jak w tym przykładzie:  
![Złe atrybuty](./media/active-directory-aadconnectsync-attributes-synchronized/badextensionattribute.png)

W takim przypadku rozpoczynać hello listę atrybutów, w tym temacie i zidentyfikować te atrybuty, które może zawierać wrażliwe lub dane osobowe danych i nie można zsynchronizować. Usuń zaznaczenie opcji te atrybuty podczas instalacji, używając [filtrowanie atrybutów i aplikacji usługi Azure AD](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering).

> [!WARNING]
> W przypadku zaznaczenia atrybuty, należy należy zachować ostrożność i tylko Anuluj wybór tych atrybutów toosynchronize absolutnie nie jest możliwe. Inne atrybuty unselecting może mieć negatywny wpływ na funkcje.
>
>

## <a name="office-365-proplus"></a>Usługi Office 365 ProPlus
| Nazwa atrybutu | Użytkownik | Komentarz |
| --- |:---:| --- |
| AccountEnabled |X |Określa, czy konto jest włączone. |
| Nazwa pospolita |X | |
| Nazwa wyświetlana |X | |
| objectSID |X |tych właściwości. Identyfikator użytkownika AD używane toomaintain synchronizacji między Azure AD i usługi AD. |
| pwdLastSet |X |tych właściwości. Używane tooknow tooinvalidate już wystawionych tokenów. Używana przez synchronizacji haseł i federacji. |
| sourceAnchor |X |tych właściwości. Identyfikator niezmienne toomaintain relacja między DODAJE i Azure AD. |
| usageLocation |X |tych właściwości. kraj Hello użytkownika. Używany do przypisywania licencji. |
| userPrincipalName |X |Nazwa UPN jest hello Identyfikatora logowania dla użytkownika hello. W większości przypadków hello taka sama jak wartość [poczty]. |

## <a name="exchange-online"></a>Exchange Online
| Nazwa atrybutu | Użytkownik | Kontakt | Grupa | Komentarz |
| --- |:---:|:---:|:---:| --- |
| AccountEnabled |X | | |Określa, czy konto jest włączone. |
| Asystent |X |X | | |
| altRecipient |X | | |Wymaga usługi Azure AD Connect kompilacji 1.1.552.0 lub po. |
| authOrig |X |X |X | |
| C |X |X | | |
| Nazwa pospolita |X | |X | |
| co |X |X | | |
| Firmy |X |X | | |
| CountryCode |X |X | | |
| Dział |X |X | | |
| description |X |X |X | |
| Nazwa wyświetlana |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| Imię |X |X | | |
| HomePhone |X |X | | |
| Informacje o |X |X |X |Ten atrybut nie jest aktualnie używane dla grup. |
| Inicjały |X |X | | |
| l |X |X | | |
| LegacyExchangeDN |X |X |X | |
| mailNickname |X |X |X | |
| mangedBy | | |X | |
| Menedżer |X |X | | |
| Element członkowski | | |X | |
| Telefon komórkowy |X |X | | |
| atrybut msDS-HABSeniorityIndex |X |X |X | |
| atrybut msDS-PhoneticDisplayName |X |X |X | |
| msExchArchiveGUID |X | | | |
| msExchArchiveName |X | | | |
| msExchAssistantName |X |X | | |
| msExchAuditAdmin |X | | | |
| msExchAuditDelegate |X | | | |
| msExchAuditDelegateAdmin |X | | | |
| msExchAuditOwner |X | | | |
| msExchBlockedSendersHash |X |X | | |
| msExchBypassAudit |X | | | |
| msExchBypassModerationLink | | |X |Dostępne w programie Azure AD Connect wersji 1.1.524.0 |
| msExchCoManagedByLink | | |X | |
| msExchDelegateListLink |X | | | |
| msExchELCExpirySuspensionEnd |X | | | |
| msExchELCExpirySuspensionStart |X | | | |
| msExchELCMailboxFlags |X | | | |
| msExchEnableModeration |X | |X | |
| msExchExtensionCustomAttribute1 |X |X |X |Ten atrybut nie jest aktualnie używane przez usługę Exchange Online. |
| msExchExtensionCustomAttribute2 |X |X |X |Ten atrybut nie jest aktualnie używane przez usługę Exchange Online. |
| msExchExtensionCustomAttribute3 |X |X |X |Ten atrybut nie jest aktualnie używane przez usługę Exchange Online. |
| msExchExtensionCustomAttribute4 |X |X |X |Ten atrybut nie jest aktualnie używane przez usługę Exchange Online. |
| msExchExtensionCustomAttribute5 |X |X |X |Ten atrybut nie jest aktualnie używane przez usługę Exchange Online. |
| msExchHideFromAddressLists |X |X |X | |
| msExchImmutableID |X | | | |
| msExchLitigationHoldDate |X |X |X | |
| msExchLitigationHoldOwner |X |X |X | |
| msExchMailboxAuditEnable |X | | | |
| msExchMailboxAuditLogAgeLimit |X | | | |
| msExchMailboxGuid |X | | | |
| msExchModeratedByLink |X |X |X | |
| msExchModerationFlags |X |X |X | |
| msExchRecipientDisplayType |X |X |X | |
| msExchRecipientTypeDetails |X |X |X | |
| msExchRemoteRecipientType |X | | | |
| msExchRequireAuthToSendTo |X |X |X | |
| msExchResourceCapacity |X | | | |
| msExchResourceDisplay |X | | | |
| msExchResourceMetaData |X | | | |
| msExchResourceSearchProperties |X | | | |
| msExchRetentionComment |X |X |X | |
| msExchRetentionURL |X |X |X | |
| msExchSafeRecipientsHash |X |X | | |
| msExchSafeSendersHash |X |X | | |
| msExchSenderHintTranslations |X |X |X | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| msExchUserHoldPolicies |X | | | |
| msOrg IsOrganizational | | |X | |
| objectSID |X | |X |tych właściwości. Identyfikator użytkownika AD używane toomaintain synchronizacji między Azure AD i usługi AD. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherTelephone |X |X | | |
| Pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| KodPocztowy |X |X | | |
| proxyAddresses |X |X |X | |
| publicDelegates |X |X |X | |
| pwdLastSet |X | | |tych właściwości. Używane tooknow tooinvalidate już wystawionych tokenów. Używana przez synchronizacji haseł i federacji. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| Securityenabled musi | | |X |Pochodne groupType |
| SN |X |X | | |
| sourceAnchor |X |X |X |tych właściwości. Identyfikator niezmienne toomaintain relacja między DODAJE i Azure AD. |
| St |X |X | | |
| Adres |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| TelephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| Tytuł |X |X | | |
| unauthOrig |X |X |X | |
| usageLocation |X | | |tych właściwości. kraj Hello użytkownika. Używany do przypisywania licencji. |
| userCertificate |X |X | | |
| userPrincipalName |X | | |Nazwa UPN jest hello Identyfikatora logowania dla użytkownika hello. W większości przypadków hello taka sama jak wartość [poczty]. |
| userSMIMECertificates |X |X | | |
| wWWHomePage |X |X | | |

## <a name="sharepoint-online"></a>SharePoint Online
| Nazwa atrybutu | Użytkownik | Kontakt | Grupa | Komentarz |
| --- |:---:|:---:|:---:| --- |
| AccountEnabled |X | | |Określa, czy konto jest włączone. |
| authOrig |X |X |X | |
| C |X |X | | |
| Nazwa pospolita |X | |X | |
| co |X |X | | |
| Firmy |X |X | | |
| CountryCode |X |X | | |
| Dział |X |X | | |
| description |X |X |X | |
| Nazwa wyświetlana |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| Imię |X |X | | |
| hideDLMembership | | |X | |
| homephone |X |X | | |
| Informacje o |X |X |X | |
| Inicjały |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| Poczty |X |X |X | |
| mailnickname |X |X |X | |
| Zarządzane | | |X | |
| Menedżer |X |X | | |
| Element członkowski | | |X | |
| middleName |X |X | | |
| Telefon komórkowy |X |X | | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointLinkedBy |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| objectSID |X | |X |tych właściwości. Identyfikator użytkownika AD używane toomaintain synchronizacji między Azure AD i usługi AD. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherIpPhone |X |X | | |
| OtherMobile |X |X | | |
| otherPager |X |X | | |
| otherTelephone |X |X | | |
| Pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| KodPocztowy |X |X | | |
| postOfficeBox |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |tych właściwości. Używane tooknow tooinvalidate już wystawionych tokenów. Używana przez synchronizacji haseł i federacji. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| Securityenabled musi | | |X |Pochodne groupType |
| SN |X |X | | |
| sourceAnchor |X |X |X |tych właściwości. Identyfikator niezmienne toomaintain relacja między DODAJE i Azure AD. |
| St |X |X | | |
| Adres |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| TelephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| Tytuł |X |X | | |
| unauthOrig |X |X |X | |
| adres URL |X |X | | |
| usageLocation |X | | |tych właściwości. kraj Hello użytkownika. Używany do przypisywania licencji. |
| userPrincipalName |X | | |Nazwa UPN jest hello Identyfikatora logowania dla użytkownika hello. W większości przypadków hello taka sama jak wartość [poczty]. |
| wWWHomePage |X |X | | |

## <a name="lync-online"></a>Lync Online
| Nazwa atrybutu | Użytkownik | Kontakt | Grupa | Komentarz |
| --- |:---:|:---:|:---:| --- |
| AccountEnabled |X | | |Określa, czy konto jest włączone. |
| C |X |X | | |
| Nazwa pospolita |X | |X | |
| co |X |X | | |
| Firmy |X |X | | |
| Dział |X |X | | |
| description |X |X |X | |
| Nazwa wyświetlana |X |X |X | |
| facsimiletelephonenumber |X |X |X | |
| Imię |X |X | | |
| homephone |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| Poczty |X |X |X | |
| mailNickname |X |X |X | |
| Zarządzane | | |X | |
| Menedżer |X |X | | |
| Element członkowski | | |X | |
| Telefon komórkowy |X |X | | |
| msExchHideFromAddressLists |X |X |X | |
| msRTCSIP-ApplicationOptions |X | | | |
| msRTCSIP-DeploymentLocator |X |X | | |
| msRTCSIP-Line. |X |X | | |
| msRTCSIP-OptionFlags |X |X | | |
| msRTCSIP-OwnerUrn |X | | | |
| msRTCSIP-PrimaryUserAddress |X |X | | |
| msRTCSIP-UserEnabled |X |X | | |
| objectSID |X | |X |tych właściwości. Identyfikator użytkownika AD używane toomaintain synchronizacji między Azure AD i usługi AD. |
| otherTelephone |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| KodPocztowy |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |tych właściwości. Używane tooknow tooinvalidate już wystawionych tokenów. Używana przez synchronizacji haseł i federacji. |
| Securityenabled musi | | |X |Pochodne groupType |
| SN |X |X | | |
| sourceAnchor |X |X |X |tych właściwości. Identyfikator niezmienne toomaintain relacja między DODAJE i Azure AD. |
| St |X |X | | |
| Adres |X |X | | |
| TelephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| Tytuł |X |X | | |
| usageLocation |X | | |tych właściwości. kraj Hello użytkownika. Używany do przypisywania licencji. |
| userPrincipalName |X | | |Nazwa UPN jest hello Identyfikatora logowania dla użytkownika hello. W większości przypadków hello taka sama jak wartość [poczty]. |
| wWWHomePage |X |X | | |

## <a name="azure-rms"></a>Usługa Azure RMS
| Nazwa atrybutu | Użytkownik | Kontakt | Grupa | Komentarz |
| --- |:---:|:---:|:---:| --- |
| AccountEnabled |X | | |Określa, czy konto jest włączone. |
| Nazwa pospolita |X | |X |Typowe nazwy ani aliasu. W większości przypadków hello prefiks wartość [poczty]. |
| Nazwa wyświetlana |X |X |X |Ciąg, który reprezentuje nazwę hello często są wyświetlane jako hello przyjazną nazwisko (imię). |
| Poczty |X |X |X |pełny adres e-mail. |
| Element członkowski | | |X | |
| objectSID |X | |X |tych właściwości. Identyfikator użytkownika AD używane toomaintain synchronizacji między Azure AD i usługi AD. |
| proxyAddresses |X |X |X |tych właściwości. Używane przez usługę Azure AD. Zawiera wszystkie adresy e-mail dodatkowej hello użytkownika. |
| pwdLastSet |X | | |tych właściwości. Używane tooknow tooinvalidate już wystawionych tokenów. |
| Securityenabled musi | | |X |Pochodne groupType. |
| sourceAnchor |X |X |X |tych właściwości. Identyfikator niezmienne toomaintain relacja między DODAJE i Azure AD. |
| usageLocation |X | | |tych właściwości. kraj Hello użytkownika. Używany do przypisywania licencji. |
| userPrincipalName |X | | |Ta nazwa UPN jest hello Identyfikatora logowania dla użytkownika hello. W większości przypadków hello taka sama jak wartość [poczty]. |

## <a name="intune"></a>Usługi Intune
| Nazwa atrybutu | Użytkownik | Kontakt | Grupa | Komentarz |
| --- |:---:|:---:|:---:| --- |
| AccountEnabled |X | | |Określa, czy konto jest włączone. |
| C |X |X | | |
| Nazwa pospolita |X | |X | |
| description |X |X |X | |
| Nazwa wyświetlana |X |X |X | |
| Poczty |X |X |X | |
| mailnickname |X |X |X | |
| Element członkowski | | |X | |
| objectSID |X | |X |tych właściwości. Identyfikator użytkownika AD używane toomaintain synchronizacji między Azure AD i usługi AD. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |tych właściwości. Używane tooknow tooinvalidate już wystawionych tokenów. Używana przez synchronizacji haseł i federacji. |
| Securityenabled musi | | |X |Pochodne groupType |
| sourceAnchor |X |X |X |tych właściwości. Identyfikator niezmienne toomaintain relacja między DODAJE i Azure AD. |
| usageLocation |X | | |tych właściwości. kraj Hello użytkownika. Używany do przypisywania licencji. |
| userPrincipalName |X | | |Nazwa UPN jest hello Identyfikatora logowania dla użytkownika hello. W większości przypadków hello taka sama jak wartość [poczty]. |

## <a name="dynamics-crm"></a>Dynamics CRM
| Nazwa atrybutu | Użytkownik | Kontakt | Grupa | Komentarz |
| --- |:---:|:---:|:---:| --- |
| AccountEnabled |X | | |Określa, czy konto jest włączone. |
| C |X |X | | |
| Nazwa pospolita |X | |X | |
| co |X |X | | |
| Firmy |X |X | | |
| CountryCode |X |X | | |
| description |X |X |X | |
| Nazwa wyświetlana |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| Imię |X |X | | |
| l |X |X | | |
| Zarządzane | | |X | |
| Menedżer |X |X | | |
| Element członkowski | | |X | |
| Telefon komórkowy |X |X | | |
| objectSID |X | |X |tych właściwości. Identyfikator użytkownika AD używane toomaintain synchronizacji między Azure AD i usługi AD. |
| physicalDeliveryOfficeName |X |X | | |
| KodPocztowy |X |X | | |
| preferredLanguage |X | | | |
| pwdLastSet |X | | |tych właściwości. Używane tooknow tooinvalidate już wystawionych tokenów. Używana przez synchronizacji haseł i federacji. |
| Securityenabled musi | | |X |Pochodne groupType |
| SN |X |X | | |
| sourceAnchor |X |X |X |tych właściwości. Identyfikator niezmienne toomaintain relacja między DODAJE i Azure AD. |
| St |X |X | | |
| Adres |X |X | | |
| TelephoneNumber |X |X | | |
| Tytuł |X |X | | |
| usageLocation |X | | |tych właściwości. kraj Hello użytkownika. Używany do przypisywania licencji. |
| userPrincipalName |X | | |Nazwa UPN jest hello Identyfikatora logowania dla użytkownika hello. W większości przypadków hello taka sama jak wartość [poczty]. |

## <a name="3rd-party-applications"></a>aplikacje firm 3
Ta grupa jest zestaw atrybutów używany jako hello atrybuty minimalne wymagane dla ogólnego obciążenia lub aplikacji. Można użyć, dla obciążenia niewymienionych w innej sekcji lub aplikacji firmy Microsoft. Jawnie służy do następujących hello:

* Yammer (używane tylko użytkownika)
* [Oferowane przez zasoby hybrydowego między firmami (B2B) całej organizacji współpracy scenariuszy, takich jak SharePoint](http://go.microsoft.com/fwlink/?LinkId=747036)

Ta grupa jest zestaw atrybutów, które mogą być używane, jeśli katalog usługi Azure AD hello jest używany toosupport usługi Office 365, Dynamics lub usługi Intune. Ma niewielki zestaw Podstawowe atrybuty.

| Nazwa atrybutu | Użytkownik | Kontakt | Grupa | Komentarz |
| --- |:---:|:---:|:---:| --- |
| AccountEnabled |X | | |Określa, czy konto jest włączone. |
| Nazwa pospolita |X | |X | |
| Nazwa wyświetlana |X |X |X | |
| Imię |X |X | | |
| Poczty |X | |X | |
| Zarządzane | | |X | |
| mailNickName |X |X |X | |
| Element członkowski | | |X | |
| objectSID |X | | |tych właściwości. Identyfikator użytkownika AD używane toomaintain synchronizacji między Azure AD i usługi AD. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |tych właściwości. Używane tooknow tooinvalidate już wystawionych tokenów. Używana przez synchronizacji haseł i federacji. |
| SN |X |X | | |
| sourceAnchor |X |X |X |tych właściwości. Identyfikator niezmienne toomaintain relacja między DODAJE i Azure AD. |
| usageLocation |X | | |tych właściwości. kraj Hello użytkownika. Używany do przypisywania licencji. |
| userPrincipalName |X | | |Nazwa UPN jest hello Identyfikatora logowania dla użytkownika hello. W większości przypadków hello taka sama jak wartość [poczty]. |

## <a name="windows-10"></a>Windows 10
Windows 10 przyłączonych do domeny computer(device) synchronizuje tooAzure niektóre atrybuty AD. Aby uzyskać więcej informacji na temat scenariuszy hello, zobacz [połączyć tooAzure urządzeń przyłączonych do domeny AD dla systemu Windows 10 napotyka](../active-directory-azureadjoin-devices-group-policy.md). Te atrybuty zawsze synchronizacji i Windows 10 nie będzie wyświetlane w aplikacji, które możesz usunąć zaznaczenie. Windows 10 przyłączonych do domeny komputera jest identyfikowany przez o userCertificate atrybutu hello wypełnione.

| Nazwa atrybutu | Urządzenie | Komentarz |
| --- |:---:| --- |
| AccountEnabled |X | |
| deviceTrustType |X |Wartość zapisane na stałe dla komputerów przyłączonych do domeny. |
| Nazwa wyświetlana |X | |
| MS-DS-CreatorSID |X |Skrót registeredOwnerReference. |
| Atrybut objectGUID |X |Skrót deviceID. |
| objectSID |X |Skrót onPremisesSecurityIdentifier. |
| system operacyjny |X |Skrót deviceOSType. |
| operatingSystemVersion |X |Skrót deviceOSVersion. |
| userCertificate |X | |

Te atrybuty **użytkownika** dodatkowo toohello inne aplikacje nie są wybrane.  

| Nazwa atrybutu | Użytkownik | Komentarz |
| --- |:---:| --- |
| domainFQDN |X |Skrót NazwaDomenyDNS. Na przykład contoso.com. |
| domainNetBios |X |Skrót netBiosName. Na przykład CONTOSO. |

## <a name="exchange-hybrid-writeback"></a>Zapisywanie zwrotne hybrydowego programu Exchange
Te atrybuty są zapisywane z usługi Azure AD tooon lokalnej usługi Active Directory po wybraniu tooenable **hybrydowym programu Exchange**. W zależności od używanej wersji programu Exchange mogą być synchronizowani mniej atrybutów.

| Nazwa atrybutu | Użytkownik | Kontakt | Grupa | Komentarz |
| --- |:---:|:---:|:---:| --- |
| atrybut msDS-identyfikatora ExternalDirectoryObjectID |X | | |Pochodną cloudAnchor w usłudze Azure AD. Ten atrybut jest nowa w programie Exchange 2016 i Windows Server 2016 AD. |
| msExchArchiveStatus |X | | |Archiwum online: Umożliwia klientom tooarchive poczty. |
| msExchBlockedSendersHash |X | | |Filtrowanie: Zapisuje ponownie filtrowania lokalne i dane online nadawcy bezpieczne i zablokowane od klientów. |
| msExchSafeRecipientsHash |X | | |Filtrowanie: Zapisuje ponownie filtrowania lokalne i dane online nadawcy bezpieczne i zablokowane od klientów. |
| msExchSafeSendersHash |X | | |Filtrowanie: Zapisuje ponownie filtrowania lokalne i dane online nadawcy bezpieczne i zablokowane od klientów. |
| msExchUCVoiceMailSettings |X | | |Włącz Unified Messaging (UM) — Poczta głosowa Online: używane przez program Microsoft Lync Server integracji tooindicate tooLync serwera lokalnego, które użytkownik hello ma poczty głosowej w usługach online. |
| msExchUserHoldPolicies |X | | |Wstrzymanie postępowań: Umożliwia toodetermine usługi chmury, której użytkownicy są w ramach postępowań przechowywania. |
| proxyAddresses |X |X |X |Dodaje się tylko hello x500 adres w usłudze Exchange Online. |
| publicDelegates |X | | |Umożliwia usłudze Exchange Online toobe skrzynki pocztowej, którym przyznano toousers prawa SendOnBehalfTo z lokalnymi skrzynek pocztowych programu Exchange. Wymaga usługi Azure AD Connect kompilacji 1.1.552.0 lub po. |

## <a name="exchange-mail-public-folder"></a>Folder publiczny poczty programu Exchange
Te atrybuty są synchronizowane z lokalnej usługi Active Directory tooAzure AD po wybraniu tooenable **folderu publicznego poczty programu Exchange**.

| Nazwa atrybutu | PublicFolder | Komentarz |
| --- | :---:| --- |
| Nazwa wyświetlana | X |  |
| Poczty | X |  |
| msExchRecipientTypeDetails | X |  |
| Atrybut objectGUID | X |  |
| proxyAddresses | X |  |
| targetAddress | X |  |

## <a name="device-writeback"></a>Zapisywanie zwrotne urządzeń
Obiekty urządzeń są tworzone w usłudze Active Directory. Obiekty te mogą znajdować się, że urządzenia przyłączone tooAzure AD lub komputerów przyłączonych do domeny systemu Windows 10.

| Nazwa atrybutu | Urządzenie | Komentarz |
| --- |:---:| --- |
| altSecurityIdentities |X | |
| Nazwa wyświetlana |X | |
| Nazwa wyróżniająca |X | |
| atrybut msDS-CloudAnchor |X | |
| atrybut msDS-DeviceID |X | |
| atrybut msDS-DeviceObjectVersion |X | |
| atrybut msDS-DeviceOSType |X | |
| atrybut msDS-DeviceOSVersion |X | |
| atrybut msDS-DevicePhysicalIDs |X | |
| atrybut msDS-KeyCredentialLink |X |Tylko ze schematem systemu Windows Server 2016 AD |
| atrybut msDS-IsCompliant |X | |
| atrybut msDS-IsEnabled |X | |
| atrybut msDS-IsManaged |X | |
| atrybut msDS-RegisteredOwner |X | |

## <a name="notes"></a>Uwagi
* Podczas korzystanie z alternatywnego Identyfikatora hello lokalnymi atrybut userPrincipalName jest synchronizowany z hello Azure AD atrybutu onPremisesUserPrincipalName. Witaj atrybutu alternatywnego Identyfikatora, na przykład poczty, jest zsynchronizowany z hello Azure AD atrybut userPrincipalName.
* W przypadku list hello powyżej hello typ obiektu **użytkownika** ma również zastosowanie typu obiektu toohello **iNetOrgPerson**.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.

Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
