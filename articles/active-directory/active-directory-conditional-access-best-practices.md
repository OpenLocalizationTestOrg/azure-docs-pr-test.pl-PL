---
title: "Najlepsze rozwiązania dla dostępu warunkowego w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Co to jest się, że należy unikać zrobić podczas konfigurowania zasad dostępu warunkowego i Dowiedz się więcej o rzeczy, o których należy wiedzieć."
services: active-directory
keywords: "dostęp warunkowy do aplikacji, dostęp warunkowy przy użyciu usługi Azure AD, bezpieczny dostęp do zasobów firmy, zasady dostępu warunkowego"
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
ms.openlocfilehash: 3e524c116479c1af6eb6a601c9b57d27a697c5a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="5b1e7-104">Najlepsze rozwiązania dotyczące dostępu warunkowego w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b1e7-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="5b1e7-105">Ten temat zawiera informacje o rzeczy, o których należy wiedzieć, i jakie są się, że należy unikać zrobić podczas konfigurowania zasad dostępu warunkowego.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="5b1e7-106">Przed przeczytaniem tego tematu, należy zapoznać się z pojęciami i terminologii określone w [dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5b1e7-106">Before reading this topic, you should familiarize yourself with the concepts and the terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="5b1e7-107">Co należy wiedzieć</span><span class="sxs-lookup"><span data-stu-id="5b1e7-107">What you should know</span></span>

### <a name="whats-required-to-make-a-policy-work"></a><span data-ttu-id="5b1e7-108">Co to są wymagane do zmiany celu zasad pracy?</span><span class="sxs-lookup"><span data-stu-id="5b1e7-108">What’s required to make a policy work?</span></span>

<span data-ttu-id="5b1e7-109">Podczas tworzenia nowych zasad nie ma żadnych użytkowników, grup, aplikacji ani wybrane kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![Aplikacje w chmurze](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="5b1e7-111">Aby działać zgodnie z zasadami, należy skonfigurować następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="5b1e7-111">To make your policy work, you must configure the following:</span></span>


|<span data-ttu-id="5b1e7-112">Co</span><span class="sxs-lookup"><span data-stu-id="5b1e7-112">What</span></span>           | <span data-ttu-id="5b1e7-113">Jak</span><span class="sxs-lookup"><span data-stu-id="5b1e7-113">How</span></span>                                  | <span data-ttu-id="5b1e7-114">Dlaczego</span><span class="sxs-lookup"><span data-stu-id="5b1e7-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="5b1e7-115">**Aplikacje w chmurze**</span><span class="sxs-lookup"><span data-stu-id="5b1e7-115">**Cloud apps**</span></span> |<span data-ttu-id="5b1e7-116">Musisz wybrać co najmniej jedną aplikację.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-116">You need to select one or more apps.</span></span>  | <span data-ttu-id="5b1e7-117">Celem zasad dostępu warunkowego jest umożliwiają dostrojenie jak autoryzowani użytkownicy mają dostęp do Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-117">The goal of a conditional access policy is to enable you to fine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="5b1e7-118">**Użytkownicy i grupy**</span><span class="sxs-lookup"><span data-stu-id="5b1e7-118">**Users and groups**</span></span> | <span data-ttu-id="5b1e7-119">Musisz wybrać co najmniej jednego użytkownika lub grupę, który jest upoważniony do dostępu do aplikacji w chmurze, który wybrano.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-119">You need to select at least one user or group that is authorized to access the cloud apps you have selected.</span></span> | <span data-ttu-id="5b1e7-120">Zasady dostępu warunkowego, który nie ma użytkowników i grupy przypisane, nigdy nie zostanie wywołany.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="5b1e7-121">**Kontrola dostępu**</span><span class="sxs-lookup"><span data-stu-id="5b1e7-121">**Access controls**</span></span> | <span data-ttu-id="5b1e7-122">Musisz wybrać kontroli dostępu co najmniej jeden.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-122">You need to select at least one access control.</span></span> | <span data-ttu-id="5b1e7-123">Procesor zasady musi wiedzieć, co należy zrobić, jeśli warunki są spełnione.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-123">Your policy processor needs to know what to do if your conditions are satisfied.</span></span>|


<span data-ttu-id="5b1e7-124">Oprócz podstawowych wymagań w wielu przypadkach należy także skonfigurować warunek.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-124">In addition to these basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="5b1e7-125">Gdy zasady również będzie działać bez skonfigurowanego warunku, warunki są pobudzenie współczynnik dostrajanie dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-125">While a policy would also work without a configured condition, conditions are the driving factor for fine-tuning access to your apps.</span></span>


![Aplikacje w chmurze](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="5b1e7-127">Jak są analizowane przypisania</span><span class="sxs-lookup"><span data-stu-id="5b1e7-127">How are assignments evaluated?</span></span>

<span data-ttu-id="5b1e7-128">Wszystkie przypisania są logicznie **and**.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="5b1e7-129">Jeśli masz więcej niż jednego przypisania skonfigurowany, aby wyzwolić zasady, wszystkie przypisania muszą być spełnione.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-129">If you have more than one assignment configured, to trigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="5b1e7-130">Jeśli potrzebujesz Konfigurowanie warunku lokalizacji, która ma zastosowanie do wszystkich połączeń z poza siecią organizacji, można wykonać to przez:</span><span class="sxs-lookup"><span data-stu-id="5b1e7-130">If you need to configure a location condition that applies to all connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="5b1e7-131">W tym **wszystkich lokalizacji**</span><span class="sxs-lookup"><span data-stu-id="5b1e7-131">Including **All locations**</span></span>
- <span data-ttu-id="5b1e7-132">Z wyjątkiem **wszystkich zaufanych adresów IP**</span><span class="sxs-lookup"><span data-stu-id="5b1e7-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-the-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="5b1e7-133">Co się stanie, jeśli masz zasady w klasycznym portalu Azure i portalu Azure skonfigurowane?</span><span class="sxs-lookup"><span data-stu-id="5b1e7-133">What happens if you have policies in the Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="5b1e7-134">Obie zasady są wymuszane przez usługę Azure Active Directory, a użytkownik uzyskuje dostęp tylko wtedy, gdy są spełnione wszystkie wymagania.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-134">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-the-intune-silverlight-portal-and-the-azure-portal"></a><span data-ttu-id="5b1e7-135">Co się stanie, jeśli masz zasady w portalu usługi Intune Silverlight i portalu Azure?</span><span class="sxs-lookup"><span data-stu-id="5b1e7-135">What happens if you have policies in the Intune Silverlight portal and the Azure Portal?</span></span>
<span data-ttu-id="5b1e7-136">Obie zasady są wymuszane przez usługę Azure Active Directory, a użytkownik uzyskuje dostęp tylko wtedy, gdy są spełnione wszystkie wymagania.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-136">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-the-same-user-configured"></a><span data-ttu-id="5b1e7-137">Co się dzieje w przypadku wielu zasad dla tego samego użytkownika skonfigurowane?</span><span class="sxs-lookup"><span data-stu-id="5b1e7-137">What happens if I have multiple policies for the same user configured?</span></span>  
<span data-ttu-id="5b1e7-138">Dla każdego logowania Azure Active Directory ocenia wszystkie zasady i zapewnia, że przed udzielony dostęp do użytkownika spełniono wszystkie wymagania.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access to the user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="5b1e7-139">Dostęp warunkowy działa z programem Exchange ActiveSync?</span><span class="sxs-lookup"><span data-stu-id="5b1e7-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="5b1e7-140">Tak, można użyć programu Exchange ActiveSync w zasadach dostępu warunkowego.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="5b1e7-141">Co należy zrobić</span><span class="sxs-lookup"><span data-stu-id="5b1e7-141">What you should avoid doing</span></span>

<span data-ttu-id="5b1e7-142">Dostęp warunkowy framework zapewnia elastyczność dużą konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-142">The conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="5b1e7-143">Jednak elastyczność oznacza także, należy dokładnie przejrzeć wszystkie zasady konfiguracji przed zwalniania go, aby uniknąć niepożądane wyniki.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-143">However, great flexibility  also means that you should carefully review each configuration policy prior to releasing it to avoid undesirable results.</span></span> <span data-ttu-id="5b1e7-144">W tym kontekście, należy zwrócić szczególną uwagę na przydziały wpływające na zestawy, takie jak **wszyscy użytkownicy / grupy / aplikacji w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-144">In this context, you should pay special attention to assignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="5b1e7-145">W środowisku należy unikać następujące konfiguracje:</span><span class="sxs-lookup"><span data-stu-id="5b1e7-145">In your environment, you should avoid the following configurations:</span></span>


<span data-ttu-id="5b1e7-146">**Dla wszystkich użytkowników wszystkich aplikacji w chmurze:**</span><span class="sxs-lookup"><span data-stu-id="5b1e7-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="5b1e7-147">**Blokowanie dostępu** — ta konfiguracja zablokuje całej organizacji, który ostatecznie nie jest dobrym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="5b1e7-148">**Wymagają zgodnego urządzenia** — dla użytkowników, która nie zarejestrowali swoich urządzeń, ale ta zasada blokuje dostęp tym do uzyskiwania dostępu do portalu usługi Intune.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access to the Intune portal.</span></span> <span data-ttu-id="5b1e7-149">Jeśli jesteś administratorem bez zarejestrowanego urządzenia te zasady blokuje powrót do portalu Azure do zmiany zasad.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into the Azure portal to change the policy.</span></span>

- <span data-ttu-id="5b1e7-150">**Wymagane było przyłączenie do domeny** — ten blok zasady dostępu ma również możliwość zablokowania dostępu dla wszystkich użytkowników w organizacji, jeśli nie masz jeszcze urządzenia przyłączone do domeny.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-150">**Require domain join** - This policy block access has also the potential to block access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="5b1e7-151">**Dla wszystkich użytkowników, wszystkie aplikacje w chmurze, wszystkie platformy urządzeń:**</span><span class="sxs-lookup"><span data-stu-id="5b1e7-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="5b1e7-152">**Blokowanie dostępu** — ta konfiguracja zablokuje całej organizacji, który ostatecznie nie jest dobrym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="5b1e7-153">Typowe scenariusze</span><span class="sxs-lookup"><span data-stu-id="5b1e7-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="5b1e7-154">Wymagania uwierzytelniania wieloskładnikowego dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="5b1e7-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="5b1e7-155">Wiele środowisk ma aplikacje wymagające wyższego poziomu ochrony od innych.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-155">Many environments have apps requiring a higher level of protection than the others.</span></span>
<span data-ttu-id="5b1e7-156">Jest to, na przykład w przypadku aplikacji, które mają dostęp do poufnych danych.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-156">This is, for example, the case for apps that have access to sensitive data.</span></span>
<span data-ttu-id="5b1e7-157">Jeśli chcesz dodać kolejną warstwę ochrony do tych aplikacji, można skonfigurować zasady dostępu warunkowego, która wymaga usługi Multi-Factor authentication, gdy użytkownicy uzyskują dostęp do tych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-157">If you want to add another layer of protection to these apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="5b1e7-158">Wymagania uwierzytelniania wieloskładnikowego dla dostępu z sieci, które nie są zaufane</span><span class="sxs-lookup"><span data-stu-id="5b1e7-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="5b1e7-159">Ten scenariusz jest podobny do poprzedniego scenariusza, ponieważ powoduje ona dodanie wymaganie uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-159">This scenario is similar to the previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="5b1e7-160">Główną różnicą jest jednak warunek tego wymagania.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-160">However, the main difference is the condition for this requirement.</span></span>  
<span data-ttu-id="5b1e7-161">Podczas na aplikacje z dostępem do danych sensitve fokus poprzedniego scenariusza, w tym scenariuszu koncentruje się na zaufanych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-161">While the focus of the previous scenario was on apps with access to sensitve data, the focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="5b1e7-162">Innymi słowy może być wymagane uwierzytelnianie wieloskładnikowe, jeśli aplikacja jest dostępna przez użytkownika z sieci, której nie ufasz.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="5b1e7-163">Tylko zaufane urządzenia mają dostęp do usług Office 365</span><span class="sxs-lookup"><span data-stu-id="5b1e7-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="5b1e7-164">Jeśli używasz usługi Intune w danym środowisku, mogą natychmiast rozpocząć korzystanie interfejs zasad dostępu warunkowego w konsoli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-164">If you are using Intune in your environment, you can immediately start using the conditional access policy interface in the Azure console.</span></span>

<span data-ttu-id="5b1e7-165">Wielu klientów usługi Intune są przy użyciu dostępu warunkowego, aby upewnić się, że tylko zaufane urządzenia mają dostęp do usług Office 365.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-165">Many Intune customers are using conditional access to ensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="5b1e7-166">Oznacza to, że urządzenia przenośne zarejestrowane w usłudze Intune i spełnić wymagania zasad zgodności i że komputery z systemem Windows są przyłączone do domeny lokalnej.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined to an on-premises domain.</span></span> <span data-ttu-id="5b1e7-167">Poprawy klucza jest, że nie trzeba ustawić te same zasady dla każdej usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-167">A key improvement is that you do not have to set the same policy for each of the Office 365 services.</span></span>  <span data-ttu-id="5b1e7-168">Podczas tworzenia nowych zasad konfigurowania aplikacji w chmurze uwzględnienie wszystkich aplikacji usługi Office 365, które chcesz chronić za pomocą przy użyciu dostępu warunkowego.</span><span class="sxs-lookup"><span data-stu-id="5b1e7-168">When you create a new policy, configure the Cloud apps to include each of the O365 apps that you wish to protect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b1e7-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5b1e7-169">Next steps</span></span>

<span data-ttu-id="5b1e7-170">Jeśli chcesz wiedzieć, jak skonfigurować zasady dostępu warunkowego, zobacz [wprowadzenie dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5b1e7-170">If you want to know how to configure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
