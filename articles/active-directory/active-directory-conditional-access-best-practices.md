---
title: "aaaBest rozwiązań dla dostępu warunkowego w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Co to jest się, że należy unikać zrobić podczas konfigurowania zasad dostępu warunkowego i Dowiedz się więcej o rzeczy, o których należy wiedzieć."
services: active-directory
keywords: "tooapps dostępu warunkowego, dostępu warunkowego z usługą Azure AD, bezpieczny dostęp do zasobów toocompany, zasady dostępu warunkowego"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="af706-104">Najlepsze rozwiązania dotyczące dostępu warunkowego w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af706-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="af706-105">Ten temat zawiera informacje o rzeczy, o których należy wiedzieć, i jakie są się, że należy unikać zrobić podczas konfigurowania zasad dostępu warunkowego.</span><span class="sxs-lookup"><span data-stu-id="af706-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="af706-106">Przed przeczytaniem tego tematu, należy się zapoznać z hello pojęcia i terminologia hello określone w [dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="af706-106">Before reading this topic, you should familiarize yourself with hello concepts and hello terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="af706-107">Co należy wiedzieć</span><span class="sxs-lookup"><span data-stu-id="af706-107">What you should know</span></span>

### <a name="whats-required-toomake-a-policy-work"></a><span data-ttu-id="af706-108">Co to są wymagane toomake pracy zasady?</span><span class="sxs-lookup"><span data-stu-id="af706-108">What’s required toomake a policy work?</span></span>

<span data-ttu-id="af706-109">Podczas tworzenia nowych zasad nie ma żadnych użytkowników, grup, aplikacji ani wybrane kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="af706-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![Aplikacje w chmurze](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="af706-111">Praca z zasadami toomake, należy skonfigurować następujące hello:</span><span class="sxs-lookup"><span data-stu-id="af706-111">toomake your policy work, you must configure hello following:</span></span>


|<span data-ttu-id="af706-112">Co</span><span class="sxs-lookup"><span data-stu-id="af706-112">What</span></span>           | <span data-ttu-id="af706-113">Jak</span><span class="sxs-lookup"><span data-stu-id="af706-113">How</span></span>                                  | <span data-ttu-id="af706-114">Dlaczego</span><span class="sxs-lookup"><span data-stu-id="af706-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="af706-115">**Aplikacje w chmurze**</span><span class="sxs-lookup"><span data-stu-id="af706-115">**Cloud apps**</span></span> |<span data-ttu-id="af706-116">Należy tooselect co najmniej jedną aplikację.</span><span class="sxs-lookup"><span data-stu-id="af706-116">You need tooselect one or more apps.</span></span>  | <span data-ttu-id="af706-117">Celem Hello zasady dostępu warunkowego jest tooenable toofine strojenia jak autoryzowani użytkownicy mają dostęp do Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="af706-117">hello goal of a conditional access policy is tooenable you toofine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="af706-118">**Użytkownicy i grupy**</span><span class="sxs-lookup"><span data-stu-id="af706-118">**Users and groups**</span></span> | <span data-ttu-id="af706-119">Należy tooselect co najmniej jednego użytkownika lub grupę, która jest autoryzowany wybrane aplikacje w chmurze hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="af706-119">You need tooselect at least one user or group that is authorized tooaccess hello cloud apps you have selected.</span></span> | <span data-ttu-id="af706-120">Zasady dostępu warunkowego, który nie ma użytkowników i grupy przypisane, nigdy nie zostanie wywołany.</span><span class="sxs-lookup"><span data-stu-id="af706-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="af706-121">**Kontrola dostępu**</span><span class="sxs-lookup"><span data-stu-id="af706-121">**Access controls**</span></span> | <span data-ttu-id="af706-122">Należy tooselect co najmniej jeden kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="af706-122">You need tooselect at least one access control.</span></span> | <span data-ttu-id="af706-123">Procesor zasady musi tooknow jakie toodo Jeśli warunki są spełnione.</span><span class="sxs-lookup"><span data-stu-id="af706-123">Your policy processor needs tooknow what toodo if your conditions are satisfied.</span></span>|


<span data-ttu-id="af706-124">W przypadku dodawania toothese podstawowych wymagań, w wielu przypadkach należy także skonfigurować warunek.</span><span class="sxs-lookup"><span data-stu-id="af706-124">In addition toothese basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="af706-125">Gdy zasady również będzie działać bez skonfigurowanego warunku, warunki są hello współczynnik pobudzenie Dostrajanie aplikacji tooyour dostępu.</span><span class="sxs-lookup"><span data-stu-id="af706-125">While a policy would also work without a configured condition, conditions are hello driving factor for fine-tuning access tooyour apps.</span></span>


![Aplikacje w chmurze](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="af706-127">Jak są analizowane przypisania</span><span class="sxs-lookup"><span data-stu-id="af706-127">How are assignments evaluated?</span></span>

<span data-ttu-id="af706-128">Wszystkie przypisania są logicznie **and**.</span><span class="sxs-lookup"><span data-stu-id="af706-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="af706-129">Jeśli masz więcej niż jeden przypisania skonfigurowane, tootrigger zasady, muszą być spełnione wszystkie przypisania.</span><span class="sxs-lookup"><span data-stu-id="af706-129">If you have more than one assignment configured, tootrigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="af706-130">Tooconfigure lokalizacji warunek, który dotyczy połączeń tooall z poza siecią organizacji, należy można osiągnąć to przez:</span><span class="sxs-lookup"><span data-stu-id="af706-130">If you need tooconfigure a location condition that applies tooall connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="af706-131">W tym **wszystkich lokalizacji**</span><span class="sxs-lookup"><span data-stu-id="af706-131">Including **All locations**</span></span>
- <span data-ttu-id="af706-132">Z wyjątkiem **wszystkich zaufanych adresów IP**</span><span class="sxs-lookup"><span data-stu-id="af706-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="af706-133">Co się stanie, jeśli masz zasady w hello klasycznego portalu Azure i portalu Azure skonfigurowane?</span><span class="sxs-lookup"><span data-stu-id="af706-133">What happens if you have policies in hello Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="af706-134">Obie zasady są wymuszane przez usługę Azure Active Directory i hello użytkownik uzyskuje dostęp tylko wtedy, gdy są spełnione wszystkie wymagania.</span><span class="sxs-lookup"><span data-stu-id="af706-134">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a><span data-ttu-id="af706-135">Co się stanie, jeśli masz zasady w hello portalu Intune Silverlight i hello Azure Portal?</span><span class="sxs-lookup"><span data-stu-id="af706-135">What happens if you have policies in hello Intune Silverlight portal and hello Azure Portal?</span></span>
<span data-ttu-id="af706-136">Obie zasady są wymuszane przez usługę Azure Active Directory i hello użytkownik uzyskuje dostęp tylko wtedy, gdy są spełnione wszystkie wymagania.</span><span class="sxs-lookup"><span data-stu-id="af706-136">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a><span data-ttu-id="af706-137">Co się stanie, jeśli wiele zasad dla tego samego użytkownika skonfigurowane hello?</span><span class="sxs-lookup"><span data-stu-id="af706-137">What happens if I have multiple policies for hello same user configured?</span></span>  
<span data-ttu-id="af706-138">Dla każdego logowania Azure Active Directory ocenia wszystkie zasady i zapewnia, że przed przyznany dostęp użytkownika toohello spełnione są wszystkie wymagania.</span><span class="sxs-lookup"><span data-stu-id="af706-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access toohello user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="af706-139">Dostęp warunkowy działa z programem Exchange ActiveSync?</span><span class="sxs-lookup"><span data-stu-id="af706-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="af706-140">Tak, można użyć programu Exchange ActiveSync w zasadach dostępu warunkowego.</span><span class="sxs-lookup"><span data-stu-id="af706-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="af706-141">Co należy zrobić</span><span class="sxs-lookup"><span data-stu-id="af706-141">What you should avoid doing</span></span>

<span data-ttu-id="af706-142">Witaj dostępu warunkowego framework zapewnia elastyczność dużą konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="af706-142">hello conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="af706-143">Jednak dużą elastyczność oznacza również należy dokładnie przejrzeć każdej konfiguracji zasad przed tooreleasing go tooavoid niepożądane wyniki.</span><span class="sxs-lookup"><span data-stu-id="af706-143">However, great flexibility  also means that you should carefully review each configuration policy prior tooreleasing it tooavoid undesirable results.</span></span> <span data-ttu-id="af706-144">W tym kontekście, trzeba zwrócić szczególną uwagę tooassignments wpływających na zestawy, takie jak **wszyscy użytkownicy / grupy / aplikacji w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="af706-144">In this context, you should pay special attention tooassignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="af706-145">W środowisku należy unikać hello następujące konfiguracje:</span><span class="sxs-lookup"><span data-stu-id="af706-145">In your environment, you should avoid hello following configurations:</span></span>


<span data-ttu-id="af706-146">**Dla wszystkich użytkowników wszystkich aplikacji w chmurze:**</span><span class="sxs-lookup"><span data-stu-id="af706-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="af706-147">**Blokowanie dostępu** — ta konfiguracja zablokuje całej organizacji, który ostatecznie nie jest dobrym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="af706-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="af706-148">**Wymagają zgodnego urządzenia** — dla użytkowników, która nie zarejestrowali swoich urządzeń, ale ta zasada blokuje dostęp w tym portalu Intune toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="af706-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access toohello Intune portal.</span></span> <span data-ttu-id="af706-149">Jeśli jesteś administratorem bez zarejestrowanego urządzenia te zasady blokuje powrót do hello Azure toochange portalu hello zasad.</span><span class="sxs-lookup"><span data-stu-id="af706-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into hello Azure portal toochange hello policy.</span></span>

- <span data-ttu-id="af706-150">**Wymagane było przyłączenie do domeny** — ten blok zasady dostępu ma również hello potencjalne tooblock dostęp dla wszystkich użytkowników w organizacji, jeśli nie masz jeszcze urządzenia przyłączone do domeny.</span><span class="sxs-lookup"><span data-stu-id="af706-150">**Require domain join** - This policy block access has also hello potential tooblock access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="af706-151">**Dla wszystkich użytkowników, wszystkie aplikacje w chmurze, wszystkie platformy urządzeń:**</span><span class="sxs-lookup"><span data-stu-id="af706-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="af706-152">**Blokowanie dostępu** — ta konfiguracja zablokuje całej organizacji, który ostatecznie nie jest dobrym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="af706-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="af706-153">Typowe scenariusze</span><span class="sxs-lookup"><span data-stu-id="af706-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="af706-154">Wymagania uwierzytelniania wieloskładnikowego dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="af706-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="af706-155">Wiele środowisk ma aplikacje wymagające wyższego poziomu ochrony niż hello innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="af706-155">Many environments have apps requiring a higher level of protection than hello others.</span></span>
<span data-ttu-id="af706-156">Jest to, na przykład w przypadku aplikacji, które mają dostęp do danych toosensitive hello.</span><span class="sxs-lookup"><span data-stu-id="af706-156">This is, for example, hello case for apps that have access toosensitive data.</span></span>
<span data-ttu-id="af706-157">Jeśli chcesz tooadd kolejną warstwę ochrony toothese aplikacji, można skonfigurować zasady dostępu warunkowego, która wymaga usługi Multi-Factor authentication, gdy użytkownicy uzyskują dostęp do tych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="af706-157">If you want tooadd another layer of protection toothese apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="af706-158">Wymagania uwierzytelniania wieloskładnikowego dla dostępu z sieci, które nie są zaufane</span><span class="sxs-lookup"><span data-stu-id="af706-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="af706-159">Ten scenariusz jest podobne toohello poprzednim scenariuszu, ponieważ powoduje ona dodanie wymaganie uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="af706-159">This scenario is similar toohello previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="af706-160">Główna różnica hello jest jednak warunek hello tego wymagania.</span><span class="sxs-lookup"><span data-stu-id="af706-160">However, hello main difference is hello condition for this requirement.</span></span>  
<span data-ttu-id="af706-161">Podczas hello fokus poprzednim scenariuszu hello na aplikacje z danymi toosensitve dostępu hello w tym scenariuszu koncentruje się na zaufanych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="af706-161">While hello focus of hello previous scenario was on apps with access toosensitve data, hello focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="af706-162">Innymi słowy może być wymagane uwierzytelnianie wieloskładnikowe, jeśli aplikacja jest dostępna przez użytkownika z sieci, której nie ufasz.</span><span class="sxs-lookup"><span data-stu-id="af706-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="af706-163">Tylko zaufane urządzenia mają dostęp do usług Office 365</span><span class="sxs-lookup"><span data-stu-id="af706-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="af706-164">Jeśli używasz usługi Intune w danym środowisku, mogą natychmiast rozpocząć korzystanie hello interfejs zasad dostępu warunkowego w hello konsoli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="af706-164">If you are using Intune in your environment, you can immediately start using hello conditional access policy interface in hello Azure console.</span></span>

<span data-ttu-id="af706-165">Wielu klientów usługi Intune korzystają z dostępu warunkowego tooensure, że tylko zaufane urządzenia mają dostęp do usług Office 365.</span><span class="sxs-lookup"><span data-stu-id="af706-165">Many Intune customers are using conditional access tooensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="af706-166">Oznacza to, że urządzenia przenośne zarejestrowane w usłudze Intune i spełnić wymagania zasad zgodności oraz czy komputery z systemem Windows są tooan przyłączone do domeny lokalnej.</span><span class="sxs-lookup"><span data-stu-id="af706-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined tooan on-premises domain.</span></span> <span data-ttu-id="af706-167">Poprawy klucza jest, że nie masz tooset hello te same zasady dla każdej z usług hello usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="af706-167">A key improvement is that you do not have tooset hello same policy for each of hello Office 365 services.</span></span>  <span data-ttu-id="af706-168">Podczas tworzenia nowych zasad konfigurowania hello chmury aplikacji tooinclude każdej aplikacji hello usługi Office 365, które mają tooprotect z przy użyciu dostępu warunkowego.</span><span class="sxs-lookup"><span data-stu-id="af706-168">When you create a new policy, configure hello Cloud apps tooinclude each of hello O365 apps that you wish tooprotect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af706-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="af706-169">Next steps</span></span>

<span data-ttu-id="af706-170">Jeśli chcesz, aby tooknow tooconfigure zasady dostępu warunkowego, zobacz temat [wprowadzenie dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="af706-170">If you want tooknow how tooconfigure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
