---
title: "Zabezpieczanie uprzywilejowanego dostępu w usłudze Azure AD | Dokumentacja firmy Microsoft"
description: "Temat opisujący podejścia do zabezpieczania uprzywilejowanego dostępu na platformie Azure, Azure Active Directory i usług Microsoft Online Services."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: mwahl
ms.assetid: 235a0ce9-1daf-4433-8f65-9c6afcd64d08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: acd1c11cecfa37f607fe5d82a76a40647093f43f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a><span data-ttu-id="3c1d6-103">Zabezpieczanie uprzywilejowanego dostępu w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c1d6-103">Securing privileged access in Azure AD</span></span>
<span data-ttu-id="3c1d6-104">Zabezpieczanie uprzywilejowanego dostępu jest krytyczne pierwszy krok w celu ochrony zasobów biznesowych w organizacji modern.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-104">Securing privileged access is a critical first step to help protect business assets in a modern organization.</span></span> <span data-ttu-id="3c1d6-105">Uprzywilejowane konta są kontami, które Administruj i Zarządzaj systemów informatycznych.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-105">Privileged accounts are accounts that administer and manage IT systems.</span></span> <span data-ttu-id="3c1d6-106">Osoby atakujące przez docelowe te konta do uzyskiwania dostępu do danych organizacji i systemów.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-106">Cyber-attackers target these accounts to gain access to an organization’s data and systems.</span></span> <span data-ttu-id="3c1d6-107">Aby zabezpieczyć uprzywilejowanego dostępu, można odizolować kont i systemów ryzyka narażenia na złośliwy użytkownik.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-107">To secure privileged access, you should isolate the accounts and systems from the risk of being exposed to a malicious user.</span></span>

<span data-ttu-id="3c1d6-108">Coraz więcej użytkowników uzyskać uprzywilejowany dostęp za pomocą usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-108">More users are starting to get privileged access through cloud services.</span></span> <span data-ttu-id="3c1d6-109">Może to obejmować Administratorzy globalni dla usługi Office 365, Administratorzy subskrypcji platformy Azure i użytkowników, którzy mają dostęp administracyjny na maszynach wirtualnych lub w aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-109">This can include global administrators of Office365, Azure subscription administrators, and users who have administrative access in VMs or on SaaS apps.</span></span>

<span data-ttu-id="3c1d6-110">Firma Microsoft zaleca wykonanie tego planu [zabezpieczanie uprzywilejowanego dostępu](https://technet.microsoft.com/library/mt631194.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-110">Microsoft recommends you follow this roadmap on [Securing Privileged Access](https://technet.microsoft.com/library/mt631194.aspx).</span></span>

<span data-ttu-id="3c1d6-111">Dla klientów korzystających z usługi Azure Active Directory, usługi Office 365 lub innych usług firmy Microsoft i aplikacji czy konta użytkowników są zarządzane i uwierzytelniony przez usługę Active Directory lub w usłudze Azure Active Directory stosuje się te zasady.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-111">For customers using Azure Active Directory, Office 365, or other Microsoft services and applications, these principles apply whether user accounts are managed and authenticated by Active Directory or in Azure Active Directory.</span></span> <span data-ttu-id="3c1d6-112">Poniższe sekcje zawierają więcej informacji na temat funkcji usługi Azure AD do obsługi zabezpieczanie uprzywilejowanego dostępu.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-112">The following sections provide more information on Azure AD features to support securing privileged access.</span></span>

## <a name="azure-multi-factor-authentication"></a><span data-ttu-id="3c1d6-113">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3c1d6-113">Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="3c1d6-114">Aby zwiększyć bezpieczeństwo administratora uwierzytelniania, należy włączyć weryfikację dwuetapową przed udzieleniem im uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-114">To increase the security of administrator authentication, you should require two-step verification before granting privileges.</span></span> <span data-ttu-id="3c1d6-115">Weryfikacja dwuetapowa jest metodę sprawdzania, kto, które są wymagane jest użycie więcej niż tylko nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-115">Two-step verification is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="3c1d6-116">Zapewnia drugą warstwę zabezpieczeń do logowania użytkowników i transakcji.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-116">It provides a second layer of security to user sign-ins and transactions.</span></span>

<span data-ttu-id="3c1d6-117">Usługa Azure Multi-Factor Authentication (MFA) jest rozwiązania weryfikacji dwuetapowej firmy Microsoft, które ułatwia zabezpieczenie dostępu do danych i aplikacji, spełniając użytkownika popytu na prosty proces logowania.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-117">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution, which helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="3c1d6-118">Zapewnia silne uwierzytelnianie za pośrednictwem szereg opcji weryfikacji łatwy w tym:</span><span class="sxs-lookup"><span data-stu-id="3c1d6-118">It delivers strong authentication via a range of easy verification options including:</span></span>

- <span data-ttu-id="3c1d6-119">połączenia telefoniczne</span><span class="sxs-lookup"><span data-stu-id="3c1d6-119">phone calls</span></span>
- <span data-ttu-id="3c1d6-120">Wiadomości SMS</span><span class="sxs-lookup"><span data-stu-id="3c1d6-120">text messages</span></span>
- <span data-ttu-id="3c1d6-121">powiadomienia z aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="3c1d6-121">mobile app notifications</span></span>
- <span data-ttu-id="3c1d6-122">kodów weryfikacyjnych aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="3c1d6-122">mobile app verification codes</span></span>
- <span data-ttu-id="3c1d6-123">Tokeny OATH innej firmy</span><span class="sxs-lookup"><span data-stu-id="3c1d6-123">third-party OATH tokens</span></span>

<span data-ttu-id="3c1d6-124">Omówienie działania usługi Azure Multi-Factor Authentication można znaleźć w poniższym klipie wideo:</span><span class="sxs-lookup"><span data-stu-id="3c1d6-124">For an overview of how Azure Multi-Factor Authentication works see the following video:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

<span data-ttu-id="3c1d6-125">Aby uzyskać więcej informacji, zobacz [MFA dla usługi Office 365 i uwierzytelniania Wieloskładnikowego na platformie Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-125">For more information, see [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span></span>

## <a name="time-bound-privileges"></a><span data-ttu-id="3c1d6-126">Uprawnienia powiązane z czasu</span><span class="sxs-lookup"><span data-stu-id="3c1d6-126">Time-bound privileges</span></span>
<span data-ttu-id="3c1d6-127">W niektórych organizacjach może się okazać mają zbyt wielu użytkownikom wysoko uprzywilejowane ról.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-127">Some organizations may find that they have too many users in highly privileged roles.</span></span> <span data-ttu-id="3c1d6-128">Użytkownik mogły zostać dodane do roli dla danego działania, takie jak zalogowania się do usługi, ale nie był używany często później tych uprawnień.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-128">A user might have been added to the role for a particular activity, like to sign up for a service, but didn't use those privileges frequently afterward.</span></span>

<span data-ttu-id="3c1d6-129">Aby zmniejszyć czas ekspozycji uprawnień i zwiększyć Twojej wgląd w ich użycia, ograniczyć użytkownikom na pobieranie tylko na swoje uprawnienia "just in time" (JIT), których potrzebują do wykonania zadania.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-129">To lower the exposure time of privileges and increase your visibility into their use, limit users to only taking on their privileges "just in time" (JIT), when they need to perform a task.</span></span> <span data-ttu-id="3c1d6-130">W przypadku usługi Azure Active Directory i usług Online firmy Microsoft, można użyć [Azure AD Privileged Identity zarządzania (PIM)](http://aka.ms/AzurePIM).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-130">For Azure Active Directory and Microsoft Online Services, you can use [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).</span></span>

![Pulpit nawigacyjny usługi PIM][2]

## <a name="attack-detection"></a><span data-ttu-id="3c1d6-132">Wykrywanie ataków</span><span class="sxs-lookup"><span data-stu-id="3c1d6-132">Attack detection</span></span>
<span data-ttu-id="3c1d6-133">[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) udostępnia skonsolidowany wgląd w zdarzenia o podwyższonym ryzyku i potencjalnych luk w zabezpieczeniach wpływających na tożsamości organizacji.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-133">[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) provides a consolidated view into risk events and potential vulnerabilities affecting your organization’s identities.</span></span> <span data-ttu-id="3c1d6-134">Oparte na zdarzenia o podwyższonym ryzyku, Identity Protection oblicza poziom ryzyka użytkownika, dla każdego użytkownika, dzięki któremu można konfigurować zasady ryzyka, aby automatycznie chronić tożsamości organizacji.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-134">Based on risk events, Identity Protection calculates a user risk level for each user, enabling you to configure risk-based policies to automatically protect the identities of your organization.</span></span> <span data-ttu-id="3c1d6-135">Te zasady, oraz innych mechanizmów kontroli dostępu warunkowego zapewniane przez usługę Azure Active Directory i EMS, można automatycznie zablokować użytkownika lub udostępniania sugestii, obejmujące resetowanie haseł i wymuszania uwierzytelnianie wieloskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-135">These policies, along with other conditional access controls provided by Azure Active Directory and EMS, can automatically block the user or offer suggestions that include password resets and multi-factor authentication enforcement.</span></span>

![Usługa Azure AD Identity Protection][3]

## <a name="conditional-access"></a><span data-ttu-id="3c1d6-137">Dostęp warunkowy</span><span class="sxs-lookup"><span data-stu-id="3c1d6-137">Conditional access</span></span>
<span data-ttu-id="3c1d6-138">Z kontroli dostępu warunkowego usługi Azure Active Directory sprawdza określonych warunków, można wybrać podczas uwierzytelniania użytkownika, przed zezwoleniem na dostęp do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-138">With conditional access control, Azure Active Directory checks the specific conditions you choose when authenticating a user, before allowing access to an application.</span></span> <span data-ttu-id="3c1d6-139">Gdy te warunki są spełnione, użytkownik jest uwierzytelniony i zezwolenie na dostęp do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-139">Once those conditions are met, the user is authenticated and allowed access to the application.</span></span>

![Ustawienie zasad dostępu warunkowego za pomocą usługi MFA][4]

## <a name="related-articles"></a><span data-ttu-id="3c1d6-141">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="3c1d6-141">Related articles</span></span>
* <span data-ttu-id="3c1d6-142">Włącz [uwierzytelnianie wieloskładnikowe platformy Azure](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="3c1d6-142">Enable [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span></span>
* <span data-ttu-id="3c1d6-143">Włącz [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span><span class="sxs-lookup"><span data-stu-id="3c1d6-143">Enable [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span></span>
* <span data-ttu-id="3c1d6-144">Włącz [Azure AD Identity Protection](../active-directory-identityprotection.md)</span><span class="sxs-lookup"><span data-stu-id="3c1d6-144">Enable [Azure AD Identity Protection](../active-directory-identityprotection.md)</span></span>
* <span data-ttu-id="3c1d6-145">Włącz [kontroli dostępu warunkowego](../active-directory-conditional-access.md)</span><span class="sxs-lookup"><span data-stu-id="3c1d6-145">Enable [conditional access controls](../active-directory-conditional-access.md)</span></span>

<span data-ttu-id="3c1d6-146">Aby uzyskać więcej informacji na tworzeniu planu pełną zabezpieczeń, zobacz sekcję "obowiązki klienta i plan" [Microsoft Cloud Security dla architektów Enterprise](http://aka.ms/securecustomer) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-146">For more information on building a complete security roadmap, see the “Customer responsibilities and roadmap” section of the [Microsoft Cloud Security for Enterprise Architects](http://aka.ms/securecustomer) document.</span></span> <span data-ttu-id="3c1d6-147">Aby uzyskać więcej informacji na angażowaniu usług firmy Microsoft z dowolnego z tych tematów, skontaktuj się z przedstawicielem firmy Microsoft lub odwiedź nasze [strony rozwiązania bezpieczeństwa](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-147">For more information on engaging Microsoft services to assist with any of these topics, contact your Microsoft representative or visit our [Cybersecurity solutions page](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).</span></span>

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
