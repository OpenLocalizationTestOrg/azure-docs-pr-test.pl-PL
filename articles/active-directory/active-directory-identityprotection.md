---
title: "Ochronę tożsamości usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Azure AD Identity Protection umożliwia ograniczenie możliwości osoby atakującej, która wykorzystać, którego bezpieczeństwo zostało naruszone tożsamości lub urządzenie i secure tożsamości lub urządzeń, które wcześniej podejrzenia lub znane naruszenia."
services: active-directory
keywords: "ochronę tożsamości usługi Azure active directory, usługa cloud app discovery, zarządzanie aplikacjami, zabezpieczeń, ryzyka, poziom ryzyka, luki w zabezpieczeniach, zasady zabezpieczeń"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 0c7a8d68c0df729441e3f7faa5cd06066db1261d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="2475c-104">Ochrona tożsamości w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2475c-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="2475c-105">Azure Active Directory Identity Protection to funkcja wersji Azure AD Premium P2, które umożliwia:</span><span class="sxs-lookup"><span data-stu-id="2475c-105">Azure Active Directory Identity Protection is a feature of the Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="2475c-106">Wykrywanie potencjalnych luk w zabezpieczeniach wpływających na tożsamości organizacji</span><span class="sxs-lookup"><span data-stu-id="2475c-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="2475c-107">Skonfiguruj automatyczne odpowiedzi wykrytych podejrzanych działań, które są związane z tożsamości organizacji</span><span class="sxs-lookup"><span data-stu-id="2475c-107">Configure automated responses to detected suspicious actions that are related to your organization’s identities</span></span>  

- <span data-ttu-id="2475c-108">Zbadaj podejrzane zdarzeń i podejmij odpowiednią akcję, aby je rozwiązać</span><span class="sxs-lookup"><span data-stu-id="2475c-108">Investigate suspicious incidents and take appropriate action to resolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="2475c-109">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="2475c-109">Getting started</span></span>

<span data-ttu-id="2475c-110">Firma Microsoft zabezpiecza oparte na chmurze tożsamości przez ponad dekadę.</span><span class="sxs-lookup"><span data-stu-id="2475c-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="2475c-111">Z usługi Azure Active Directory Identity Protection w danym środowisku, można użyć tego samego systemy ochrony, wykorzystywane przez firmę Microsoft do zabezpieczania tożsamości.</span><span class="sxs-lookup"><span data-stu-id="2475c-111">With Azure Active Directory Identity Protection, in your environment, you can use the same protection systems Microsoft uses to secure identities.</span></span>

<span data-ttu-id="2475c-112">Większość naruszeń zabezpieczeń ma miejsce, gdy osoby atakujące uzyskania dostępu do środowiska kradzieży tożsamości użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2475c-112">The vast majority of security breaches take place when attackers gain access to an environment by stealing a user’s identity.</span></span> <span data-ttu-id="2475c-113">Całościowo osoby atakujące stały się coraz bardziej skuteczne w wykorzystaniu naruszeń innych firm i za pomocą zaawansowanej wyłudzania.</span><span class="sxs-lookup"><span data-stu-id="2475c-113">Over the years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="2475c-114">Jak osoba atakująca uzyska dostęp do nawet niski uprzywilejowanych kont, jest względnie łatwe uzyskanie dostępu do zasobów firmy ważne za pośrednictwem penetracji sieci.</span><span class="sxs-lookup"><span data-stu-id="2475c-114">As soon as an attacker gains access to even low privileged user accounts, it is relatively easy for them to gain access to important company resources through lateral movement.</span></span>

<span data-ttu-id="2475c-115">W wyniku tego należy:</span><span class="sxs-lookup"><span data-stu-id="2475c-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="2475c-116">Ochrona wszystkich tożsamości, niezależnie od ich poziom uprawnień</span><span class="sxs-lookup"><span data-stu-id="2475c-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="2475c-117">Aktywne uniemożliwić złamany tożsamości są użyte</span><span class="sxs-lookup"><span data-stu-id="2475c-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="2475c-118">Odnajdywanie złamany tożsamości jest bez łatwe zadania.</span><span class="sxs-lookup"><span data-stu-id="2475c-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="2475c-119">Azure Active Directory korzysta z algorytmów uczenia maszynowego adaptacyjną i heurystyki w celu wykrycia nieprawidłowości i podejrzane zdarzenia, które wskazują potencjalnie naruszony tożsamości.</span><span class="sxs-lookup"><span data-stu-id="2475c-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="2475c-120">Przy użyciu tych danych, Identity Protection generuje raporty i alerty, które pozwalają ocenić wykrytych problemów i podjąć odpowiednie środki zaradcze lub akcji korygowania.</span><span class="sxs-lookup"><span data-stu-id="2475c-120">Using this data, Identity Protection generates reports and alerts that enable you to evaluate the detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="2475c-121">Azure Active Directory Identity Protection jest większa niż monitorowania i raportowania narzędzia.</span><span class="sxs-lookup"><span data-stu-id="2475c-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="2475c-122">Aby chronić tożsamości organizacji, umożliwiają konfigurowanie zasad ryzyka automatycznie odpowiadać na wykryte błędy, jeśli został osiągnięty poziom określonego ryzyka.</span><span class="sxs-lookup"><span data-stu-id="2475c-122">To protect your organization's identities, you can configure risk-based policies that automatically respond to detected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="2475c-123">Te zasady, oprócz innych kontroli dostępu warunkowego zapewniane przez usługę Azure Active Directory i EMS, można automatycznie blokować lub zainicjować akcji korygowania adaptacyjną, które resetowania haseł włącznie i wymuszania uwierzytelnianie wieloskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="2475c-123">These policies, in addition to other conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="2475c-124">Funkcje ochrony tożsamości</span><span class="sxs-lookup"><span data-stu-id="2475c-124">Identity Protection capabilities</span></span>

<span data-ttu-id="2475c-125">**Wykrywanie luk w zabezpieczeniach i ryzykowne kont:**</span><span class="sxs-lookup"><span data-stu-id="2475c-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="2475c-126">Zapewnianie niestandardowych zalecenia dotyczące poprawy ogólny stan zabezpieczeń przez wyróżnianie luk w zabezpieczeniach</span><span class="sxs-lookup"><span data-stu-id="2475c-126">Providing custom recommendations to improve overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="2475c-127">Obliczanie poziomów ryzyka do logowania</span><span class="sxs-lookup"><span data-stu-id="2475c-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="2475c-128">Obliczanie poziomów ryzyka użytkownika</span><span class="sxs-lookup"><span data-stu-id="2475c-128">Calculating user risk levels</span></span>


<span data-ttu-id="2475c-129">**Badanie zdarzenia ryzyka:**</span><span class="sxs-lookup"><span data-stu-id="2475c-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="2475c-130">Wysyłanie powiadomienia o zdarzeniach ryzyka</span><span class="sxs-lookup"><span data-stu-id="2475c-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="2475c-131">Badania ryzyka zdarzeń za pomocą odpowiednich i kontekstowych informacji</span><span class="sxs-lookup"><span data-stu-id="2475c-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="2475c-132">Zapewnienie podstawowych przepływów pracy do śledzenia kontroli</span><span class="sxs-lookup"><span data-stu-id="2475c-132">Providing basic workflows to track investigations</span></span>
* <span data-ttu-id="2475c-133">Zapewniając łatwy dostęp do akcji korygowania, takich jak Resetowanie hasła</span><span class="sxs-lookup"><span data-stu-id="2475c-133">Providing easy access to remediation actions such as password reset</span></span>

<span data-ttu-id="2475c-134">**Zasady dostępu warunkowego opartego na ryzyka:**</span><span class="sxs-lookup"><span data-stu-id="2475c-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="2475c-135">Zasady złagodzić ryzykowne logowania przez blokowanie logowania lub wymaganie uwierzytelniania wieloskładnikowego wyzwania.</span><span class="sxs-lookup"><span data-stu-id="2475c-135">Policy to mitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="2475c-136">Zasady na wartość Blokuj lub kont użytkowników ryzykowne bezpieczne</span><span class="sxs-lookup"><span data-stu-id="2475c-136">Policy to block or secure risky user accounts</span></span>
* <span data-ttu-id="2475c-137">Zasady, aby wymagać od użytkowników rejestracji w usłudze Multi-Factor authentication</span><span class="sxs-lookup"><span data-stu-id="2475c-137">Policy to require users to register for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="2475c-138">Role ochrony tożsamości</span><span class="sxs-lookup"><span data-stu-id="2475c-138">Identity Protection roles</span></span>

<span data-ttu-id="2475c-139">Na potrzeby równoważenia obciążenia zarządzaniem wokół implementacji ochronę tożsamości, można przypisać kilka ról.</span><span class="sxs-lookup"><span data-stu-id="2475c-139">To load balance the management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="2475c-140">Azure AD Identity Protection obsługuje 3 role katalogu:</span><span class="sxs-lookup"><span data-stu-id="2475c-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="2475c-141">Rola</span><span class="sxs-lookup"><span data-stu-id="2475c-141">Role</span></span>                         | <span data-ttu-id="2475c-142">Możliwość</span><span class="sxs-lookup"><span data-stu-id="2475c-142">Can do</span></span>                          | <span data-ttu-id="2475c-143">Nie można wykonać</span><span class="sxs-lookup"><span data-stu-id="2475c-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="2475c-144">Administrator globalny</span><span class="sxs-lookup"><span data-stu-id="2475c-144">Global administrator</span></span>         | <span data-ttu-id="2475c-145">Pełny dostęp do ochrony tożsamości, dołączyć Identity Protection</span><span class="sxs-lookup"><span data-stu-id="2475c-145">Full access to Identity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="2475c-146">Administrator zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="2475c-146">Security administrator</span></span>       | <span data-ttu-id="2475c-147">Pełny dostęp do Identity Protection</span><span class="sxs-lookup"><span data-stu-id="2475c-147">Full access to Identity Protection</span></span> | <span data-ttu-id="2475c-148">Dołączyć ochronę tożsamości, zresetuj hasła dla użytkownika</span><span class="sxs-lookup"><span data-stu-id="2475c-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="2475c-149">Czytelnik zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="2475c-149">Security reader</span></span>              | <span data-ttu-id="2475c-150">Dostęp tylko do gotowy do ochrony tożsamości</span><span class="sxs-lookup"><span data-stu-id="2475c-150">Ready-only access to Identity Protection</span></span> | <span data-ttu-id="2475c-151">Dołączyć ochronę tożsamości użytkowników remidiate skonfigurować zasady, resetowania haseł</span><span class="sxs-lookup"><span data-stu-id="2475c-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="2475c-152">Aby uzyskać więcej informacji, zobacz [przypisywanie ról administratorów w usłudze Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2475c-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="2475c-153">Wykrywanie</span><span class="sxs-lookup"><span data-stu-id="2475c-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="2475c-154">Luki w zabezpieczeniach</span><span class="sxs-lookup"><span data-stu-id="2475c-154">Vulnerabilities</span></span>

<span data-ttu-id="2475c-155">Azure Active Directory Identity Protection analizy konfiguracji i wykrywa luk w zabezpieczeniach, które mogą mieć wpływ na tożsamości użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2475c-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="2475c-156">Aby uzyskać więcej informacji, zobacz [luk w zabezpieczeniach wykrywanych przez usługę Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="2475c-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="2475c-157">Zdarzenia ryzyka</span><span class="sxs-lookup"><span data-stu-id="2475c-157">Risk events</span></span>

<span data-ttu-id="2475c-158">Usługi Azure Active Directory korzysta z algorytmów uczenia maszynowego adaptacyjną i heurystyki do wykrycia podejrzanych działań, które są związane z tożsamości użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2475c-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user's identities.</span></span> <span data-ttu-id="2475c-159">System tworzy rekord dla każdego wykrytego podejrzane działania.</span><span class="sxs-lookup"><span data-stu-id="2475c-159">The system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="2475c-160">Te rekordy są także nazywane zdarzenia ryzyka.</span><span class="sxs-lookup"><span data-stu-id="2475c-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="2475c-161">Aby uzyskać więcej informacji, zobacz [Zdarzenia o podwyższonym ryzyku w usłudze Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="2475c-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="2475c-162">Badanie</span><span class="sxs-lookup"><span data-stu-id="2475c-162">Investigation</span></span>
<span data-ttu-id="2475c-163">Podróży za pomocą ochrony tożsamości zwykle zaczyna się od pulpit nawigacyjny ochrony tożsamości.</span><span class="sxs-lookup"><span data-stu-id="2475c-163">Your journey through Identity Protection typically starts with the Identity Protection dashboard.</span></span>

<span data-ttu-id="2475c-164">![Korygowanie](./media/active-directory-identityprotection/1000.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="2475c-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="2475c-165">Pulpit nawigacyjny umożliwia dostęp do:</span><span class="sxs-lookup"><span data-stu-id="2475c-165">The dashboard gives you access to:</span></span>

* <span data-ttu-id="2475c-166">Raporty takie jak **użytkownicy oflagowani ryzyka**, **ryzyka zdarzenia** i **luk w zabezpieczeniach**</span><span class="sxs-lookup"><span data-stu-id="2475c-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="2475c-167">Ustawienia, takie jak konfiguracja sieci **zasady zabezpieczeń**, **powiadomienia** i **rejestracji usługi Multi-Factor authentication**</span><span class="sxs-lookup"><span data-stu-id="2475c-167">Settings such as the configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="2475c-168">Zwykle to punkt startowy dla badania, czyli proces oceny działania, dzienników i inne istotne informacje powiązane ze zdarzeniem ryzyka zdecydować, czy korygowania lub ograniczenie kroki są niezbędne, i jak tożsamość zostało naruszone i zrozumieć korzystania ze złamanymi zabezpieczeniami tożsamości.</span><span class="sxs-lookup"><span data-stu-id="2475c-168">It is typically your starting point for investigation, which is the process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary,  and how the identity was compromised, and understand how the compromised identity was used.</span></span>

<span data-ttu-id="2475c-169">Można powiązać działaniach badań do [powiadomienia](active-directory-identityprotection-notifications.md) usługi Azure Active Directory Protection wysyła na wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="2475c-169">You can tie your investigation activities to the [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="2475c-170">Poniższe sekcje zawierają więcej szczegółowych informacji i kroki, które są związane z dochodzenia.</span><span class="sxs-lookup"><span data-stu-id="2475c-170">The following sections provide you with more details and the steps that are related to an investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="2475c-171">Ryzykowne logowania</span><span class="sxs-lookup"><span data-stu-id="2475c-171">Risky sign-ins</span></span>

<span data-ttu-id="2475c-172">Usługa Azure Active Directory wykryje [ryzyka typów zdarzeń](active-directory-reporting-risk-events.md#risk-event-types) w czasie rzeczywistym i w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="2475c-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="2475c-173">Każde zdarzenie zagrożenia wykrytego dla logowanie użytkownika przyczynia się do pojęcie logiczne, nazywane ryzykowne logowania.</span><span class="sxs-lookup"><span data-stu-id="2475c-173">Each risk event that has been detected for a sign-in of a user contributes to a logical concept called risky sign-in.</span></span> <span data-ttu-id="2475c-174">Ryzykowne logowanie jest wskaźnik prób logowania, które nie mogły zostać wykonane przez uprawnionego właściciela konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2475c-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by the legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="2475c-175">Poziom ryzyka logowania</span><span class="sxs-lookup"><span data-stu-id="2475c-175">Sign-in risk level</span></span>

<span data-ttu-id="2475c-176">Poziom ryzyka logowania jest wskazanie (wysoki, średni lub niski) prawdopodobieństwa, że próba logowania nie została wykonana przez wiarygodnego właściciela konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2475c-176">A sign-in risk level is an indication (High, Medium, or Low) of the likelihood that a sign-in attempt was not performed by the legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="2475c-177">Zmniejszenia zdarzenia logowania ryzyka</span><span class="sxs-lookup"><span data-stu-id="2475c-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="2475c-178">Środki zaradcze jest akcji, aby ograniczyć możliwość atakujący wykorzystać złamany tożsamości lub urządzenia bez przywrócenia tożsamości lub urządzenie to bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="2475c-178">A mitigation is an action to limit the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="2475c-179">Środki zaradcze nie można rozpoznać poprzednie zdarzenia logowania ryzyko związane z tożsamości lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2475c-179">A mitigation does not resolve previous sign-in risk events associated with the identity or device.</span></span>

<span data-ttu-id="2475c-180">Aby uniknąć automatycznie ryzykowne logowania, można skonfigurować policicies zabezpieczeń logowania ryzyka.</span><span class="sxs-lookup"><span data-stu-id="2475c-180">To mitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="2475c-181">Korzystając z tych zasad, należy wziąć pod uwagę poziom ryzyka użytkownika lub przy logowaniu do blokowania ryzykowne logowania lub użytkownik przeprowadzać uwierzytelnianie wieloskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="2475c-181">Using these policies, you consider the risk level of the user or the sign-in to block risky sign-ins or require the user to perform multi-factor authentication.</span></span> <span data-ttu-id="2475c-182">Te akcje mogą uniemożliwiać osobie atakującej wykorzystanie kradzieży tożsamości, aby spowodować szkody i może spowodować pewien czas do zabezpieczania tożsamości.</span><span class="sxs-lookup"><span data-stu-id="2475c-182">These actions may prevent an attacker from exploiting a stolen identity to cause damage, and may give you some time to secure the identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="2475c-183">Zasady zabezpieczeń logowania ryzyka</span><span class="sxs-lookup"><span data-stu-id="2475c-183">Sign-in risk security policy</span></span>
<span data-ttu-id="2475c-184">Zasady logowania ryzyko jest zasady dostępu warunkowego, która ocenia ryzyko dla określonych logowanie i stosuje środki zaradcze, na podstawie wstępnie zdefiniowane warunki i zasady.</span><span class="sxs-lookup"><span data-stu-id="2475c-184">A sign-in risk policy is a conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="2475c-185">![Zasady logowania ryzyka](./media/active-directory-identityprotection/1014.png "logowania zasad ryzyka")</span><span class="sxs-lookup"><span data-stu-id="2475c-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="2475c-186">Azure AD Identity Protection pomaga w zarządzaniu łagodzenie ryzykowne logowania umożliwiając:</span><span class="sxs-lookup"><span data-stu-id="2475c-186">Azure AD Identity Protection helps you manage the mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="2475c-187">Ustaw użytkowników i grup, których dotyczy zasada:</span><span class="sxs-lookup"><span data-stu-id="2475c-187">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="2475c-188">![Zasady logowania ryzyka](./media/active-directory-identityprotection/1015.png "logowania zasad ryzyka")</span><span class="sxs-lookup"><span data-stu-id="2475c-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="2475c-189">Należy ustawić logowania ryzyka poziomu próg (niski, średni lub wysoki) wyzwalania zasad:</span><span class="sxs-lookup"><span data-stu-id="2475c-189">Set the sign-in risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="2475c-190">![Zasady logowania ryzyka](./media/active-directory-identityprotection/1016.png "logowania zasad ryzyka")</span><span class="sxs-lookup"><span data-stu-id="2475c-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="2475c-191">Ustaw formanty mają być egzekwowane, gdy wyzwala zasad:</span><span class="sxs-lookup"><span data-stu-id="2475c-191">Set the controls to be enforced when the policy triggers:</span></span>  

    <span data-ttu-id="2475c-192">![Zasady logowania ryzyka](./media/active-directory-identityprotection/1017.png "logowania zasad ryzyka")</span><span class="sxs-lookup"><span data-stu-id="2475c-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="2475c-193">Przełącz stan tej zasady:</span><span class="sxs-lookup"><span data-stu-id="2475c-193">Switch the state of your policy:</span></span>

    <span data-ttu-id="2475c-194">![Rejestracja usługi MFA](./media/active-directory-identityprotection/403.png "rejestracji usługi MFA")</span><span class="sxs-lookup"><span data-stu-id="2475c-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="2475c-195">Przegląd i ocena wpływu zmiany przed uaktywnieniem go:</span><span class="sxs-lookup"><span data-stu-id="2475c-195">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="2475c-196">![Zasady logowania ryzyka](./media/active-directory-identityprotection/1018.png "logowania zasad ryzyka")</span><span class="sxs-lookup"><span data-stu-id="2475c-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-to-know"></a><span data-ttu-id="2475c-197">Co należy wiedzieć</span><span class="sxs-lookup"><span data-stu-id="2475c-197">What you need to know</span></span>
<span data-ttu-id="2475c-198">Można skonfigurować zasady zabezpieczeń ryzyka logowania, aby wymusić uwierzytelnianie wieloskładnikowe:</span><span class="sxs-lookup"><span data-stu-id="2475c-198">You can configure a sign-in risk security policy to require multi-factor authentication:</span></span>

<span data-ttu-id="2475c-199">![Zasady logowania ryzyka](./media/active-directory-identityprotection/1017.png "logowania zasad ryzyka")</span><span class="sxs-lookup"><span data-stu-id="2475c-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="2475c-200">Jednak ze względu na bezpieczeństwo, to ustawienie działa tylko dla użytkowników, które zostały już zarejestrowane w usłudze Multi-Factor authentication.</span><span class="sxs-lookup"><span data-stu-id="2475c-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="2475c-201">Jeśli spełniony jest warunek wymaganie uwierzytelniania wieloskładnikowego dla użytkownika, który nie jest jeszcze zarejestrowany w usłudze Multi-Factor authentication, użytkownik jest zablokowany.</span><span class="sxs-lookup"><span data-stu-id="2475c-201">If the condition to require multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, the user is blocked.</span></span>

<span data-ttu-id="2475c-202">Najlepszym rozwiązaniem Jeśli chcesz wymusić uwierzytelnianie wieloskładnikowe ryzykowne logowania, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2475c-202">As a best practice, if you want to require multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="2475c-203">Włącz [zasady rejestracji usługi Multi-Factor authentication](#multi-factor-authentication-registration-policy) określonych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2475c-203">Enable the [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for the affected users.</span></span>
2. <span data-ttu-id="2475c-204">Wymaga odpowiednich użytkowników, aby logowania w sesji ryzykowne do wykonania rejestracji usługi MFA</span><span class="sxs-lookup"><span data-stu-id="2475c-204">Require the affected users to login in a non-risky session to perform a MFA registration</span></span>

<span data-ttu-id="2475c-205">Wykonanie tych kroków gwarantuje, że uwierzytelnianie wieloskładnikowe jest wymagany dla ryzykownych logowanie.</span><span class="sxs-lookup"><span data-stu-id="2475c-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="2475c-206">Najlepsze praktyki</span><span class="sxs-lookup"><span data-stu-id="2475c-206">Best practices</span></span>
<span data-ttu-id="2475c-207">Wybieranie **wysokiej** próg zmniejsza liczbę razy zasadę wyzwoleniu oraz zminimalizować wpływ na użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2475c-207">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>  

<span data-ttu-id="2475c-208">Jednak nie obejmuje **małej** i **średni** logowania oznaczona flagą ryzyko związane z zasad, które nie mogą blokować osoba atakująca możliwości wykorzystania złamany tożsamości.</span><span class="sxs-lookup"><span data-stu-id="2475c-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from the policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="2475c-209">Podczas ustawiania zasad</span><span class="sxs-lookup"><span data-stu-id="2475c-209">When setting the policy,</span></span>

* <span data-ttu-id="2475c-210">Wyklucz użytkowników, którzy nie / nie można wprowadzić uwierzytelnianie wieloskładnikowe</span><span class="sxs-lookup"><span data-stu-id="2475c-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="2475c-211">Wyklucz użytkowników, w których włączenie zasad nie jest praktyczne ustawień regionalnych (na przykład brak dostępu do działu pomocy technicznej)</span><span class="sxs-lookup"><span data-stu-id="2475c-211">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="2475c-212">Wyklucz użytkowników, które mogą generować dużą alarmów false (deweloperów, analityków zabezpieczeń)</span><span class="sxs-lookup"><span data-stu-id="2475c-212">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="2475c-213">Użyj **wysokiej** próg podczas początkowej zasad zbiorczego, lub jeśli należy zminimalizować problemy, które zostały odebrane przez użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="2475c-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="2475c-214">Użyj **małej** progu, jeśli organizacja wymaga wyższego poziomu bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="2475c-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="2475c-215">Wybieranie **małej** próg wprowadzono dodatkowe użytkownika logowania wyzwania, ale zwiększyć bezpieczeństwo.</span><span class="sxs-lookup"><span data-stu-id="2475c-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="2475c-216">Jest zalecana domyślna w przypadku większości organizacji do skonfigurowania reguły dla **średni** próg uzyskanie równowagi między użyteczność i zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="2475c-216">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="2475c-217">Zasady logowania ryzyka są:</span><span class="sxs-lookup"><span data-stu-id="2475c-217">The sign-in risk policy is:</span></span>

* <span data-ttu-id="2475c-218">Stosowane do całego ruchu w przeglądarce i logowania korzystających z nowoczesnego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="2475c-218">Applied to all browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="2475c-219">Nie dotyczy aplikacji przy użyciu starszych protokołów zabezpieczeń przez wyłączenie punkt końcowy protokołu WS-Trust w federacyjnym dostawców tożsamości, takie jak usługi AD FS.</span><span class="sxs-lookup"><span data-stu-id="2475c-219">Not applied to applications using older security protocols by disabling the WS-Trust endpoint at the federated IDP, such as ADFS.</span></span>

<span data-ttu-id="2475c-220">**Zdarzenia o podwyższonym ryzyku** w konsoli programu Identity Protection Wyświetla listę wszystkich zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="2475c-220">The **Risk Events** page in the Identity Protection console lists all events:</span></span>

* <span data-ttu-id="2475c-221">Ta zasada została zastosowana do</span><span class="sxs-lookup"><span data-stu-id="2475c-221">This policy was applied to</span></span>
* <span data-ttu-id="2475c-222">Można sprawdzić działanie i ustalić, czy akcja została odpowiednie</span><span class="sxs-lookup"><span data-stu-id="2475c-222">You can review the activity and determine whether the action was appropriate or not</span></span>

<span data-ttu-id="2475c-223">Omówienie powiązane funkcje użytkownika Zobacz:</span><span class="sxs-lookup"><span data-stu-id="2475c-223">For an overview of the related user experience, see:</span></span>

* [<span data-ttu-id="2475c-224">Ryzykowne odzyskiwania logowania</span><span class="sxs-lookup"><span data-stu-id="2475c-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="2475c-225">Ryzykowne logowania zablokowane</span><span class="sxs-lookup"><span data-stu-id="2475c-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="2475c-226">Logowanie, korzystając z usługi Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="2475c-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="2475c-227">**Aby otworzyć okno dialogowe elementami konfiguracji**:</span><span class="sxs-lookup"><span data-stu-id="2475c-227">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="2475c-228">Na **Azure AD Identity Protection** bloku, w **Konfiguruj** kliknij **logowania zasad ryzyka**.</span><span class="sxs-lookup"><span data-stu-id="2475c-228">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="2475c-229">![Zasady użytkownika ridk](./media/active-directory-identityprotection/1014.png "zasady ridk użytkownika")</span><span class="sxs-lookup"><span data-stu-id="2475c-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="2475c-230">Użytkownicy oflagowani w związku z ryzykiem</span><span class="sxs-lookup"><span data-stu-id="2475c-230">Users flagged for risk</span></span>

<span data-ttu-id="2475c-231">Wszystkie aktywne [ryzyka zdarzenia](active-directory-identity-protection-risk-events.md) zostały wykryte przez usługę Azure Active Directory dla użytkownika współtworzyć pojęcie logiczne o nazwie użytkownika ryzyka.</span><span class="sxs-lookup"><span data-stu-id="2475c-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute to a logical concept called user risk.</span></span> <span data-ttu-id="2475c-232">Użytkownik oznaczona flagą ryzyko jest wskaźnikiem dla konta użytkownika, który może być zagrożone.</span><span class="sxs-lookup"><span data-stu-id="2475c-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![Użytkownicy oflagowani w związku z ryzykiem](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="2475c-234">Poziom ryzyka użytkownika</span><span class="sxs-lookup"><span data-stu-id="2475c-234">User risk level</span></span>

<span data-ttu-id="2475c-235">Poziom ryzyka użytkownika będzie wskazywać prawdopodobieństwo, że tożsamość użytkownika została naruszona poufność (wysoki, średni lub niski).</span><span class="sxs-lookup"><span data-stu-id="2475c-235">A user risk level is an indication (High, Medium, or Low) of the likelihood that the user’s identity has been compromised.</span></span> <span data-ttu-id="2475c-236">Jest obliczana na podstawie zdarzeń ryzyka użytkownika, które są skojarzone z tożsamością użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2475c-236">It is calculated based on the user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="2475c-237">Stan zdarzenia ryzyko jest **Active** lub **zamknięte**.</span><span class="sxs-lookup"><span data-stu-id="2475c-237">The status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="2475c-238">Tylko ryzyka zdarzenia, które są **Active** przyczyniają się do obliczania poziomu ryzyka użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2475c-238">Only risk events that are **Active** contribute to the user risk level calculation.</span></span>

<span data-ttu-id="2475c-239">Poziom ryzyka użytkownika jest obliczana przy użyciu następujących danych wejściowych:</span><span class="sxs-lookup"><span data-stu-id="2475c-239">The user risk level is calculated using the following inputs:</span></span>

* <span data-ttu-id="2475c-240">Zdarzenia aktywne ryzyka wpływu na użytkownika</span><span class="sxs-lookup"><span data-stu-id="2475c-240">Active risk events impacting the user</span></span>
* <span data-ttu-id="2475c-241">Poziom ryzyka tych zdarzeń</span><span class="sxs-lookup"><span data-stu-id="2475c-241">Risk level of these events</span></span>
* <span data-ttu-id="2475c-242">Określa, czy wykonano wszystkie akcje naprawcze wykonane</span><span class="sxs-lookup"><span data-stu-id="2475c-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="2475c-243">![Ryzyko użytkownika](./media/active-directory-identityprotection/1031.png "zagrożeń użytkownika")</span><span class="sxs-lookup"><span data-stu-id="2475c-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="2475c-244">Umożliwia tworzenie zasad dostępu warunkowego, które blokują ryzykowne użytkownikom logowanie użytkownika poziomów ryzyka lub mogą bezpiecznie zmienić swoje hasło.</span><span class="sxs-lookup"><span data-stu-id="2475c-244">You can use the user risk levels to create conditional access policies that block risky users from signing in, or force them to securely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="2475c-245">Zamknięcie zdarzenia o podwyższonym ryzyku ręcznie</span><span class="sxs-lookup"><span data-stu-id="2475c-245">Closing risk events manually</span></span>

<span data-ttu-id="2475c-246">W większości przypadków potrwa akcji korygowania, takich jak bezpieczny resetowania hasła, aby automatycznie zamknąć zdarzenia ryzyka.</span><span class="sxs-lookup"><span data-stu-id="2475c-246">In most cases, you will take remediation actions such as a secure password reset to automatically close risk events.</span></span> <span data-ttu-id="2475c-247">Jednak to może nie być możliwe.</span><span class="sxs-lookup"><span data-stu-id="2475c-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="2475c-248">To, na przykład sytuacji, gdy:</span><span class="sxs-lookup"><span data-stu-id="2475c-248">This is, for example, the case, when:</span></span>

* <span data-ttu-id="2475c-249">Użytkownik z zdarzenia Active ryzyka został usunięty.</span><span class="sxs-lookup"><span data-stu-id="2475c-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="2475c-250">Badanie wykaże, że zdarzenie zagrożenia zgłoszony został wykonać przez wiarygodnego użytkownika</span><span class="sxs-lookup"><span data-stu-id="2475c-250">An investigation reveals that a reported risk event has been perform by the legitimate user</span></span>

<span data-ttu-id="2475c-251">Ponieważ zdarzenia ryzyka, które są **Active** przyczyniają się do obliczania ryzyka użytkownika, może być konieczne ręczne obniżyć poziom ryzyka zamknięcie zdarzenia o podwyższonym ryzyku ręcznie.</span><span class="sxs-lookup"><span data-stu-id="2475c-251">Because risk events that are **Active** contribute to the user risk calculation, you may have to manually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="2475c-252">W trakcie badania można wykonać dowolną z tych akcji, aby zmienić stan zdarzenia ryzyka:</span><span class="sxs-lookup"><span data-stu-id="2475c-252">During the course of investigation, you can choose to take any of these actions to change the status of a risk event:</span></span>

<span data-ttu-id="2475c-253">![Akcje](./media/active-directory-identityprotection/34.png "akcje")</span><span class="sxs-lookup"><span data-stu-id="2475c-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="2475c-254">**Rozwiąż** — Jeśli po zbadaniu zdarzenia ryzyka, trwało akcji korygowania odpowiednie poza ochrony tożsamości i uważasz, że zdarzenie ryzyka należy traktować jako zamknięty, oznaczenia zdarzeń jako rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="2475c-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that the risk event should be considered closed, mark the event as Resolved.</span></span> <span data-ttu-id="2475c-255">Rozwiązane zdarzeń ustawi stan zdarzenia ryzyka zamknięte i zdarzenia ryzyka już przyczyniają się do użytkownika ryzyka.</span><span class="sxs-lookup"><span data-stu-id="2475c-255">Resolved events will set the risk event’s status to Closed and the risk event will no longer contribute to user risk.</span></span>
* <span data-ttu-id="2475c-256">**Oznacz jako fałszywie dodatnich** — w niektórych przypadkach można zbadać zdarzenia ryzyka i wykryć, czy został niepoprawnie oznaczone jako ryzykowne.</span><span class="sxs-lookup"><span data-stu-id="2475c-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="2475c-257">Można ograniczyć liczbę wystąpień takich przez oznaczenie zdarzeń ryzyka jako fałszywie dodatnich.</span><span class="sxs-lookup"><span data-stu-id="2475c-257">You can help reduce the number of such occurrences by marking the risk event as False-positive.</span></span> <span data-ttu-id="2475c-258">Dzięki temu algorytmów, aby zwiększyć w przyszłości klasyfikacji zdarzenia podobne uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="2475c-258">This will help the machine learning algorithms to improve the classification of similar events in the future.</span></span> <span data-ttu-id="2475c-259">Status zdarzenia fałszywie dodatnich **zamknięte** i nie wpływają one ryzyko użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2475c-259">The status of false-positive events is to **Closed** and they will no longer contribute to user risk.</span></span>
* <span data-ttu-id="2475c-260">**Ignoruj** — Jeśli nie miały żadnych działań korygujących, ale można usunąć z listy aktywne zdarzenie ryzyka można oznaczyć zdarzeniem ryzyka Ignoruj i stan zdarzenia zostanie zamknięty.</span><span class="sxs-lookup"><span data-stu-id="2475c-260">**Ignore** - If you have not taken any remediation action, but want the risk event to be removed from the active list, you can mark a risk event Ignore and the event status will be Closed.</span></span> <span data-ttu-id="2475c-261">Zignorowano zdarzenia nie przyczyniają się ryzyko użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2475c-261">Ignored events do not contribute to user risk.</span></span> <span data-ttu-id="2475c-262">Tej opcji należy używać tylko w niezwykłych okolicznościach.</span><span class="sxs-lookup"><span data-stu-id="2475c-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="2475c-263">**Uaktywnij ponownie** -ryzyka zdarzenia, które zostały ręcznie zamknięty (wybierając **rozwiązać**, **wynik fałszywie dodatni**, lub **Ignoruj**) można ponownie uaktywnić, ustawienie stanu zdarzenia do **Active**.</span><span class="sxs-lookup"><span data-stu-id="2475c-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting the event status back to **Active**.</span></span> <span data-ttu-id="2475c-264">Zdarzenia ponownie uaktywnione ryzyka przyczyniają się do obliczania poziomu ryzyka użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2475c-264">Reactivated risk events contribute to the user risk level calculation.</span></span> <span data-ttu-id="2475c-265">Nie można ponownie uaktywnić zamknięte przy użyciu funkcji korygowania (takie jak resetowania hasła bezpiecznego) zdarzenia ryzyka.</span><span class="sxs-lookup"><span data-stu-id="2475c-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="2475c-266">**Aby otworzyć okno dialogowe elementami konfiguracji**:</span><span class="sxs-lookup"><span data-stu-id="2475c-266">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="2475c-267">Na **Azure AD Identity Protection** bloku, w obszarze **zbadaj**, kliknij przycisk **ryzyka zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="2475c-267">On the **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="2475c-268">![Resetowania hasła ręczne](./media/active-directory-identityprotection/1002.png "resetowania hasła ręczne")</span><span class="sxs-lookup"><span data-stu-id="2475c-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="2475c-269">W **ryzyka zdarzenia** kliknij zagrożenie.</span><span class="sxs-lookup"><span data-stu-id="2475c-269">In the **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="2475c-270">![Resetowania hasła ręczne](./media/active-directory-identityprotection/1003.png "resetowania hasła ręczne")</span><span class="sxs-lookup"><span data-stu-id="2475c-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="2475c-271">W bloku ryzyka kliknij prawym przyciskiem myszy przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2475c-271">On the risk blade, right-click a user.</span></span>

    <span data-ttu-id="2475c-272">![Resetowania hasła ręczne](./media/active-directory-identityprotection/1004.png "resetowania hasła ręczne")</span><span class="sxs-lookup"><span data-stu-id="2475c-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="2475c-273">Ręczne zamknięcie wszystkich zdarzeń ryzyka dla użytkownika</span><span class="sxs-lookup"><span data-stu-id="2475c-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="2475c-274">Zamiast ręcznie indywidualnie zamknięcie zdarzenia ryzyka dla użytkownika, Azure Active Directory Identity Protection zapewnia także metodę Zamknij wszystkie zdarzenia dla użytkownika z jednego kliknięcia.</span><span class="sxs-lookup"><span data-stu-id="2475c-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method to close all events for a user with one click.</span></span>

<span data-ttu-id="2475c-275">![Akcje](./media/active-directory-identityprotection/2222.png "akcje")</span><span class="sxs-lookup"><span data-stu-id="2475c-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="2475c-276">Po kliknięciu **odrzucić wszystkie zdarzenia**, wszystkie zdarzenia zostaną zamknięte i użytkownika, którego dotyczy nie jest już na ryzyko.</span><span class="sxs-lookup"><span data-stu-id="2475c-276">When you click **Dismiss all events**, all events are closed and the affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="2475c-277">Zdarzenia o podwyższonym ryzyku korygując użytkownika</span><span class="sxs-lookup"><span data-stu-id="2475c-277">Remediating user risk events</span></span>

<span data-ttu-id="2475c-278">Korygowanie jest czynnością do zabezpieczania tożsamości lub urządzeń, które wcześniej podejrzenia lub znane naruszenia.</span><span class="sxs-lookup"><span data-stu-id="2475c-278">A remediation is an action to secure an identity or a device that was previously suspected or known to be compromised.</span></span> <span data-ttu-id="2475c-279">Akcja korygowania przywraca tożsamości lub urządzenie to bezpieczne i usuwa poprzednie zdarzenia ryzyko związane z tożsamości lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2475c-279">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

<span data-ttu-id="2475c-280">Aby skorygować użytkownika zdarzenia o podwyższonym ryzyku, można:</span><span class="sxs-lookup"><span data-stu-id="2475c-280">To remediate user risk events, you can:</span></span>

* <span data-ttu-id="2475c-281">Bezpieczne hasło zresetować ręcznie skorygować zdarzenia o podwyższonym ryzyku użytkownika</span><span class="sxs-lookup"><span data-stu-id="2475c-281">Perform a secure password reset to remediate user risk events manually</span></span>
* <span data-ttu-id="2475c-282">Konfigurowanie zasad zabezpieczeń użytkownika ryzyko ograniczenia lub automatycznie korygować zdarzenia o podwyższonym ryzyku użytkownika</span><span class="sxs-lookup"><span data-stu-id="2475c-282">Configure a user risk security policy to mitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="2475c-283">Ponowne instalowanie obrazu zainfekowanych urządzeń</span><span class="sxs-lookup"><span data-stu-id="2475c-283">Re-image the infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="2475c-284">Resetowanie ręczne bezpiecznego hasła</span><span class="sxs-lookup"><span data-stu-id="2475c-284">Manual secure password reset</span></span>
<span data-ttu-id="2475c-285">Bezpieczne hasło jest skuteczne korygowania w przypadku wielu zdarzeń ryzyka i wykonywana, automatycznie powoduje zamknięcie zdarzenia o podwyższonym ryzyku i ponownie oblicza poziom ryzyka użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2475c-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates the user risk level.</span></span> <span data-ttu-id="2475c-286">Pulpit nawigacyjny ochrony tożsamości służy do inicjowania resetowania hasła dla użytkownika ryzykowne.</span><span class="sxs-lookup"><span data-stu-id="2475c-286">You can use the Identity Protection dashboard to initiate a password reset for a risky user.</span></span>

<span data-ttu-id="2475c-287">Określone okno zapewnia dwie różne metody, aby zresetować hasło:</span><span class="sxs-lookup"><span data-stu-id="2475c-287">The related dialog provides two different methods to reset a password:</span></span>

<span data-ttu-id="2475c-288">**Zresetuj hasło** — wybierz tę opcję **wymagają od użytkownika do zresetowania swojego hasła** Aby zezwolić użytkownikowi na własnym odzyskania, jeśli użytkownik został zarejestrowany w usłudze Multi-Factor authentication.</span><span class="sxs-lookup"><span data-stu-id="2475c-288">**Reset password** - Select **Require the user to reset their password** to allow the user to self-recover if the user has registered for multi-factor authentication.</span></span> <span data-ttu-id="2475c-289">Podczas jego następnego logowania użytkownik będzie wymagane do rozwiązania pomyślnie żądanie uwierzytelniania wieloskładnikowego i następnie wymuszone, aby zmienić hasło.</span><span class="sxs-lookup"><span data-stu-id="2475c-289">During the user's next sign-in, the user will be required to solve a multi-factor authentication challenge successfully and then, forced to change the password.</span></span> <span data-ttu-id="2475c-290">Ta opcja jest niedostępna, jeśli konto użytkownika nie jest już zarejestrowany uwierzytelnianie wieloskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="2475c-290">This option isn't available if the user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="2475c-291">**Hasło tymczasowe** — wybierz tę opcję **wygenerować hasło tymczasowe** natychmiast unieważnia istniejące hasło i utworzenie nowego hasła tymczasowego dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2475c-291">**Temporary password** - Select **Generate a temporary password** to immediately invalidate the existing password, and create a new temporary password for the user.</span></span> <span data-ttu-id="2475c-292">Alternatywny adres e-mail użytkownika lub menedżerem użytkownika, należy wysłać nowe hasło tymczasowe.</span><span class="sxs-lookup"><span data-stu-id="2475c-292">Send the new temporary password to an alternate email address for the user or to the user's manager.</span></span> <span data-ttu-id="2475c-293">Ponieważ hasło tymczasowe, użytkownik pojawi się monit o zmianę hasła podczas logowania.</span><span class="sxs-lookup"><span data-stu-id="2475c-293">Because the password is temporary, the user will be prompted to change the password upon sign-in.</span></span>

<span data-ttu-id="2475c-294">![Zasady](./media/active-directory-identityprotection/1005.png "zasad")</span><span class="sxs-lookup"><span data-stu-id="2475c-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="2475c-295">**Aby otworzyć okno dialogowe elementami konfiguracji**:</span><span class="sxs-lookup"><span data-stu-id="2475c-295">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="2475c-296">Na **Azure AD Identity Protection** bloku, kliknij przycisk **użytkownicy oflagowani ryzyka**.</span><span class="sxs-lookup"><span data-stu-id="2475c-296">On the **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="2475c-297">![Resetowania hasła ręczne](./media/active-directory-identityprotection/1006.png "resetowania hasła ręczne")</span><span class="sxs-lookup"><span data-stu-id="2475c-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="2475c-298">Z listy użytkowników wybierz użytkownika z ryzykiem co najmniej jednego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="2475c-298">From the list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="2475c-299">![Resetowania hasła ręczne](./media/active-directory-identityprotection/1007.png "resetowania hasła ręczne")</span><span class="sxs-lookup"><span data-stu-id="2475c-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="2475c-300">W bloku użytkownika kliknij **resetowania hasła**.</span><span class="sxs-lookup"><span data-stu-id="2475c-300">On the user blade, click **Reset password**.</span></span>

    <span data-ttu-id="2475c-301">![Resetowania hasła ręczne](./media/active-directory-identityprotection/1008.png "resetowania hasła ręczne")</span><span class="sxs-lookup"><span data-stu-id="2475c-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="2475c-302">Zasady zabezpieczeń użytkownika ryzyka</span><span class="sxs-lookup"><span data-stu-id="2475c-302">User risk security policy</span></span>
<span data-ttu-id="2475c-303">Zasady zabezpieczeń użytkownika ryzyko jest zasady dostępu warunkowego, które ocenia poziom ryzyka dla określonego użytkownika, a następnie stosuje akcje korygowania i środki zaradcze, na podstawie wstępnie zdefiniowane warunki i zasady.</span><span class="sxs-lookup"><span data-stu-id="2475c-303">A user risk security policy is a conditional access policy that evaluates the risk level to a specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="2475c-304">![Zasady użytkownika ridk](./media/active-directory-identityprotection/1009.png "zasady ridk użytkownika")</span><span class="sxs-lookup"><span data-stu-id="2475c-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="2475c-305">Azure AD Identity Protection pomaga w zarządzaniu łagodzenia i korygowania oflagowane ryzyka, umożliwiając użytkownikom:</span><span class="sxs-lookup"><span data-stu-id="2475c-305">Azure AD Identity Protection helps you manage the mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="2475c-306">Ustaw użytkowników i grup, których dotyczy zasada:</span><span class="sxs-lookup"><span data-stu-id="2475c-306">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="2475c-307">![Zasady użytkownika ridk](./media/active-directory-identityprotection/1010.png "zasady ridk użytkownika")</span><span class="sxs-lookup"><span data-stu-id="2475c-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="2475c-308">Należy ustawić użytkownika ryzyka poziomu próg (niski, średni lub wysoki) wyzwalania zasad:</span><span class="sxs-lookup"><span data-stu-id="2475c-308">Set the user risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="2475c-309">![Zasady użytkownika ridk](./media/active-directory-identityprotection/1011.png "zasady ridk użytkownika")</span><span class="sxs-lookup"><span data-stu-id="2475c-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="2475c-310">Ustaw formanty mają być egzekwowane, gdy wyzwala zasad:</span><span class="sxs-lookup"><span data-stu-id="2475c-310">Set the controls to be enforced when the policy triggers:</span></span>

    <span data-ttu-id="2475c-311">![Zasady użytkownika ridk](./media/active-directory-identityprotection/1012.png "zasady ridk użytkownika")</span><span class="sxs-lookup"><span data-stu-id="2475c-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="2475c-312">Przełącz stan tej zasady:</span><span class="sxs-lookup"><span data-stu-id="2475c-312">Switch the state of your policy:</span></span>

    <span data-ttu-id="2475c-313">![Zasady użytkownika ridk](./media/active-directory-identityprotection/403.png "rejestracji usługi MFA")</span><span class="sxs-lookup"><span data-stu-id="2475c-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="2475c-314">Przegląd i ocena wpływu zmiany przed uaktywnieniem go:</span><span class="sxs-lookup"><span data-stu-id="2475c-314">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="2475c-315">![Zasady użytkownika ridk](./media/active-directory-identityprotection/1013.png "zasady ridk użytkownika")</span><span class="sxs-lookup"><span data-stu-id="2475c-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="2475c-316">Wybieranie **wysokiej** próg zmniejsza liczbę razy zasadę wyzwoleniu oraz zminimalizować wpływ na użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2475c-316">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>
<span data-ttu-id="2475c-317">Jednak nie obejmuje **małej** i **średni** użytkowników oznaczona flagą ryzyko związane z zasad, które mogą nie zapewnić tożsamości lub urządzenia, który zostały wcześniej podejrzanych lub znane naruszenia.</span><span class="sxs-lookup"><span data-stu-id="2475c-317">However, it excludes **Low** and **Medium** users flagged for risk from the policy, which may not secure identities or devices that were previously suspected or known to be compromised.</span></span>

<span data-ttu-id="2475c-318">Podczas ustawiania zasad</span><span class="sxs-lookup"><span data-stu-id="2475c-318">When setting the policy,</span></span>

* <span data-ttu-id="2475c-319">Wyklucz użytkowników, które mogą generować dużą alarmów false (deweloperów, analityków zabezpieczeń)</span><span class="sxs-lookup"><span data-stu-id="2475c-319">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="2475c-320">Wyklucz użytkowników, w których włączenie zasad nie jest praktyczne ustawień regionalnych (na przykład brak dostępu do działu pomocy technicznej)</span><span class="sxs-lookup"><span data-stu-id="2475c-320">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="2475c-321">Użyj **wysokiej** próg podczas początkowej zasad zbiorczego, lub jeśli należy zminimalizować problemy, które zostały odebrane przez użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="2475c-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="2475c-322">Użyj **małej** progu, jeśli organizacja wymaga wyższego poziomu bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="2475c-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="2475c-323">Wybieranie **małej** próg wprowadzono dodatkowe użytkownika logowania wyzwania, ale zwiększyć bezpieczeństwo.</span><span class="sxs-lookup"><span data-stu-id="2475c-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="2475c-324">Jest zalecana domyślna w przypadku większości organizacji do skonfigurowania reguły dla **średni** próg uzyskanie równowagi między użyteczność i zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="2475c-324">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="2475c-325">Omówienie powiązane funkcje użytkownika Zobacz:</span><span class="sxs-lookup"><span data-stu-id="2475c-325">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="2475c-326">[Złamania zabezpieczeń konta przepływu odzyskiwania](active-directory-identityprotection-flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="2475c-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="2475c-327">[Naruszone zablokowano konto przepływu](active-directory-identityprotection-flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="2475c-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="2475c-328">**Aby otworzyć okno dialogowe elementami konfiguracji**:</span><span class="sxs-lookup"><span data-stu-id="2475c-328">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="2475c-329">Na **Azure AD Identity Protection** bloku, w **Konfiguruj** kliknij **zasad ryzyka użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="2475c-329">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="2475c-330">![Zasady użytkownika ridk](./media/active-directory-identityprotection/1009.png "zasady ridk użytkownika")</span><span class="sxs-lookup"><span data-stu-id="2475c-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="2475c-331">Zmniejszenia zdarzenia o podwyższonym ryzyku użytkownika</span><span class="sxs-lookup"><span data-stu-id="2475c-331">Mitigating user risk events</span></span>
<span data-ttu-id="2475c-332">Administratorzy mogą skonfigurować zasady zabezpieczeń ryzyka użytkownika, aby uniemożliwić użytkownikom na logowanie się w zależności od poziomu zagrożenia.</span><span class="sxs-lookup"><span data-stu-id="2475c-332">Administrators can set a user risk security policy to block users upon sign-in depending on the risk level.</span></span>

<span data-ttu-id="2475c-333">Blokowanie logowania:</span><span class="sxs-lookup"><span data-stu-id="2475c-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="2475c-334">Uniemożliwia wygenerowanie nowego zdarzenia ryzyka użytkownika dla użytkownika, którego dotyczy</span><span class="sxs-lookup"><span data-stu-id="2475c-334">Prevents the generation of new user risk events for the affected user</span></span>
* <span data-ttu-id="2475c-335">Administratorzy mogą ręcznie skorygować zdarzenia o podwyższonym ryzyku wpływających na tożsamości użytkownika i przywrócenia stanu bezpiecznego</span><span class="sxs-lookup"><span data-stu-id="2475c-335">Enables administrators to manually remediate the risk events affecting the user's identity and restore it to a secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="2475c-336">Zasady rejestracji usługi Multi-Factor authentication</span><span class="sxs-lookup"><span data-stu-id="2475c-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="2475c-337">Uwierzytelnianie wieloskładnikowe platformy Azure jest metodę weryfikacji tożsamości, która wymaga użycia więcej niż tylko nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="2475c-337">Azure multi-factor authentication is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="2475c-338">Zapewnia drugą warstwę zabezpieczeń do logowania użytkowników i transakcji.</span><span class="sxs-lookup"><span data-stu-id="2475c-338">It provides a second layer of security to user sign-ins and transactions.</span></span>  
<span data-ttu-id="2475c-339">Firma Microsoft zaleca wymagane uwierzytelnianie wieloskładnikowe platformy Azure logowania użytkownika, ponieważ jego:</span><span class="sxs-lookup"><span data-stu-id="2475c-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="2475c-340">Zapewnia silne uwierzytelnianie za pomocą różnych opcji weryfikacji łatwe</span><span class="sxs-lookup"><span data-stu-id="2475c-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="2475c-341">Odgrywa kluczową rolę w przygotowywanie organizacji do ochrony i odzyskiwania z dokonywania konta</span><span class="sxs-lookup"><span data-stu-id="2475c-341">Plays a key role in preparing your organization to protect and recover from account compromises</span></span>

<span data-ttu-id="2475c-342">![Zasady użytkownika ridk](./media/active-directory-identityprotection/1019.png "zasady ridk użytkownika")</span><span class="sxs-lookup"><span data-stu-id="2475c-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="2475c-343">Aby uzyskać więcej informacji, zobacz [co to jest uwierzytelnianie wieloskładnikowe Azure?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2475c-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="2475c-344">Azure AD Identity Protection pomaga w zarządzaniu wdrożenie uwierzytelniania wieloskładnikowego rejestracji przez skonfigurowanie zasad, które umożliwia:</span><span class="sxs-lookup"><span data-stu-id="2475c-344">Azure AD Identity Protection helps you manage the roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="2475c-345">Ustaw użytkowników i grup, których dotyczy zasada:</span><span class="sxs-lookup"><span data-stu-id="2475c-345">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="2475c-346">![Zasady MFA](./media/active-directory-identityprotection/1020.png "zasad MFA")</span><span class="sxs-lookup"><span data-stu-id="2475c-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="2475c-347">Ustawianie formantów, które mają być egzekwowane, gdy zasady wyzwala::</span><span class="sxs-lookup"><span data-stu-id="2475c-347">Set the controls to be enforced when the policy triggers::</span></span>  

    <span data-ttu-id="2475c-348">![Zasady MFA](./media/active-directory-identityprotection/1021.png "zasad MFA")</span><span class="sxs-lookup"><span data-stu-id="2475c-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="2475c-349">Przełącz stan tej zasady:</span><span class="sxs-lookup"><span data-stu-id="2475c-349">Switch the state of your policy:</span></span>

    <span data-ttu-id="2475c-350">![Zasady MFA](./media/active-directory-identityprotection/403.png "zasad MFA")</span><span class="sxs-lookup"><span data-stu-id="2475c-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="2475c-351">Wyświetl bieżący stan rejestracji:</span><span class="sxs-lookup"><span data-stu-id="2475c-351">View the current registration status:</span></span>

    <span data-ttu-id="2475c-352">![Zasady MFA](./media/active-directory-identityprotection/1022.png "zasad MFA")</span><span class="sxs-lookup"><span data-stu-id="2475c-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="2475c-353">Omówienie powiązane funkcje użytkownika Zobacz:</span><span class="sxs-lookup"><span data-stu-id="2475c-353">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="2475c-354">[Uwierzytelnianie wieloskładnikowe rejestracji przepływu](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="2475c-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="2475c-355">[Logowanie napotyka przy użyciu usługi Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span><span class="sxs-lookup"><span data-stu-id="2475c-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="2475c-356">**Aby otworzyć okno dialogowe elementami konfiguracji**:</span><span class="sxs-lookup"><span data-stu-id="2475c-356">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="2475c-357">Na **Azure AD Identity Protection** bloku, w **Konfiguruj** kliknij **rejestracji usługi Multi-Factor authentication**.</span><span class="sxs-lookup"><span data-stu-id="2475c-357">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="2475c-358">![Zasady MFA](./media/active-directory-identityprotection/1019.png "zasad MFA")</span><span class="sxs-lookup"><span data-stu-id="2475c-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="2475c-359">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2475c-359">Next steps</span></span>
* [<span data-ttu-id="2475c-360">Kanał 9: Usługi Azure AD i Pokaż tożsamości: Podgląd ochrony tożsamości</span><span class="sxs-lookup"><span data-stu-id="2475c-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="2475c-361">Włączenie ochrony tożsamości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2475c-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="2475c-362">Luk w zabezpieczeniach wykrywanych przez usługę Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="2475c-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="2475c-363">Zdarzenia o podwyższonym ryzyku Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2475c-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="2475c-364">Azure Active Directory Identity Protection powiadomienia</span><span class="sxs-lookup"><span data-stu-id="2475c-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="2475c-365">Azure podręcznikowym ochronę tożsamości w usłudze Active Directory</span><span class="sxs-lookup"><span data-stu-id="2475c-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="2475c-366">Azure Active Directory Identity Protection słownik</span><span class="sxs-lookup"><span data-stu-id="2475c-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="2475c-367">Logowanie, korzystając z usługi Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="2475c-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="2475c-368">Azure Active Directory Identity Protection — sposób odblokowania użytkowników</span><span class="sxs-lookup"><span data-stu-id="2475c-368">Azure Active Directory Identity Protection - How to unblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="2475c-369">Wprowadzenie do usługi Azure Active Directory Identity Protection oraz Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="2475c-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
