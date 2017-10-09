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
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a><span data-ttu-id="85b40-103">Azure Active Directory na podstawie certyfikatu uwierzytelniania w systemie iOS</span><span class="sxs-lookup"><span data-stu-id="85b40-103">Azure Active Directory certificate-based authentication on iOS</span></span>

<span data-ttu-id="85b40-104">Uwierzytelnianie oparte na certyfikatach (CBA) umożliwia toobe uwierzytelniony przez usługę Azure Active Directory przy użyciu certyfikatu klienta na urządzeniu z systemem Windows, Android lub iOS podczas łączenia Twoje konto programu Exchange online:</span><span class="sxs-lookup"><span data-stu-id="85b40-104">Certificate-based authentication (CBA) enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="85b40-105">Aplikacje mobilne pakietu Office, takich jak Microsoft Outlook i Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="85b40-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="85b40-106">Klienci programu Exchange ActiveSync (EAS)</span><span class="sxs-lookup"><span data-stu-id="85b40-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="85b40-107">Konfigurowanie tej funkcji eliminuje hello potrzeby tooenter nazwę użytkownika i kombinacja hasła do niektórych poczty i aplikacje Microsoft Office na urządzeniu przenośnym.</span><span class="sxs-lookup"><span data-stu-id="85b40-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="85b40-108">W tym temacie przedstawiono wymagania hello i hello obsługiwane scenariusze związane z konfigurowaniem CBA na urządzeniu z systemem iOS(Android) dla użytkowników dzierżaw Office 365 Enterprise, Business, edukacji, instytucji rządowych Stanów Zjednoczonych, Chin i planów Niemczech.</span><span class="sxs-lookup"><span data-stu-id="85b40-108">This topic provides you with hello requirements and hello supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>

<span data-ttu-id="85b40-109">Ta funkcja jest dostępna w wersji zapoznawczej w planach Office 365 instytucji rządowych Stanów Zjednoczonych obrony i federalne.</span><span class="sxs-lookup"><span data-stu-id="85b40-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>




## <a name="office-mobile-applications-support"></a><span data-ttu-id="85b40-110">Obsługa aplikacji mobilnych pakietu Office</span><span class="sxs-lookup"><span data-stu-id="85b40-110">Office mobile applications support</span></span>

| <span data-ttu-id="85b40-111">Aplikacje</span><span class="sxs-lookup"><span data-stu-id="85b40-111">Apps</span></span> | <span data-ttu-id="85b40-112">Pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="85b40-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="85b40-113">Azure Information Protection aplikacji</span><span class="sxs-lookup"><span data-stu-id="85b40-113">Azure Information Protection app</span></span> |![Zaznacz][1] |
| <span data-ttu-id="85b40-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="85b40-115">Microsoft Teams</span></span> |![Zaznacz][1] |
| <span data-ttu-id="85b40-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="85b40-117">OneNote</span></span> |![Zaznacz][1] |
| <span data-ttu-id="85b40-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="85b40-119">OneDrive</span></span> |![Zaznacz][1] |
| <span data-ttu-id="85b40-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="85b40-121">Outlook</span></span> |![Zaznacz][1] |
| <span data-ttu-id="85b40-123">Aplikacji mobilnych usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="85b40-123">Power BI mobile apps</span></span> |![Zaznacz][1] |
| <span data-ttu-id="85b40-125">Skype dla firm</span><span class="sxs-lookup"><span data-stu-id="85b40-125">Skype for Business</span></span> |![Zaznacz][1] |
| <span data-ttu-id="85b40-127">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="85b40-127">Word / Excel / PowerPoint</span></span> |![Zaznacz][1] |
| <span data-ttu-id="85b40-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="85b40-129">Yammer</span></span> |![Zaznacz][1] |


## <a name="requirements"></a><span data-ttu-id="85b40-131">Wymagania</span><span class="sxs-lookup"><span data-stu-id="85b40-131">Requirements</span></span> 

<span data-ttu-id="85b40-132">Witaj systemu operacyjnego urządzenia musi być w wersji dla systemu iOS 9 lub nowszym</span><span class="sxs-lookup"><span data-stu-id="85b40-132">hello device OS version must be iOS 9 and above</span></span> 

<span data-ttu-id="85b40-133">Serwer federacyjny musi być skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="85b40-133">A federation server must be configured.</span></span>  

<span data-ttu-id="85b40-134">Authenticator firmy Microsoft jest wymagana w przypadku aplikacji pakietu Office w systemie iOS.</span><span class="sxs-lookup"><span data-stu-id="85b40-134">Microsoft Authenticator is required for Office applications on iOS.</span></span>  

<span data-ttu-id="85b40-135">Dla usługi Azure Active Directory toorevoke certyfikat klienta tokenu usług AD FS hello musi mieć powitania po oświadczeń:</span><span class="sxs-lookup"><span data-stu-id="85b40-135">For Azure Active Directory toorevoke a client certificate, hello ADFS token must have hello following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="85b40-136">(hello numer seryjny certyfikatu klienta hello)</span><span class="sxs-lookup"><span data-stu-id="85b40-136">(hello serial number of hello client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="85b40-137">(ciąg hello hello wystawcy certyfikatu klienta hello)</span><span class="sxs-lookup"><span data-stu-id="85b40-137">(hello string for hello issuer of hello client certificate)</span></span> 

<span data-ttu-id="85b40-138">Azure Active Directory dodaje token odświeżania toohello te oświadczenia, jeśli są dostępne w hello tokenu usług AD FS (lub inne tokenu SAML).</span><span class="sxs-lookup"><span data-stu-id="85b40-138">Azure Active Directory adds these claims toohello refresh token if they are available in hello ADFS token (or any other SAML token).</span></span> <span data-ttu-id="85b40-139">Gdy hello token odświeżania musi toobe zweryfikowane, te informacje są używane toocheck hello odwołania.</span><span class="sxs-lookup"><span data-stu-id="85b40-139">When hello refresh token needs toobe validated, this information is used toocheck hello revocation.</span></span> 

<span data-ttu-id="85b40-140">Najlepszym rozwiązaniem należy zaktualizować strony błędów usług AD FS hello hello następujący:</span><span class="sxs-lookup"><span data-stu-id="85b40-140">As a best practice, you should update hello ADFS error pages with hello following:</span></span>

* <span data-ttu-id="85b40-141">Hello wymagania dotyczące instalowania hello Authenticator firmy Microsoft w systemie iOS</span><span class="sxs-lookup"><span data-stu-id="85b40-141">hello requirement for installing hello Microsoft Authenticator on iOS</span></span>
* <span data-ttu-id="85b40-142">Instrukcje dotyczące tooget certyfikatu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="85b40-142">Instructions on how tooget a user certificate.</span></span> 

<span data-ttu-id="85b40-143">Aby uzyskać więcej informacji, zobacz [dostosowywanie stron hello AD FS logowania](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="85b40-143">For more details, see [Customizing hello AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>

<span data-ttu-id="85b40-144">Wyślij niektóre aplikacje pakietu Office (z włączoną nowoczesnego uwierzytelniania) "*= monit logowania*" tooAzure AD w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="85b40-144">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ tooAzure AD in their request.</span></span> <span data-ttu-id="85b40-145">Domyślnie usługi Azure AD tłumaczy to w tooADFS żądania hello zbyt "*wauth = usernamepassworduri*" (żąda uwierzytelniania U/P toodo usług AD FS) i "*wfresh = 0*" (prosi o stan logowania jednokrotnego tooignore usług AD FS i wykonać świeże uwierzytelnianie) .</span><span class="sxs-lookup"><span data-stu-id="85b40-145">By default, Azure AD translates this in hello request tooADFS too‘*wauth=usernamepassworduri*’ (asks ADFS toodo U/P auth) and ‘*wfresh=0*’ (asks ADFS tooignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="85b40-146">Jeśli chcesz tooenable uwierzytelniania opartego na certyfikatach dla tych aplikacji, należy toomodify hello zachowanie usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85b40-146">If you want tooenable certificate-based authentication for these apps, you need toomodify hello default Azure AD behavior.</span></span> <span data-ttu-id="85b40-147">Tylko zestaw hello "*PromptLoginBehavior*" w ustawieniach domeny federacyjnej zbyt "*wyłączone*".</span><span class="sxs-lookup"><span data-stu-id="85b40-147">Just set hello ‘*PromptLoginBehavior*’ in your federated domain settings too‘*Disabled*‘.</span></span> <span data-ttu-id="85b40-148">Można użyć hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) tooperform polecenia cmdlet tego zadania:</span><span class="sxs-lookup"><span data-stu-id="85b40-148">You can use hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="85b40-149">Obsługa klientów programu Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="85b40-149">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="85b40-150">W systemie iOS 9 lub nowszy klient poczty natywnego iOS hello jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="85b40-150">On iOS 9 or later, hello native iOS mail client is supported.</span></span> <span data-ttu-id="85b40-151">Dla wszystkich innych aplikacji Exchange ActiveSync toodetermine Jeśli ta funkcja jest obsługiwana, skontaktuj się z deweloperem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="85b40-151">For all other Exchange ActiveSync applications, toodetermine if this feature is supported, contact your application developer.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="85b40-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="85b40-152">Next steps</span></span>

<span data-ttu-id="85b40-153">Jeśli w danym środowisku uwierzytelniania opartego na certyfikatach tooconfigure, zobacz [wprowadzenie do uwierzytelniania opartego na certyfikatach w systemie Android](active-directory-certificate-based-authentication-get-started.md) instrukcje.</span><span class="sxs-lookup"><span data-stu-id="85b40-153">If you want tooconfigure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
