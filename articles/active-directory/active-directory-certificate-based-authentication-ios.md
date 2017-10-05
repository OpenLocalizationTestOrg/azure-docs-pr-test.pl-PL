---
title: Azure Active Directory na podstawie certyfikatu uwierzytelniania w systemie iOS | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat obsługiwanych scenariuszy i wymagania dotyczące konfigurowania uwierzytelniania opartego na certyfikatach w rozwiązaniach z urządzeń z systemem iOS"
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
ms.openlocfilehash: c781f3f054fad5c5092fed5058c932fd4e97cf35
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a><span data-ttu-id="e8f4b-103">Azure Active Directory na podstawie certyfikatu uwierzytelniania w systemie iOS</span><span class="sxs-lookup"><span data-stu-id="e8f4b-103">Azure Active Directory certificate-based authentication on iOS</span></span>

<span data-ttu-id="e8f4b-104">Uwierzytelnianie oparte na certyfikatach (CBA) pozwala na uwierzytelniony przez usługę Azure Active Directory przy użyciu certyfikatu klienta na urządzeniu z systemem Windows, Android lub iOS podczas łączenia Twoje konto programu Exchange online:</span><span class="sxs-lookup"><span data-stu-id="e8f4b-104">Certificate-based authentication (CBA) enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="e8f4b-105">Aplikacje mobilne pakietu Office, takich jak Microsoft Outlook i Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="e8f4b-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="e8f4b-106">Klienci programu Exchange ActiveSync (EAS)</span><span class="sxs-lookup"><span data-stu-id="e8f4b-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="e8f4b-107">Konfigurowanie tej funkcji eliminuje potrzebę wprowadzić kombinacja nazwy użytkownika i hasła do niektórych poczty i aplikacje Microsoft Office na urządzeniu przenośnym.</span><span class="sxs-lookup"><span data-stu-id="e8f4b-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="e8f4b-108">W tym temacie przedstawiono wymagania i obsługiwane scenariusze związane z konfigurowaniem CBA na urządzeniu z systemem iOS(Android) dla użytkowników dzierżaw Office 365 Enterprise, Business, edukacji, instytucji rządowych Stanów Zjednoczonych, Chin i planów Niemczech.</span><span class="sxs-lookup"><span data-stu-id="e8f4b-108">This topic provides you with the requirements and the supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>

<span data-ttu-id="e8f4b-109">Ta funkcja jest dostępna w wersji zapoznawczej w planach Office 365 instytucji rządowych Stanów Zjednoczonych obrony i federalne.</span><span class="sxs-lookup"><span data-stu-id="e8f4b-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>




## <a name="office-mobile-applications-support"></a><span data-ttu-id="e8f4b-110">Obsługa aplikacji mobilnych pakietu Office</span><span class="sxs-lookup"><span data-stu-id="e8f4b-110">Office mobile applications support</span></span>

| <span data-ttu-id="e8f4b-111">Aplikacje</span><span class="sxs-lookup"><span data-stu-id="e8f4b-111">Apps</span></span> | <span data-ttu-id="e8f4b-112">Pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="e8f4b-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="e8f4b-113">Azure Information Protection aplikacji</span><span class="sxs-lookup"><span data-stu-id="e8f4b-113">Azure Information Protection app</span></span> |![Zaznacz][1] |
| <span data-ttu-id="e8f4b-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e8f4b-115">Microsoft Teams</span></span> |![Zaznacz][1] |
| <span data-ttu-id="e8f4b-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="e8f4b-117">OneNote</span></span> |![Zaznacz][1] |
| <span data-ttu-id="e8f4b-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="e8f4b-119">OneDrive</span></span> |![Zaznacz][1] |
| <span data-ttu-id="e8f4b-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="e8f4b-121">Outlook</span></span> |![Zaznacz][1] |
| <span data-ttu-id="e8f4b-123">Aplikacji mobilnych usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="e8f4b-123">Power BI mobile apps</span></span> |![Zaznacz][1] |
| <span data-ttu-id="e8f4b-125">Skype dla firm</span><span class="sxs-lookup"><span data-stu-id="e8f4b-125">Skype for Business</span></span> |![Zaznacz][1] |
| <span data-ttu-id="e8f4b-127">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="e8f4b-127">Word / Excel / PowerPoint</span></span> |![Zaznacz][1] |
| <span data-ttu-id="e8f4b-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="e8f4b-129">Yammer</span></span> |![Zaznacz][1] |


## <a name="requirements"></a><span data-ttu-id="e8f4b-131">Wymagania</span><span class="sxs-lookup"><span data-stu-id="e8f4b-131">Requirements</span></span> 

<span data-ttu-id="e8f4b-132">Wersja systemu operacyjnego urządzenia musi być systemu iOS 9 lub nowszym</span><span class="sxs-lookup"><span data-stu-id="e8f4b-132">The device OS version must be iOS 9 and above</span></span> 

<span data-ttu-id="e8f4b-133">Serwer federacyjny musi być skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="e8f4b-133">A federation server must be configured.</span></span>  

<span data-ttu-id="e8f4b-134">Authenticator firmy Microsoft jest wymagana w przypadku aplikacji pakietu Office w systemie iOS.</span><span class="sxs-lookup"><span data-stu-id="e8f4b-134">Microsoft Authenticator is required for Office applications on iOS.</span></span>  

<span data-ttu-id="e8f4b-135">Dla usługi Azure Active Directory odwołać certyfikat klienta tokenu usług AD FS musi mieć następujące oświadczeń:</span><span class="sxs-lookup"><span data-stu-id="e8f4b-135">For Azure Active Directory to revoke a client certificate, the ADFS token must have the following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="e8f4b-136">(Numer seryjny certyfikatu klienta)</span><span class="sxs-lookup"><span data-stu-id="e8f4b-136">(The serial number of the client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="e8f4b-137">(String wystawcy certyfikatu klienta)</span><span class="sxs-lookup"><span data-stu-id="e8f4b-137">(The string for the issuer of the client certificate)</span></span> 

<span data-ttu-id="e8f4b-138">Usługa Azure Active Directory dodaje te oświadczenia do tokenu odświeżania, jeśli są dostępne w tokenu usług AD FS (lub inne tokenu SAML).</span><span class="sxs-lookup"><span data-stu-id="e8f4b-138">Azure Active Directory adds these claims to the refresh token if they are available in the ADFS token (or any other SAML token).</span></span> <span data-ttu-id="e8f4b-139">Gdy token odświeżania musi być weryfikowane, te informacje służy do sprawdzania odwołania.</span><span class="sxs-lookup"><span data-stu-id="e8f4b-139">When the refresh token needs to be validated, this information is used to check the revocation.</span></span> 

<span data-ttu-id="e8f4b-140">Najlepszym rozwiązaniem należy zaktualizować strony błędów usług AD FS z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="e8f4b-140">As a best practice, you should update the ADFS error pages with the following:</span></span>

* <span data-ttu-id="e8f4b-141">Wymagania dotyczące instalowania Authenticator firmy Microsoft w systemie iOS</span><span class="sxs-lookup"><span data-stu-id="e8f4b-141">The requirement for installing the Microsoft Authenticator on iOS</span></span>
* <span data-ttu-id="e8f4b-142">Instrukcje dotyczące sposobu uzyskania certyfikatu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e8f4b-142">Instructions on how to get a user certificate.</span></span> 

<span data-ttu-id="e8f4b-143">Aby uzyskać więcej informacji, zobacz [dostosowywanie stron AD FS logowania](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="e8f4b-143">For more details, see [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>

<span data-ttu-id="e8f4b-144">Wyślij niektóre aplikacje pakietu Office (z włączoną nowoczesnego uwierzytelniania) "*= monit logowania*" do usługi Azure AD w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="e8f4b-144">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ to Azure AD in their request.</span></span> <span data-ttu-id="e8f4b-145">Domyślnie program Azure AD tłumaczy to w żądaniu, aby usługi AD FS do "*wauth = usernamepassworduri*" (zapyta usług AD FS do uwierzytelniania U/P) i "*wfresh = 0*" (zapyta usług AD FS, aby zignorować stan logowania jednokrotnego i wykonać świeże uwierzytelnianie).</span><span class="sxs-lookup"><span data-stu-id="e8f4b-145">By default, Azure AD translates this in the request to ADFS to ‘*wauth=usernamepassworduri*’ (asks ADFS to do U/P auth) and ‘*wfresh=0*’ (asks ADFS to ignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="e8f4b-146">Aby włączyć uwierzytelnianie oparte na certyfikatach dla tych aplikacji, należy zmodyfikować domyślne zachowanie usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8f4b-146">If you want to enable certificate-based authentication for these apps, you need to modify the default Azure AD behavior.</span></span> <span data-ttu-id="e8f4b-147">Ustaw wartość "*PromptLoginBehavior*"w ustawieniach domeny federacyjnej do"*wyłączone*".</span><span class="sxs-lookup"><span data-stu-id="e8f4b-147">Just set the ‘*PromptLoginBehavior*’ in your federated domain settings to ‘*Disabled*‘.</span></span> <span data-ttu-id="e8f4b-148">Można użyć [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) polecenia cmdlet do wykonania tego zadania:</span><span class="sxs-lookup"><span data-stu-id="e8f4b-148">You can use the [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet to perform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="e8f4b-149">Obsługa klientów programu Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="e8f4b-149">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="e8f4b-150">W systemie iOS 9 lub nowszy iOS natywnego klienta poczty e-mail jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="e8f4b-150">On iOS 9 or later, the native iOS mail client is supported.</span></span> <span data-ttu-id="e8f4b-151">Dla wszystkich innych aplikacji Exchange ActiveSync do ustalenia, czy ta funkcja jest obsługiwana, skontaktuj się z deweloperem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e8f4b-151">For all other Exchange ActiveSync applications, to determine if this feature is supported, contact your application developer.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="e8f4b-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e8f4b-152">Next steps</span></span>

<span data-ttu-id="e8f4b-153">Jeśli chcesz skonfigurować uwierzytelnianie oparte na certyfikatach w danym środowisku, zobacz [wprowadzenie do uwierzytelniania opartego na certyfikatach w systemie Android](active-directory-certificate-based-authentication-get-started.md) instrukcje.</span><span class="sxs-lookup"><span data-stu-id="e8f4b-153">If you want to configure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
