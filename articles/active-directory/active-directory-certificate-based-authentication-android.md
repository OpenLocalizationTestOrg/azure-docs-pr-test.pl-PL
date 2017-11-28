---
title: Azure Active Directory na podstawie certyfikatu uwierzytelniania w systemie Android | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat obsługiwanych scenariuszy i wymagania dotyczące konfigurowania uwierzytelniania opartego na certyfikatach w rozwiązaniach urządzeń z systemem Android"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/28/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 8005bfe821fea25539c84efdccf6c49bd5f1f8ee
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-android"></a><span data-ttu-id="4d120-103">Azure Active Directory na podstawie certyfikatu uwierzytelniania w systemie Android</span><span class="sxs-lookup"><span data-stu-id="4d120-103">Azure Active Directory certificate-based authentication on Android</span></span>


<span data-ttu-id="4d120-104">Uwierzytelnianie oparte na certyfikatach (CBA) pozwala na uwierzytelniony przez usługę Azure Active Directory przy użyciu certyfikatu klienta na urządzeniu z systemem Windows, Android lub iOS podczas łączenia Twoje konto programu Exchange online:</span><span class="sxs-lookup"><span data-stu-id="4d120-104">Certificate-based authentication (CBA) enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="4d120-105">Aplikacje mobilne pakietu Office, takich jak Microsoft Outlook i Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="4d120-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="4d120-106">Klienci programu Exchange ActiveSync (EAS)</span><span class="sxs-lookup"><span data-stu-id="4d120-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="4d120-107">Konfigurowanie tej funkcji eliminuje potrzebę wprowadzić kombinacja nazwy użytkownika i hasła do niektórych poczty i aplikacje Microsoft Office na urządzeniu przenośnym.</span><span class="sxs-lookup"><span data-stu-id="4d120-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="4d120-108">W tym temacie przedstawiono wymagania i obsługiwane scenariusze związane z konfigurowaniem CBA na urządzeniu z systemem iOS(Android) dla użytkowników dzierżaw Office 365 Enterprise, Business, edukacji, instytucji rządowych Stanów Zjednoczonych, Chin i planów Niemczech.</span><span class="sxs-lookup"><span data-stu-id="4d120-108">This topic provides you with the requirements and the supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>



<span data-ttu-id="4d120-109">Ta funkcja jest dostępna w wersji zapoznawczej w planach Office 365 instytucji rządowych Stanów Zjednoczonych obrony i federalne.</span><span class="sxs-lookup"><span data-stu-id="4d120-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>


## <a name="office-mobile-applications-support"></a><span data-ttu-id="4d120-110">Obsługa aplikacji mobilnych pakietu Office</span><span class="sxs-lookup"><span data-stu-id="4d120-110">Office mobile applications support</span></span>
| <span data-ttu-id="4d120-111">Aplikacje</span><span class="sxs-lookup"><span data-stu-id="4d120-111">Apps</span></span> | <span data-ttu-id="4d120-112">Pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="4d120-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="4d120-113">Azure Information Protection aplikacji</span><span class="sxs-lookup"><span data-stu-id="4d120-113">Azure Information Protection app</span></span> |![Zaznacz][1] |
| <span data-ttu-id="4d120-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4d120-115">Microsoft Teams</span></span> |![Zaznacz][1] |
| <span data-ttu-id="4d120-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="4d120-117">OneNote</span></span> |![Zaznacz][1] |
| <span data-ttu-id="4d120-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="4d120-119">OneDrive</span></span> |![Zaznacz][1] |
| <span data-ttu-id="4d120-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="4d120-121">Outlook</span></span> |![Zaznacz][1] |
| <span data-ttu-id="4d120-123">Aplikacji mobilnych usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="4d120-123">Power BI mobile apps</span></span> |![Zaznacz][1] |
| <span data-ttu-id="4d120-125">Skype dla firm</span><span class="sxs-lookup"><span data-stu-id="4d120-125">Skype for Business</span></span> |![Zaznacz][1] |
| <span data-ttu-id="4d120-127">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="4d120-127">Word / Excel / PowerPoint</span></span> |![Zaznacz][1] |
| <span data-ttu-id="4d120-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="4d120-129">Yammer</span></span> |![Zaznacz][1] |


### <a name="implementation-requirements"></a><span data-ttu-id="4d120-131">Wymagania dotyczące implementacji</span><span class="sxs-lookup"><span data-stu-id="4d120-131">Implementation requirements</span></span>

<span data-ttu-id="4d120-132">Wersja systemu operacyjnego urządzenia musi być Android 5.0 (interfejs typu lizak) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="4d120-132">The device OS version must be Android 5.0 (Lollipop) and above.</span></span> 

<span data-ttu-id="4d120-133">Serwer federacyjny musi być skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="4d120-133">A federation server must be configured.</span></span>  

<span data-ttu-id="4d120-134">Dla usługi Azure Active Directory odwołać certyfikat klienta tokenu usług AD FS musi mieć następujące oświadczeń:</span><span class="sxs-lookup"><span data-stu-id="4d120-134">For Azure Active Directory to revoke a client certificate, the ADFS token must have the following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="4d120-135">(Numer seryjny certyfikatu klienta)</span><span class="sxs-lookup"><span data-stu-id="4d120-135">(The serial number of the client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="4d120-136">(String wystawcy certyfikatu klienta)</span><span class="sxs-lookup"><span data-stu-id="4d120-136">(The string for the issuer of the client certificate)</span></span> 

<span data-ttu-id="4d120-137">Usługa Azure Active Directory dodaje te oświadczenia do tokenu odświeżania, jeśli są dostępne w tokenu usług AD FS (lub inne tokenu SAML).</span><span class="sxs-lookup"><span data-stu-id="4d120-137">Azure Active Directory adds these claims to the refresh token if they are available in the ADFS token (or any other SAML token).</span></span> <span data-ttu-id="4d120-138">Gdy token odświeżania musi być weryfikowane, te informacje służy do sprawdzania odwołania.</span><span class="sxs-lookup"><span data-stu-id="4d120-138">When the refresh token needs to be validated, this information is used to check the revocation.</span></span> 

<span data-ttu-id="4d120-139">Najlepszym rozwiązaniem należy zaktualizować strony błędów usług AD FS z instrukcjami dotyczącymi sposobu uzyskania certyfikatu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4d120-139">As a best practice, you should update the ADFS error pages with instructions on how to get a user certificate.</span></span>  
<span data-ttu-id="4d120-140">Aby uzyskać więcej informacji, zobacz [dostosowywanie stron AD FS logowania](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d120-140">For more details, see [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>  

<span data-ttu-id="4d120-141">Wyślij niektóre aplikacje pakietu Office (z włączoną nowoczesnego uwierzytelniania) "*= monit logowania*" do usługi Azure AD w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="4d120-141">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ to Azure AD in their request.</span></span> <span data-ttu-id="4d120-142">Domyślnie program Azure AD tłumaczy to w żądaniu, aby usługi AD FS do "*wauth = usernamepassworduri*" (zapyta usług AD FS do uwierzytelniania U/P) i "*wfresh = 0*" (zapyta usług AD FS, aby zignorować stan logowania jednokrotnego i wykonać świeże uwierzytelnianie).</span><span class="sxs-lookup"><span data-stu-id="4d120-142">By default, Azure AD translates this in the request to ADFS to ‘*wauth=usernamepassworduri*’ (asks ADFS to do U/P auth) and ‘*wfresh=0*’ (asks ADFS to ignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="4d120-143">Aby włączyć uwierzytelnianie oparte na certyfikatach dla tych aplikacji, należy zmodyfikować domyślne zachowanie usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d120-143">If you want to enable certificate-based authentication for these apps, you need to modify the default Azure AD behavior.</span></span> <span data-ttu-id="4d120-144">Ustaw wartość "*PromptLoginBehavior*"w ustawieniach domeny federacyjnej do"*wyłączone*".</span><span class="sxs-lookup"><span data-stu-id="4d120-144">Just set the ‘*PromptLoginBehavior*’ in your federated domain settings to ‘*Disabled*‘.</span></span> <span data-ttu-id="4d120-145">Można użyć [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) polecenia cmdlet do wykonania tego zadania:</span><span class="sxs-lookup"><span data-stu-id="4d120-145">You can use the [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet to perform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`



## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="4d120-146">Obsługa klientów programu Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="4d120-146">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="4d120-147">Niektóre aplikacje programu Exchange ActiveSync w systemie Android 5.0 (interfejs typu lizak) lub nowszym są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="4d120-147">Certain Exchange ActiveSync applications on Android 5.0 (Lollipop) or later are supported.</span></span> <span data-ttu-id="4d120-148">Aby ustalić, czy aplikację poczty e-mail obsługuje tę funkcję, skontaktuj się z deweloperem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4d120-148">To determine if your email application does support this feature, please contact your application developer.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="4d120-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4d120-149">Next steps</span></span>

<span data-ttu-id="4d120-150">Jeśli chcesz skonfigurować uwierzytelnianie oparte na certyfikatach w danym środowisku, zobacz [wprowadzenie do uwierzytelniania opartego na certyfikatach w systemie Android](active-directory-certificate-based-authentication-get-started.md) instrukcje.</span><span class="sxs-lookup"><span data-stu-id="4d120-150">If you want to configure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-android/ic195031.png
