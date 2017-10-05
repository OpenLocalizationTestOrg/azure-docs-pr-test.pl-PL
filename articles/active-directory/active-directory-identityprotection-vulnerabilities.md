---
title: "Luk w zabezpieczeniach wykrywanych przez usługę Azure Active Directory Identity Protection | Dokumentacja firmy Microsoft"
description: "Przegląd luk w zabezpieczeniach wykryta przez usługę Azure Active Directory Identity Protection."
services: active-directory
keywords: "ochronę tożsamości usługi Azure active directory, usługa cloud app discovery, zarządzanie aplikacjami, zabezpieczeń, ryzyka, poziom ryzyka, luki w zabezpieczeniach, zasady zabezpieczeń"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 364873ff54099a6123e40b12e819d1745751f285
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="ad6fc-104">Luk w zabezpieczeniach wykrywanych przez usługę Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ad6fc-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="ad6fc-105">Luki w zabezpieczeniach występują słabe strony w danym środowisku, które może być wykorzystane przez atakującego.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="ad6fc-106">Zaleca się rozwiązać te luki w zabezpieczeniach aby poprawić stan zabezpieczeń organizacji i uniemożliwić osobom atakującym ich wykorzystania.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-106">We recommend that you address these vulnerabilities to improve the security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="ad6fc-107">![luki w zabezpieczeniach](./media/active-directory-identityprotection-vulnerabilities/101.png "luk w zabezpieczeniach")</span><span class="sxs-lookup"><span data-stu-id="ad6fc-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="ad6fc-108">Poniższe sekcje zawierają przegląd luk w zabezpieczeniach zgłoszone przez ochronę tożsamości.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-108">The following sections provide you with an overview of the vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="ad6fc-109">Rejestracja usługi Multi-Factor authentication nie jest skonfigurowany</span><span class="sxs-lookup"><span data-stu-id="ad6fc-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="ad6fc-110">Ta luka w zabezpieczeniach ułatwia kontrolowanie wdrażania usługi Azure Multi-Factor Authentication w organizacji.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-110">This vulnerability helps you control the deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="ad6fc-111">Usługa Azure Multi-Factor authentication udostępnia drugą warstwę zabezpieczeń w celu uwierzytelnienia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-111">Azure multi-factor authentication provides a second layer of security to user authentication.</span></span> <span data-ttu-id="ad6fc-112">Go pomaga w zabezpieczaniu dostępu do danych i aplikacji spełniając zapotrzebowanie na prosty proces logowania.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-112">It helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="ad6fc-113">Zapewnia silne uwierzytelnianie za pomocą różnych opcji weryfikacji łatwe — połączenie telefoniczne, wiadomość tekstowa lub aplikacji mobilnej weryfikacji lub powiadamiania o kod i 3rd strona tokenów OATH.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="ad6fc-114">Firma Microsoft zaleca wymusić uwierzytelnianie wieloskładnikowe Azure logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins.</span></span> <span data-ttu-id="ad6fc-115">Uwierzytelnianie wieloskładnikowe odgrywa kluczową rolę w zasadach dostępu warunkowego opartego na ryzyko dostępne za pośrednictwem Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-115">Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="ad6fc-116">Aby uzyskać więcej informacji, zobacz [co to jest uwierzytelnianie wieloskładnikowe Azure?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ad6fc-116">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="ad6fc-117">Aplikacje w chmurze niezarządzane</span><span class="sxs-lookup"><span data-stu-id="ad6fc-117">Unmanaged cloud apps</span></span>
<span data-ttu-id="ad6fc-118">Ta luka w zabezpieczeniach pomaga zidentyfikować aplikacje w chmurze niezarządzane w Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-118">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="ad6fc-119">W przedsiębiorstwach nowoczesnego działu IT są często zna wszystkie aplikacje chmury, które użytkownicy w organizacji korzystają z ich w pracy.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-119">In modern enterprises, IT departments are often unaware of all the cloud applications that users in their organization are using to do their work.</span></span> <span data-ttu-id="ad6fc-120">To proste zobaczyć, dlaczego Administratorzy byłyby problemów dotyczących nieautoryzowanego dostępu do danych firmowych, wycieku danych i inne zagrożenia dla bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-120">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="ad6fc-121">Firma Microsoft zaleca wdrożenia Cloud App Discovery do wykrywania aplikacji w chmurze niezarządzane oraz do zarządzania te aplikacje przy użyciu usługi Azure Active Directory w organizacji.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-121">We recommend that your organization deploy Cloud App Discovery to discover unmanaged cloud applications, and to manage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="ad6fc-122">Aby uzyskać więcej informacji, zobacz [znajdowania aplikacji w chmurze niezarządzane z usługi Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ad6fc-122">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="ad6fc-123">Alerty zabezpieczeń ze Zarządzanie tożsamościami uprzywilejowanymi</span><span class="sxs-lookup"><span data-stu-id="ad6fc-123">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="ad6fc-124">Ta luka w zabezpieczeniach pomaga wykrywać oraz rozwiązywanie alertów dotyczących tożsamości uprzywilejowanych w Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-124">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="ad6fc-125">Aby umożliwić użytkownikom do wykonywania uprzywilejowanych operacji, organizacja musi udzielić użytkownikom tymczasowych lub trwałych uprzywilejowanego dostępu w usłudze Azure AD, Azure lub usługi Office 365 zasobów lub innych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-125">To enable users to carry out privileged operations, organizations need to grant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="ad6fc-126">Każdy z tych użytkownicy o odpowiednich uprawnieniach zwiększa obszar narażony Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-126">Each of these privileged users increases the attack surface of your organization.</span></span> <span data-ttu-id="ad6fc-127">Ta luka w zabezpieczeniach pomaga zidentyfikować użytkowników z niepotrzebnych uprzywilejowanego dostępu i podjąć odpowiednie działania w celu ograniczenie lub wyeliminowanie ryzyka, które stanowią one.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-127">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action to reduce or eliminate the risk they pose.</span></span> 

<span data-ttu-id="ad6fc-128">Zaleca się Twoja organizacja korzysta z usługi Azure AD Privileged Identity Management w celu zarządzania kontrolą, i monitor uprzywilejowany tożsamości i dostępu do zasobów w usłudze Azure AD, a także innych usług online firmy Microsoft, takich jak usługi Office 365 lub Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="ad6fc-128">We recommend that your organization uses Azure AD Privileged Identity Management to manage, control, and monitor privileged identities and their access to resources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="ad6fc-129">Aby uzyskać więcej informacji, zobacz [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ad6fc-129">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="ad6fc-130">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ad6fc-130">See also</span></span>
* [<span data-ttu-id="ad6fc-131">Ochronę tożsamości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad6fc-131">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

