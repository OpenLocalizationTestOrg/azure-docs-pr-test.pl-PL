---
title: "uwierzytelnianie oparte na certyfikatach pakietu aaaAzure usługi Active Directory w systemie iOS | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello obsługiwane scenariusze i hello wymagania dotyczące konfigurowania uwierzytelniania opartego na certyfikatach w rozwiązaniach z urządzeń z systemem iOS"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: 26a6fc54-0153-44fb-b970-9b432c99e9f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 4486ff5239c2897b3bc187053f31d74807430301
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a>Azure Active Directory na podstawie certyfikatu uwierzytelniania w systemie iOS

Uwierzytelnianie oparte na certyfikatach (CBA) umożliwia toobe uwierzytelniony przez usługę Azure Active Directory przy użyciu certyfikatu klienta na urządzeniu z systemem Windows, Android lub iOS podczas łączenia Twoje konto programu Exchange online: 

* Aplikacje mobilne pakietu Office, takich jak Microsoft Outlook i Microsoft Word   
* Klienci programu Exchange ActiveSync (EAS) 

Konfigurowanie tej funkcji eliminuje hello potrzeby tooenter nazwę użytkownika i kombinacja hasła do niektórych poczty i aplikacje Microsoft Office na urządzeniu przenośnym. 

W tym temacie przedstawiono wymagania hello i hello obsługiwane scenariusze związane z konfigurowaniem CBA na urządzeniu z systemem iOS(Android) dla użytkowników dzierżaw Office 365 Enterprise, Business, edukacji, instytucji rządowych Stanów Zjednoczonych, Chin i planów Niemczech.

Ta funkcja jest dostępna w wersji zapoznawczej w planach Office 365 instytucji rządowych Stanów Zjednoczonych obrony i federalne.




## <a name="office-mobile-applications-support"></a>Obsługa aplikacji mobilnych pakietu Office

| Aplikacje | Pomoc techniczna |
| --- | --- |
| Azure Information Protection aplikacji |![Zaznacz][1] |
| Microsoft Teams |![Zaznacz][1] |
| OneNote |![Zaznacz][1] |
| OneDrive |![Zaznacz][1] |
| Outlook |![Zaznacz][1] |
| Aplikacji mobilnych usługi Power BI |![Zaznacz][1] |
| Skype dla firm |![Zaznacz][1] |
| Word / Excel / PowerPoint |![Zaznacz][1] |
| Yammer |![Zaznacz][1] |


## <a name="requirements"></a>Wymagania 

Witaj systemu operacyjnego urządzenia musi być w wersji dla systemu iOS 9 lub nowszym 

Serwer federacyjny musi być skonfigurowany.  

Authenticator firmy Microsoft jest wymagana w przypadku aplikacji pakietu Office w systemie iOS.  

Dla usługi Azure Active Directory toorevoke certyfikat klienta tokenu usług AD FS hello musi mieć powitania po oświadczeń:  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  (hello numer seryjny certyfikatu klienta hello) 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  (ciąg hello hello wystawcy certyfikatu klienta hello) 

Azure Active Directory dodaje token odświeżania toohello te oświadczenia, jeśli są dostępne w hello tokenu usług AD FS (lub inne tokenu SAML). Gdy hello token odświeżania musi toobe zweryfikowane, te informacje są używane toocheck hello odwołania. 

Najlepszym rozwiązaniem należy zaktualizować strony błędów usług AD FS hello hello następujący:

* Hello wymagania dotyczące instalowania hello Authenticator firmy Microsoft w systemie iOS
* Instrukcje dotyczące tooget certyfikatu użytkownika. 

Aby uzyskać więcej informacji, zobacz [dostosowywanie stron hello AD FS logowania](https://technet.microsoft.com/library/dn280950.aspx).

Wyślij niektóre aplikacje pakietu Office (z włączoną nowoczesnego uwierzytelniania) "*= monit logowania*" tooAzure AD w żądaniu. Domyślnie usługi Azure AD tłumaczy to w tooADFS żądania hello zbyt "*wauth = usernamepassworduri*" (żąda uwierzytelniania U/P toodo usług AD FS) i "*wfresh = 0*" (prosi o stan logowania jednokrotnego tooignore usług AD FS i wykonać świeże uwierzytelnianie) . Jeśli chcesz tooenable uwierzytelniania opartego na certyfikatach dla tych aplikacji, należy toomodify hello zachowanie usługi Azure AD. Tylko zestaw hello "*PromptLoginBehavior*" w ustawieniach domeny federacyjnej zbyt "*wyłączone*". Można użyć hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) tooperform polecenia cmdlet tego zadania:

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a>Obsługa klientów programu Exchange ActiveSync
W systemie iOS 9 lub nowszy klient poczty natywnego iOS hello jest obsługiwany. Dla wszystkich innych aplikacji Exchange ActiveSync toodetermine Jeśli ta funkcja jest obsługiwana, skontaktuj się z deweloperem aplikacji.  


## <a name="next-steps"></a>Następne kroki

Jeśli w danym środowisku uwierzytelniania opartego na certyfikatach tooconfigure, zobacz [wprowadzenie do uwierzytelniania opartego na certyfikatach w systemie Android](active-directory-certificate-based-authentication-get-started.md) instrukcje.


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
