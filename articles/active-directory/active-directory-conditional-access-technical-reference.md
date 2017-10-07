---
title: "informacje techniczne dotyczące dostępu warunkowego usługi Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Z kontroli dostępu warunkowego usługi Azure Active Directory sprawdza hello określonych warunków, można wybrać podczas uwierzytelniania użytkownika hello i przed zezwoleniem na dostęp toohello aplikacji. Gdy te warunki są spełnione, użytkownik hello uwierzytelniony i dozwolone dostępu toohello aplikacji."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="ccdb3-104">Dokumentacja techniczna usługi Azure Active Directory dostępu warunkowego</span><span class="sxs-lookup"><span data-stu-id="ccdb3-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="ccdb3-105">Włączone przy użyciu dostępu warunkowego usługi</span><span class="sxs-lookup"><span data-stu-id="ccdb3-105">Services enabled with conditional access</span></span>

<span data-ttu-id="ccdb3-106">Zasady dostępu warunkowego są obsługiwane w wielu różnych typów aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="ccdb3-107">Ta lista zawiera:</span><span class="sxs-lookup"><span data-stu-id="ccdb3-107">This list includes:</span></span>


* <span data-ttu-id="ccdb3-108">Aplikacje zarejestrowane na powitania serwera Proxy aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="ccdb3-108">Applications registered with hello Azure Application Proxy</span></span>
* <span data-ttu-id="ccdb3-109">Usługa Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="ccdb3-109">Azure Remote App</span></span>
* <span data-ttu-id="ccdb3-110">Rozwinięte wiersz działalności biznesowej i aplikacje wielodostępne w zarejestrowany z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccdb3-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="ccdb3-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="ccdb3-111">Dynamics CRM</span></span>
* <span data-ttu-id="ccdb3-112">Aplikacji federacyjnych z galerii aplikacji hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccdb3-112">Federated applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="ccdb3-113">Yammer pakietu Microsoft Office 365</span><span class="sxs-lookup"><span data-stu-id="ccdb3-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="ccdb3-114">Microsoft Office 365 usługi Exchange Online</span><span class="sxs-lookup"><span data-stu-id="ccdb3-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="ccdb3-115">Microsoft Office 365 SharePoint Online (w tym usługi OneDrive dla firm)</span><span class="sxs-lookup"><span data-stu-id="ccdb3-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="ccdb3-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="ccdb3-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="ccdb3-117">Hasło logowania jednokrotnego aplikacje z galerii aplikacji hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccdb3-117">Password SSO applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="ccdb3-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="ccdb3-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="ccdb3-119">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ccdb3-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="ccdb3-120">Włącz zasady dostępu</span><span class="sxs-lookup"><span data-stu-id="ccdb3-120">Enable access rules</span></span>
<span data-ttu-id="ccdb3-121">Każda reguła może być włączona lub wyłączona na poszczególnych zasad aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="ccdb3-122">Jeśli zasady są **ON** one będzie włączony i egzekwowane dla użytkowników uzyskujących dostęp do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-122">When rules are **ON** they will be enabled and enforced for users accessing hello application.</span></span> <span data-ttu-id="ccdb3-123">Gdy są one **OFF** nie będą używane i zostanie nie wpływ hello logowania środowisko.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-123">When they are **OFF** they will not be used and will not impact hello users sign in experience.</span></span>

## <a name="applying-rules-toospecific-users"></a><span data-ttu-id="ccdb3-124">Stosowanie reguły toospecific użytkowników</span><span class="sxs-lookup"><span data-stu-id="ccdb3-124">Applying rules toospecific users</span></span>
<span data-ttu-id="ccdb3-125">Zasady mogą być zastosowane toospecific zbiorów użytkowników oparte na grupę zabezpieczeń, ustawiając **Zastosuj do**.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-125">Rules can be applied toospecific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="ccdb3-126">**Zastosuj do** można ustawić także**wszyscy użytkownicy** lub **grup**.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-126">**Apply To** can be set too**All Users** or **Groups**.</span></span> <span data-ttu-id="ccdb3-127">Gdy ustawiona zbyt**wszyscy użytkownicy** hello zasady będą stosowane tooany użytkownika z aplikacją toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-127">When set too**All Users** hello rules will apply tooany user with access toohello application.</span></span> <span data-ttu-id="ccdb3-128">Witaj **grup** opcja umożliwia zabezpieczeń i toobe grup dystrybucji zaznaczone, reguły będą wymuszane tylko dla tych grup.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-128">hello **Groups** option allows specific security and distribution groups toobe selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="ccdb3-129">W przypadku wdrażania reguły, jest często toofirst zastosowania określonych użytkowników, które są członkami grup pilotażowego.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-129">When deploying a rule,  it is common toofirst apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="ccdb3-130">Gdy reguła pełną hello może zostać zastosowana za**wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-130">Once complete hello rule can be applied too**All Users**.</span></span> <span data-ttu-id="ccdb3-131">Spowoduje to reguła hello toobe wymuszone dla wszystkich użytkowników w organizacji hello.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-131">This will cause hello rule toobe enforced for all users in hello organization.</span></span>

<span data-ttu-id="ccdb3-132">Wybierz grupy może również zostać wykluczony z zasad przy użyciu hello **z wyjątkiem** opcji.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-132">Select groups may also be exempted from policy using hello **Except** option.</span></span> <span data-ttu-id="ccdb3-133">Wszystkich członków tych grup będą zwolnione, nawet jeśli znajdują się w grupie uwzględnione.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="ccdb3-134">Sieci "w miejscu pracy"</span><span class="sxs-lookup"><span data-stu-id="ccdb3-134">“At work” networks</span></span>
<span data-ttu-id="ccdb3-135">Zasady dostępu warunkowego, korzystających z sieci "w miejscu pracy" zależą od zaufanych zakresów adresów IP, które zostały skonfigurowane w usłudze Azure AD, lub użycie hello "w sieci corpnet" oświadczeń z usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of hello "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="ccdb3-136">Do tych reguł należą:</span><span class="sxs-lookup"><span data-stu-id="ccdb3-136">These rules include:</span></span>

* <span data-ttu-id="ccdb3-137">Wymagaj uwierzytelniania wieloskładnikowego podczas nie podczas pracy</span><span class="sxs-lookup"><span data-stu-id="ccdb3-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="ccdb3-138">Blokowanie dostępu, gdy nie w pracy</span><span class="sxs-lookup"><span data-stu-id="ccdb3-138">Block access when not at work</span></span>

<span data-ttu-id="ccdb3-139">Określenie opcji sieci "w miejscu pracy"</span><span class="sxs-lookup"><span data-stu-id="ccdb3-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="ccdb3-140">Konfigurowanie zaufanych zakresów adresów IP w hello [strony konfiguracji uwierzytelniania wieloskładnikowego](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="ccdb3-140">Configure trusted IP address ranges in hello [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="ccdb3-141">Zasady dostępu warunkowego użyje zakresy hello skonfigurowane w każdej uwierzytelniania żądania i tokenu tooevaluate reguły wystawiania.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-141">Conditional Access policy will use hello configured ranges on each authentication request and token issuance tooevaluate rules.</span></span> 
2. <span data-ttu-id="ccdb3-142">Skonfiguruj używanie hello wewnątrz corpnet oświadczenia, ta opcja może być używany z katalogami federacyjnego, przy użyciu usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-142">Configure use of hello inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="ccdb3-143">toolearn więcej informacji na temat hello wewnątrz corpnet oświadczeń, zobacz [adresów IP Tusted](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="ccdb3-143">toolearn more about hello inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="ccdb3-144">Reguły oparte na czułości aplikacji</span><span class="sxs-lookup"><span data-stu-id="ccdb3-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="ccdb3-145">Reguły są konfigurowane dla poszczególnych aplikacji, umożliwiając toobe usługi wysokiej wartości hello zabezpieczone bez wpływu na usługi tooother dostępu.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-145">Rules are configured per application allowing hello high value services toobe secured without impacting access tooother services.</span></span> <span data-ttu-id="ccdb3-146">Można skonfigurować zasady dostępu warunkowego na powitania **Konfiguruj** kartę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-146">Conditional access rules can be configured on hello  **Configure** tab of hello application.</span></span> 

<span data-ttu-id="ccdb3-147">Zasady dostępne:</span><span class="sxs-lookup"><span data-stu-id="ccdb3-147">Rules currently offered:</span></span>

* <span data-ttu-id="ccdb3-148">**Wymagaj uwierzytelniania wieloskładnikowego**</span><span class="sxs-lookup"><span data-stu-id="ccdb3-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="ccdb3-149">Wszyscy użytkownicy czy te zasady są stosowane toowill być wymagane tooauthenticate za pośrednictwem usługi Multi-Factor authentication co najmniej raz.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-149">All users that this policy is applied toowill be required tooauthenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="ccdb3-150">**Wymagaj uwierzytelniania wieloskładnikowego podczas nie podczas pracy**</span><span class="sxs-lookup"><span data-stu-id="ccdb3-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="ccdb3-151">Jeśli ta zasada jest stosowana, wszyscy użytkownicy będzie wymagane toohave wykonać uwierzytelnianie wieloskładnikowe co najmniej raz, jeśli dostępu do usługi hello z lokalizacji zdalnej bez pracy.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-151">If this policy is applied, all users will be required toohave performed multi-factor authentication at least once if they access hello service from a non-work remote location.</span></span> <span data-ttu-id="ccdb3-152">Jeśli przechodzą z miejsca pracy tooremote, zostaną one tooperform wymagane uwierzytelnianie wieloskładnikowe podczas uzyskiwania dostępu do usługi hello.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-152">If they move from a work tooremote location, they will be required tooperform multifactor authentication when accessing hello service.</span></span>
* <span data-ttu-id="ccdb3-153">**Blokowanie dostępu, gdy nie w pracy**</span><span class="sxs-lookup"><span data-stu-id="ccdb3-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="ccdb3-154">Gdy użytkownik przeniesie z lokalizacji zdalnej tooa pracy, będą blokowani Jeśli hello "Blokowanie dostępu, gdy nie w pracy" zasady są stosowane toothem.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-154">When users move from work tooa remote location, they will be blocked if hello "Block access when not at work" policy is applied toothem.</span></span>  <span data-ttu-id="ccdb3-155">Ponownie zezwoleniem dostępu, gdy w miejscu pracy.</span><span class="sxs-lookup"><span data-stu-id="ccdb3-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="ccdb3-156">Powiązane tematy</span><span class="sxs-lookup"><span data-stu-id="ccdb3-156">Related topics</span></span>
* [<span data-ttu-id="ccdb3-157">Zabezpieczanie dostępu tooOffice 365 i innych aplikacji połączone tooAzure usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="ccdb3-157">Securing access tooOffice 365 and other apps connected tooAzure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="ccdb3-158">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ccdb3-158">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

