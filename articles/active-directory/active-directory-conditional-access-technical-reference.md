---
title: "Dokumentacja techniczna usługi Azure Active Directory dostępu warunkowego | Dokumentacja firmy Microsoft"
description: "Z kontroli dostępu warunkowego usługi Azure Active Directory sprawdza określonych warunków, można wybrać podczas uwierzytelniania użytkownika i przed zezwoleniem na dostęp do aplikacji. Gdy te warunki są spełnione, użytkownik jest uwierzytelniony i zezwolenie na dostęp do aplikacji."
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
ms.openlocfilehash: ca16a5399f94fd1ab267e0798cade3fd83f75b13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="59316-104">Dokumentacja techniczna usługi Azure Active Directory dostępu warunkowego</span><span class="sxs-lookup"><span data-stu-id="59316-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="59316-105">Włączone przy użyciu dostępu warunkowego usługi</span><span class="sxs-lookup"><span data-stu-id="59316-105">Services enabled with conditional access</span></span>

<span data-ttu-id="59316-106">Zasady dostępu warunkowego są obsługiwane w wielu różnych typów aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59316-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="59316-107">Ta lista zawiera:</span><span class="sxs-lookup"><span data-stu-id="59316-107">This list includes:</span></span>


* <span data-ttu-id="59316-108">Zarejestrowanych aplikacji przy użyciu serwera Proxy aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="59316-108">Applications registered with the Azure Application Proxy</span></span>
* <span data-ttu-id="59316-109">Usługa Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="59316-109">Azure Remote App</span></span>
* <span data-ttu-id="59316-110">Rozwinięte wiersz działalności biznesowej i aplikacje wielodostępne w zarejestrowany z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="59316-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="59316-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="59316-111">Dynamics CRM</span></span>
* <span data-ttu-id="59316-112">Aplikacji federacyjnych w galerii aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59316-112">Federated applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="59316-113">Yammer pakietu Microsoft Office 365</span><span class="sxs-lookup"><span data-stu-id="59316-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="59316-114">Microsoft Office 365 usługi Exchange Online</span><span class="sxs-lookup"><span data-stu-id="59316-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="59316-115">Microsoft Office 365 SharePoint Online (w tym usługi OneDrive dla firm)</span><span class="sxs-lookup"><span data-stu-id="59316-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="59316-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="59316-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="59316-117">Hasło logowania jednokrotnego aplikacje z galerii aplikacji Azure AD</span><span class="sxs-lookup"><span data-stu-id="59316-117">Password SSO applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="59316-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="59316-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="59316-119">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="59316-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="59316-120">Włącz zasady dostępu</span><span class="sxs-lookup"><span data-stu-id="59316-120">Enable access rules</span></span>
<span data-ttu-id="59316-121">Każda reguła może być włączona lub wyłączona na poszczególnych zasad aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59316-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="59316-122">Jeśli zasady są **ON** one będzie włączony i egzekwowane dla użytkowników uzyskujących dostęp do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59316-122">When rules are **ON** they will be enabled and enforced for users accessing the application.</span></span> <span data-ttu-id="59316-123">Gdy są one **OFF** nie będzie używany i nie ma wpływu na środowisko logowania użytkowników.</span><span class="sxs-lookup"><span data-stu-id="59316-123">When they are **OFF** they will not be used and will not impact the users sign in experience.</span></span>

## <a name="applying-rules-to-specific-users"></a><span data-ttu-id="59316-124">Stosowania zasad do określonych użytkowników</span><span class="sxs-lookup"><span data-stu-id="59316-124">Applying rules to specific users</span></span>
<span data-ttu-id="59316-125">Zasady można zastosować do określonych zestawów użytkowników oparte na grupę zabezpieczeń, ustawiając **Zastosuj do**.</span><span class="sxs-lookup"><span data-stu-id="59316-125">Rules can be applied to specific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="59316-126">**Zastosuj do** może być ustawiony na **wszyscy użytkownicy** lub **grup**.</span><span class="sxs-lookup"><span data-stu-id="59316-126">**Apply To** can be set to **All Users** or **Groups**.</span></span> <span data-ttu-id="59316-127">Jeśli wartość **wszyscy użytkownicy** zasady zostaną zastosowane do każdego użytkownika z dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59316-127">When set to **All Users** the rules will apply to any user with access to the application.</span></span> <span data-ttu-id="59316-128">**Grup** opcja umożliwia zabezpieczeń i grup dystrybucyjnych, należy wybrać tylko zostaną wymuszone zasady dla tych grup.</span><span class="sxs-lookup"><span data-stu-id="59316-128">The **Groups** option allows specific security and distribution groups to be selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="59316-129">W przypadku wdrażania reguły, jest często stosowanym rozwiązaniem najpierw zastosować go ograniczony zestaw użytkowników, które są członkami grup pilotażowego.</span><span class="sxs-lookup"><span data-stu-id="59316-129">When deploying a rule,  it is common to first apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="59316-130">Po wykonaniu tych czynności reguły mogą dotyczyć **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="59316-130">Once complete the rule can be applied to **All Users**.</span></span> <span data-ttu-id="59316-131">To spowoduje, że reguły mają być egzekwowane dla wszystkich użytkowników w organizacji.</span><span class="sxs-lookup"><span data-stu-id="59316-131">This will cause the rule to be enforced for all users in the organization.</span></span>

<span data-ttu-id="59316-132">Wybierz grupy może również zostać wykluczony z zasad przy użyciu opcji **z wyjątkiem** opcji.</span><span class="sxs-lookup"><span data-stu-id="59316-132">Select groups may also be exempted from policy using the **Except** option.</span></span> <span data-ttu-id="59316-133">Wszystkich członków tych grup będą zwolnione, nawet jeśli znajdują się w grupie uwzględnione.</span><span class="sxs-lookup"><span data-stu-id="59316-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="59316-134">Sieci "w miejscu pracy"</span><span class="sxs-lookup"><span data-stu-id="59316-134">“At work” networks</span></span>
<span data-ttu-id="59316-135">Zasady dostępu warunkowego, korzystających z sieci "w miejscu pracy" zależą od zaufanych zakresów adresów IP, które zostały skonfigurowane w usłudze Azure AD, lub użyj oświadczenia "wewnątrz corpnet" z usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="59316-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of the "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="59316-136">Do tych reguł należą:</span><span class="sxs-lookup"><span data-stu-id="59316-136">These rules include:</span></span>

* <span data-ttu-id="59316-137">Wymagaj uwierzytelniania wieloskładnikowego podczas nie podczas pracy</span><span class="sxs-lookup"><span data-stu-id="59316-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="59316-138">Blokowanie dostępu, gdy nie w pracy</span><span class="sxs-lookup"><span data-stu-id="59316-138">Block access when not at work</span></span>

<span data-ttu-id="59316-139">Określenie opcji sieci "w miejscu pracy"</span><span class="sxs-lookup"><span data-stu-id="59316-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="59316-140">Konfigurowanie zaufanych zakresy adresów IP w [strony konfiguracji uwierzytelniania wieloskładnikowego](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="59316-140">Configure trusted IP address ranges in the [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="59316-141">Zasady dostępu warunkowego użyje skonfigurowanych zakresów we wszystkich żądań uwierzytelnienia i wydawania tokenów do oceny zasad.</span><span class="sxs-lookup"><span data-stu-id="59316-141">Conditional Access policy will use the configured ranges on each authentication request and token issuance to evaluate rules.</span></span> 
2. <span data-ttu-id="59316-142">Skonfiguruj używanie wewnątrz oświadczeń corpnet tej opcji można użyć z katalogami federacyjnego, przy użyciu usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="59316-142">Configure use of the inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="59316-143">Aby dowiedzieć się więcej na temat wewnętrznej corpnet oświadczeń, zobacz [adresów IP Tusted](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="59316-143">To learn more about the inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="59316-144">Reguły oparte na czułości aplikacji</span><span class="sxs-lookup"><span data-stu-id="59316-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="59316-145">Reguły są konfigurowane dla poszczególnych aplikacji, dzięki czemu usługi wysokiej wartości być zabezpieczone bez wpływu na dostęp do innych usług.</span><span class="sxs-lookup"><span data-stu-id="59316-145">Rules are configured per application allowing the high value services to be secured without impacting access to other services.</span></span> <span data-ttu-id="59316-146">Można skonfigurować zasady dostępu warunkowego na **Konfiguruj** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59316-146">Conditional access rules can be configured on the  **Configure** tab of the application.</span></span> 

<span data-ttu-id="59316-147">Zasady dostępne:</span><span class="sxs-lookup"><span data-stu-id="59316-147">Rules currently offered:</span></span>

* <span data-ttu-id="59316-148">**Wymagaj uwierzytelniania wieloskładnikowego**</span><span class="sxs-lookup"><span data-stu-id="59316-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="59316-149">Wszyscy użytkownicy, których dotyczą te zasady do będzie wymagane do uwierzytelniania za pośrednictwem usługi Multi-Factor authentication co najmniej raz.</span><span class="sxs-lookup"><span data-stu-id="59316-149">All users that this policy is applied to will be required to authenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="59316-150">**Wymagaj uwierzytelniania wieloskładnikowego podczas nie podczas pracy**</span><span class="sxs-lookup"><span data-stu-id="59316-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="59316-151">Jeśli ta zasada jest stosowana, wszyscy użytkownicy będzie musiał wykonano uwierzytelnianie wieloskładnikowe w co najmniej raz, jeśli dostępu do usługi z lokalizacji zdalnej wolnych.</span><span class="sxs-lookup"><span data-stu-id="59316-151">If this policy is applied, all users will be required to have performed multi-factor authentication at least once if they access the service from a non-work remote location.</span></span> <span data-ttu-id="59316-152">Jeśli zostały przeniesione z pracy do zdalnej lokalizacji muszą przeprowadzać uwierzytelnianie wieloskładnikowe podczas uzyskiwania dostępu do usługi.</span><span class="sxs-lookup"><span data-stu-id="59316-152">If they move from a work to remote location, they will be required to perform multifactor authentication when accessing the service.</span></span>
* <span data-ttu-id="59316-153">**Blokowanie dostępu, gdy nie w pracy**</span><span class="sxs-lookup"><span data-stu-id="59316-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="59316-154">Gdy użytkownik przeniesie z pracy do zdalnej lokalizacji, będą blokowani Jeśli zastosowano zasady "Blokowanie dostępu, gdy nie w pracy" do nich.</span><span class="sxs-lookup"><span data-stu-id="59316-154">When users move from work to a remote location, they will be blocked if the "Block access when not at work" policy is applied to them.</span></span>  <span data-ttu-id="59316-155">Ponownie zezwoleniem dostępu, gdy w miejscu pracy.</span><span class="sxs-lookup"><span data-stu-id="59316-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="59316-156">Powiązane tematy</span><span class="sxs-lookup"><span data-stu-id="59316-156">Related topics</span></span>
* [<span data-ttu-id="59316-157">Zabezpieczanie dostępu do usługi Office 365 i innych aplikacji podłączone do usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59316-157">Securing access to Office 365 and other apps connected to Azure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="59316-158">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59316-158">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

