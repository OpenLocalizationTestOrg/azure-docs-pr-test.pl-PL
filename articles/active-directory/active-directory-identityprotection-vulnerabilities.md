---
title: "aaaVulnerabilities wykryta przez usługę Azure Active Directory Identity Protection | Dokumentacja firmy Microsoft"
description: "Przegląd luk w zabezpieczeniach hello wykrywanych przez usługę Azure Active Directory Identity Protection."
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
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="7411c-104">Luk w zabezpieczeniach wykrywanych przez usługę Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="7411c-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="7411c-105">Luki w zabezpieczeniach występują słabe strony w danym środowisku, które może być wykorzystane przez atakującego.</span><span class="sxs-lookup"><span data-stu-id="7411c-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="7411c-106">Zaleca się rozwiązać te luki w zabezpieczeniach tooimprove hello stan zabezpieczeń organizacji i uniemożliwić osobom atakującym ich wykorzystania.</span><span class="sxs-lookup"><span data-stu-id="7411c-106">We recommend that you address these vulnerabilities tooimprove hello security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="7411c-107">![luki w zabezpieczeniach](./media/active-directory-identityprotection-vulnerabilities/101.png "luk w zabezpieczeniach")</span><span class="sxs-lookup"><span data-stu-id="7411c-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="7411c-108">Hello następujące sekcje zawierają omówienie luk w zabezpieczeniach hello zgłoszone przez ochronę tożsamości.</span><span class="sxs-lookup"><span data-stu-id="7411c-108">hello following sections provide you with an overview of hello vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="7411c-109">Rejestracja usługi Multi-Factor authentication nie jest skonfigurowany</span><span class="sxs-lookup"><span data-stu-id="7411c-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="7411c-110">Ta luka w zabezpieczeniach pomaga kontrolować hello wdrożenia usługi Azure Multi-Factor Authentication w organizacji.</span><span class="sxs-lookup"><span data-stu-id="7411c-110">This vulnerability helps you control hello deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="7411c-111">Usługa Azure Multi-Factor authentication udostępnia drugą warstwę zabezpieczeń toouser uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="7411c-111">Azure multi-factor authentication provides a second layer of security toouser authentication.</span></span> <span data-ttu-id="7411c-112">Ułatwia zabezpieczenie dostępu toodata i aplikacje spełniając zapotrzebowanie na prosty proces logowania.</span><span class="sxs-lookup"><span data-stu-id="7411c-112">It helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="7411c-113">Zapewnia silne uwierzytelnianie za pomocą różnych opcji weryfikacji łatwe — połączenie telefoniczne, wiadomość tekstowa lub aplikacji mobilnej weryfikacji lub powiadamiania o kod i 3rd strona tokenów OATH.</span><span class="sxs-lookup"><span data-stu-id="7411c-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="7411c-114">Firma Microsoft zaleca wymusić uwierzytelnianie wieloskładnikowe Azure logowania użytkownika. Uwierzytelnianie wieloskładnikowe odgrywa kluczową rolę w zasadach dostępu warunkowego opartego na ryzyko dostępne za pośrednictwem Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="7411c-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins. Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="7411c-115">Aby uzyskać więcej informacji, zobacz [co to jest uwierzytelnianie wieloskładnikowe Azure?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="7411c-115">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="7411c-116">Aplikacje w chmurze niezarządzane</span><span class="sxs-lookup"><span data-stu-id="7411c-116">Unmanaged cloud apps</span></span>
<span data-ttu-id="7411c-117">Ta luka w zabezpieczeniach pomaga zidentyfikować aplikacje w chmurze niezarządzane w Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="7411c-117">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="7411c-118">W nowoczesnych przedsiębiorstwa działów IT są często zna wszystkie aplikacje chmury hello korzystania przez użytkowników w organizacji toodo służbowym.</span><span class="sxs-lookup"><span data-stu-id="7411c-118">In modern enterprises, IT departments are often unaware of all hello cloud applications that users in their organization are using toodo their work.</span></span> <span data-ttu-id="7411c-119">Jest łatwy toosee Dlaczego Administratorzy byłyby danych toocorporate nieautoryzowanym dostępem, wycieku danych oraz inne zagrożenia dla bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="7411c-119">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="7411c-120">Firma Microsoft zaleca organizacji do wdrożenia aplikacji w chmurze niezarządzane toodiscover Cloud App Discovery i toomanage te aplikacje przy użyciu usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7411c-120">We recommend that your organization deploy Cloud App Discovery toodiscover unmanaged cloud applications, and toomanage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="7411c-121">Aby uzyskać więcej informacji, zobacz [znajdowania aplikacji w chmurze niezarządzane z usługi Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7411c-121">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="7411c-122">Alerty zabezpieczeń ze Zarządzanie tożsamościami uprzywilejowanymi</span><span class="sxs-lookup"><span data-stu-id="7411c-122">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="7411c-123">Ta luka w zabezpieczeniach pomaga wykrywać oraz rozwiązywanie alertów dotyczących tożsamości uprzywilejowanych w Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="7411c-123">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="7411c-124">toocarry użytkowników tooenable operacje uprzywilejowane, organizacje muszą także tymczasowych lub trwałych uprzywilejowanego dostępu w usłudze Azure AD, użytkownicy toogrant zasobów platformy Azure lub usługi Office 365 lub innych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="7411c-124">tooenable users toocarry out privileged operations, organizations need toogrant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="7411c-125">Każdy z tych użytkownicy o odpowiednich uprawnieniach zwiększa hello ataku Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="7411c-125">Each of these privileged users increases hello attack surface of your organization.</span></span> <span data-ttu-id="7411c-126">Tę lukę w zabezpieczeniach pomaga zidentyfikować użytkowników z dostępem uprzywilejowanym zbędne i podjąć odpowiednie działania tooreduce lub wyeliminowanie hello ryzyka, które stanowią one.</span><span class="sxs-lookup"><span data-stu-id="7411c-126">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action tooreduce or eliminate hello risk they pose.</span></span> 

<span data-ttu-id="7411c-127">Zaleca się, że Twoja organizacja korzysta z usługi Azure AD Privileged Identity Management toomanage, kontroli i monitor uprzywilejowany tożsamości i ich tooresources dostępu w usłudze Azure AD, jak również innych usług online firmy Microsoft, takich jak usługi Office 365 lub Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="7411c-127">We recommend that your organization uses Azure AD Privileged Identity Management toomanage, control, and monitor privileged identities and their access tooresources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="7411c-128">Aby uzyskać więcej informacji, zobacz [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="7411c-128">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="7411c-129">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="7411c-129">See also</span></span>
* [<span data-ttu-id="7411c-130">Ochronę tożsamości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7411c-130">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

