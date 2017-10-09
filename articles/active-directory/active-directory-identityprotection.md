---
title: "aaaAzure ochronę tożsamości w usłudze Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Azure AD Identity Protection umożliwia zdolność hello toolimit tooexploit osoba atakująca, którego bezpieczeństwo zostało naruszone tożsamości lub urządzenie i toosecure tożsamości lub urządzenia, które wcześniej były toobe podejrzenia lub znanych naruszenia zabezpieczeń."
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
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="096f1-104">Ochrona tożsamości w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="096f1-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="096f1-105">Azure Active Directory Identity Protection to funkcja wersji hello Azure AD Premium P2, które umożliwia:</span><span class="sxs-lookup"><span data-stu-id="096f1-105">Azure Active Directory Identity Protection is a feature of hello Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="096f1-106">Wykrywanie potencjalnych luk w zabezpieczeniach wpływających na tożsamości organizacji</span><span class="sxs-lookup"><span data-stu-id="096f1-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="096f1-107">Skonfiguruj automatyczne odpowiedzi toodetected podejrzane akcji, które są powiązane tooyour organizacji tożsamości</span><span class="sxs-lookup"><span data-stu-id="096f1-107">Configure automated responses toodetected suspicious actions that are related tooyour organization’s identities</span></span>  

- <span data-ttu-id="096f1-108">Zbadaj podejrzane zdarzenia i podejmij odpowiednią akcję tooresolve je</span><span class="sxs-lookup"><span data-stu-id="096f1-108">Investigate suspicious incidents and take appropriate action tooresolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="096f1-109">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="096f1-109">Getting started</span></span>

<span data-ttu-id="096f1-110">Firma Microsoft zabezpiecza oparte na chmurze tożsamości przez ponad dekadę.</span><span class="sxs-lookup"><span data-stu-id="096f1-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="096f1-111">Z usługi Azure Active Directory Identity Protection, w danym środowisku, możesz użyć hello korzysta z tej samej ochrony systemy Microsoft toosecure tożsamości.</span><span class="sxs-lookup"><span data-stu-id="096f1-111">With Azure Active Directory Identity Protection, in your environment, you can use hello same protection systems Microsoft uses toosecure identities.</span></span>

<span data-ttu-id="096f1-112">Większość Hello zabezpieczeń potrwać naruszeń miejsce, gdy osoby atakujące uzyskania dostępu do środowiska tooan kradzieży tożsamości użytkownika.</span><span class="sxs-lookup"><span data-stu-id="096f1-112">hello vast majority of security breaches take place when attackers gain access tooan environment by stealing a user’s identity.</span></span> <span data-ttu-id="096f1-113">Latach hello osoby atakujące stały się coraz bardziej skuteczne w wykorzystaniu naruszeń innych firm i za pomocą zaawansowanej wyłudzania.</span><span class="sxs-lookup"><span data-stu-id="096f1-113">Over hello years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="096f1-114">Gdy osoba atakująca uzyska dostęp do konta użytkownika uprzywilejowanego niskiego tooeven, są one względnie łatwe im dostęp do toogain tooimportant zasobów firmowych za pośrednictwem penetracji sieci.</span><span class="sxs-lookup"><span data-stu-id="096f1-114">As soon as an attacker gains access tooeven low privileged user accounts, it is relatively easy for them toogain access tooimportant company resources through lateral movement.</span></span>

<span data-ttu-id="096f1-115">W wyniku tego należy:</span><span class="sxs-lookup"><span data-stu-id="096f1-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="096f1-116">Ochrona wszystkich tożsamości, niezależnie od ich poziom uprawnień</span><span class="sxs-lookup"><span data-stu-id="096f1-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="096f1-117">Aktywne uniemożliwić złamany tożsamości są użyte</span><span class="sxs-lookup"><span data-stu-id="096f1-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="096f1-118">Odnajdywanie złamany tożsamości jest bez łatwe zadania.</span><span class="sxs-lookup"><span data-stu-id="096f1-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="096f1-119">Azure Active Directory korzysta z algorytmów uczenia maszynowego adaptacyjną i nieprawidłowości toodetect Algorytm heurystyczny i podejrzane zdarzenia, które wskazują potencjalnie naruszony tożsamości.</span><span class="sxs-lookup"><span data-stu-id="096f1-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="096f1-120">Przy użyciu tych danych, Identity Protection generuje raporty i alerty, które umożliwiają tooevaluate hello wykrytych problemów i podjąć odpowiednie środki zaradcze lub akcji korygowania.</span><span class="sxs-lookup"><span data-stu-id="096f1-120">Using this data, Identity Protection generates reports and alerts that enable you tooevaluate hello detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="096f1-121">Azure Active Directory Identity Protection jest większa niż monitorowania i raportowania narzędzia.</span><span class="sxs-lookup"><span data-stu-id="096f1-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="096f1-122">tooprotect tożsamości organizacji, można skonfigurować zasady stosowane na podstawie ryzyka odpowiadające automatycznie toodetected problemów, gdy zostanie osiągnięty poziom ryzyka określony.</span><span class="sxs-lookup"><span data-stu-id="096f1-122">tooprotect your organization's identities, you can configure risk-based policies that automatically respond toodetected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="096f1-123">Te zasady dodatkowo tooother warunkowy dostęp do formantów zapewniane przez usługę Azure Active Directory i EMS, można automatycznie blokować lub zainicjować akcji korygowania adaptacyjną tym resetowanie haseł i wymuszania uwierzytelnianie wieloskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="096f1-123">These policies, in addition tooother conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="096f1-124">Funkcje ochrony tożsamości</span><span class="sxs-lookup"><span data-stu-id="096f1-124">Identity Protection capabilities</span></span>

<span data-ttu-id="096f1-125">**Wykrywanie luk w zabezpieczeniach i ryzykowne kont:**</span><span class="sxs-lookup"><span data-stu-id="096f1-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="096f1-126">Udostępnia zalecenia niestandardowych tooimprove ogólny stan zabezpieczeń przez wyróżnianie luk w zabezpieczeniach</span><span class="sxs-lookup"><span data-stu-id="096f1-126">Providing custom recommendations tooimprove overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="096f1-127">Obliczanie poziomów ryzyka do logowania</span><span class="sxs-lookup"><span data-stu-id="096f1-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="096f1-128">Obliczanie poziomów ryzyka użytkownika</span><span class="sxs-lookup"><span data-stu-id="096f1-128">Calculating user risk levels</span></span>


<span data-ttu-id="096f1-129">**Badanie zdarzenia ryzyka:**</span><span class="sxs-lookup"><span data-stu-id="096f1-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="096f1-130">Wysyłanie powiadomienia o zdarzeniach ryzyka</span><span class="sxs-lookup"><span data-stu-id="096f1-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="096f1-131">Badania ryzyka zdarzeń za pomocą odpowiednich i kontekstowych informacji</span><span class="sxs-lookup"><span data-stu-id="096f1-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="096f1-132">Zapewnienie podstawowych przepływów pracy dochodzenia tootrack</span><span class="sxs-lookup"><span data-stu-id="096f1-132">Providing basic workflows tootrack investigations</span></span>
* <span data-ttu-id="096f1-133">Zapewniając łatwy dostęp tooremediation akcji, takich jak Resetowanie hasła</span><span class="sxs-lookup"><span data-stu-id="096f1-133">Providing easy access tooremediation actions such as password reset</span></span>

<span data-ttu-id="096f1-134">**Zasady dostępu warunkowego opartego na ryzyka:**</span><span class="sxs-lookup"><span data-stu-id="096f1-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="096f1-135">Zasady toomitigate ryzykowne logowania przez blokowanie logowania lub wymaganie uwierzytelniania wieloskładnikowego wyzwania.</span><span class="sxs-lookup"><span data-stu-id="096f1-135">Policy toomitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="096f1-136">Zasady tooblock lub kont użytkowników ryzykowne bezpieczne</span><span class="sxs-lookup"><span data-stu-id="096f1-136">Policy tooblock or secure risky user accounts</span></span>
* <span data-ttu-id="096f1-137">Zasady toorequire użytkowników tooregister uwierzytelnianie wieloskładnikowe</span><span class="sxs-lookup"><span data-stu-id="096f1-137">Policy toorequire users tooregister for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="096f1-138">Role ochrony tożsamości</span><span class="sxs-lookup"><span data-stu-id="096f1-138">Identity Protection roles</span></span>

<span data-ttu-id="096f1-139">tooload saldo hello działania związane z zarządzaniem wokół implementacji ochronę tożsamości, można przypisać kilku ról.</span><span class="sxs-lookup"><span data-stu-id="096f1-139">tooload balance hello management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="096f1-140">Azure AD Identity Protection obsługuje 3 role katalogu:</span><span class="sxs-lookup"><span data-stu-id="096f1-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="096f1-141">Rola</span><span class="sxs-lookup"><span data-stu-id="096f1-141">Role</span></span>                         | <span data-ttu-id="096f1-142">Możliwość</span><span class="sxs-lookup"><span data-stu-id="096f1-142">Can do</span></span>                          | <span data-ttu-id="096f1-143">Nie można wykonać</span><span class="sxs-lookup"><span data-stu-id="096f1-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="096f1-144">Administrator globalny</span><span class="sxs-lookup"><span data-stu-id="096f1-144">Global administrator</span></span>         | <span data-ttu-id="096f1-145">Pełny dostęp tooIdentity ochrony, dołączyć Identity Protection</span><span class="sxs-lookup"><span data-stu-id="096f1-145">Full access tooIdentity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="096f1-146">Administrator zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="096f1-146">Security administrator</span></span>       | <span data-ttu-id="096f1-147">Pełny dostęp tooIdentity ochrony</span><span class="sxs-lookup"><span data-stu-id="096f1-147">Full access tooIdentity Protection</span></span> | <span data-ttu-id="096f1-148">Dołączyć ochronę tożsamości, zresetuj hasła dla użytkownika</span><span class="sxs-lookup"><span data-stu-id="096f1-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="096f1-149">Czytelnik zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="096f1-149">Security reader</span></span>              | <span data-ttu-id="096f1-150">Dostęp tylko do gotowe tooIdentity ochrony</span><span class="sxs-lookup"><span data-stu-id="096f1-150">Ready-only access tooIdentity Protection</span></span> | <span data-ttu-id="096f1-151">Dołączyć ochronę tożsamości użytkowników remidiate skonfigurować zasady, resetowania haseł</span><span class="sxs-lookup"><span data-stu-id="096f1-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="096f1-152">Aby uzyskać więcej informacji, zobacz [przypisywanie ról administratorów w usłudze Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="096f1-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="096f1-153">Wykrywanie</span><span class="sxs-lookup"><span data-stu-id="096f1-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="096f1-154">Luki w zabezpieczeniach</span><span class="sxs-lookup"><span data-stu-id="096f1-154">Vulnerabilities</span></span>

<span data-ttu-id="096f1-155">Azure Active Directory Identity Protection analizy konfiguracji i wykrywa luk w zabezpieczeniach, które mogą mieć wpływ na tożsamości użytkownika.</span><span class="sxs-lookup"><span data-stu-id="096f1-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="096f1-156">Aby uzyskać więcej informacji, zobacz [luk w zabezpieczeniach wykrywanych przez usługę Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="096f1-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="096f1-157">Zdarzenia ryzyka</span><span class="sxs-lookup"><span data-stu-id="096f1-157">Risk events</span></span>

<span data-ttu-id="096f1-158">Azure Active Directory korzysta z adaptacyjną uczenia algorytmów i heurystyki toodetect podejrzane akcji, które są tożsamości użytkownika powiązanych tooyour maszynowego.</span><span class="sxs-lookup"><span data-stu-id="096f1-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user's identities.</span></span> <span data-ttu-id="096f1-159">Witaj system tworzy rekord dla każdego wykrytego podejrzane działania.</span><span class="sxs-lookup"><span data-stu-id="096f1-159">hello system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="096f1-160">Te rekordy są także nazywane zdarzenia ryzyka.</span><span class="sxs-lookup"><span data-stu-id="096f1-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="096f1-161">Aby uzyskać więcej informacji, zobacz [Zdarzenia o podwyższonym ryzyku w usłudze Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="096f1-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="096f1-162">Badanie</span><span class="sxs-lookup"><span data-stu-id="096f1-162">Investigation</span></span>
<span data-ttu-id="096f1-163">Podróży za pomocą ochrony tożsamości zwykle zaczyna się od hello ochronę tożsamości z pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="096f1-163">Your journey through Identity Protection typically starts with hello Identity Protection dashboard.</span></span>

<span data-ttu-id="096f1-164">![Korygowanie](./media/active-directory-identityprotection/1000.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="096f1-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="096f1-165">pulpit nawigacyjny Hello daje dostęp do:</span><span class="sxs-lookup"><span data-stu-id="096f1-165">hello dashboard gives you access to:</span></span>

* <span data-ttu-id="096f1-166">Raporty takie jak **użytkownicy oflagowani ryzyka**, **ryzyka zdarzenia** i **luk w zabezpieczeniach**</span><span class="sxs-lookup"><span data-stu-id="096f1-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="096f1-167">Ustawienia, takie jak konfiguracja hello Twojej **zasady zabezpieczeń**, **powiadomienia** i **rejestracji usługi Multi-Factor authentication**</span><span class="sxs-lookup"><span data-stu-id="096f1-167">Settings such as hello configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="096f1-168">Zwykle to punkt startowy dochodzenia, które jest procesem hello sprawdzania hello działań, dzienniki i inne istotne informacje pokrewne tooa ryzyka toodecide zdarzeń czy korygowania lub migracji kroki są niezbędne, i jak został hello tożsamości uszkodzone i zrozumieć, jak hello naruszony tożsamości została użyta.</span><span class="sxs-lookup"><span data-stu-id="096f1-168">It is typically your starting point for investigation, which is hello process of reviewing hello activities, logs, and other relevant information related tooa risk event toodecide whether remediation or mitigation steps are necessary,  and how hello identity was compromised, and understand how hello compromised identity was used.</span></span>

<span data-ttu-id="096f1-169">Można powiązać Twoje toohello działania dochodzenia [powiadomienia](active-directory-identityprotection-notifications.md) usługi Azure Active Directory Protection wysyła na wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="096f1-169">You can tie your investigation activities toohello [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="096f1-170">Witaj następujące sekcje zawierają bardziej szczegółowe informacje i hello kroki, które są powiązane tooan dochodzenia.</span><span class="sxs-lookup"><span data-stu-id="096f1-170">hello following sections provide you with more details and hello steps that are related tooan investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="096f1-171">Ryzykowne logowania</span><span class="sxs-lookup"><span data-stu-id="096f1-171">Risky sign-ins</span></span>

<span data-ttu-id="096f1-172">Usługa Azure Active Directory wykryje [ryzyka typów zdarzeń](active-directory-reporting-risk-events.md#risk-event-types) w czasie rzeczywistym i w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="096f1-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="096f1-173">Każde zdarzenie zagrożenia wykrytego dla logowanie użytkownika wspiera tooa pojęcie logiczne o nazwie ryzykowne logowania.</span><span class="sxs-lookup"><span data-stu-id="096f1-173">Each risk event that has been detected for a sign-in of a user contributes tooa logical concept called risky sign-in.</span></span> <span data-ttu-id="096f1-174">Ryzykowne logowanie jest wskaźnik prób logowania, które nie mogły zostać wykonane przez właściciela uzasadnionych hello konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="096f1-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by hello legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="096f1-175">Poziom ryzyka logowania</span><span class="sxs-lookup"><span data-stu-id="096f1-175">Sign-in risk level</span></span>

<span data-ttu-id="096f1-176">Poziom ryzyka logowania jest wskazaniem (wysoki, średni lub niski) prawdopodobieństwo hello próba logowania nie została wykonana przez właściciela uzasadnionych hello konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="096f1-176">A sign-in risk level is an indication (High, Medium, or Low) of hello likelihood that a sign-in attempt was not performed by hello legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="096f1-177">Zmniejszenia zdarzenia logowania ryzyka</span><span class="sxs-lookup"><span data-stu-id="096f1-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="096f1-178">Środki zaradcze jest możliwość hello toolimit akcji tooexploit atakująca złamany tożsamości lub urządzenia bez przywracania hello tożsamości lub urządzenie tooa bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="096f1-178">A mitigation is an action toolimit hello ability of an attacker tooexploit a compromised identity or device without restoring hello identity or device tooa safe state.</span></span> <span data-ttu-id="096f1-179">Środki zaradcze nie można rozpoznać poprzednie zdarzenia logowania ryzyko związane z tożsamości hello lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="096f1-179">A mitigation does not resolve previous sign-in risk events associated with hello identity or device.</span></span>

<span data-ttu-id="096f1-180">toomitigate ryzykowne logowania automatycznie, można skonfigurować policicies zabezpieczeń logowania ryzyka.</span><span class="sxs-lookup"><span data-stu-id="096f1-180">toomitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="096f1-181">Korzystając z tych zasad, należy wziąć pod uwagę poziom ryzyka hello hello użytkownika lub hello logowania tooblock ryzykowne logowania lub wymusić uwierzytelnianie wieloskładnikowe tooperform użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="096f1-181">Using these policies, you consider hello risk level of hello user or hello sign-in tooblock risky sign-ins or require hello user tooperform multi-factor authentication.</span></span> <span data-ttu-id="096f1-182">Te akcje mogą uniemożliwiać osobie atakującej wykorzystanie uszkodzenia toocause kradzieży tożsamości i może dać niektórych tożsamości hello toosecure czasu.</span><span class="sxs-lookup"><span data-stu-id="096f1-182">These actions may prevent an attacker from exploiting a stolen identity toocause damage, and may give you some time toosecure hello identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="096f1-183">Zasady zabezpieczeń logowania ryzyka</span><span class="sxs-lookup"><span data-stu-id="096f1-183">Sign-in risk security policy</span></span>
<span data-ttu-id="096f1-184">Zasady logowania ryzyko jest zasady dostępu warunkowego, która ocenia hello ryzyka tooa określonych logowania i stosuje środki zaradcze, na podstawie wstępnie zdefiniowane warunki i zasady.</span><span class="sxs-lookup"><span data-stu-id="096f1-184">A sign-in risk policy is a conditional access policy that evaluates hello risk tooa specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="096f1-185">![Zasady logowania ryzyka](./media/active-directory-identityprotection/1014.png "logowania zasad ryzyka")</span><span class="sxs-lookup"><span data-stu-id="096f1-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="096f1-186">Azure AD Identity Protection pomaga w zarządzaniu hello zmniejszenie ryzykowne logowania umożliwiając:</span><span class="sxs-lookup"><span data-stu-id="096f1-186">Azure AD Identity Protection helps you manage hello mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="096f1-187">Ustaw hello użytkowników i grup hello zasady ma zastosowanie do:</span><span class="sxs-lookup"><span data-stu-id="096f1-187">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="096f1-188">![Zasady logowania ryzyka](./media/active-directory-identityprotection/1015.png "logowania zasad ryzyka")</span><span class="sxs-lookup"><span data-stu-id="096f1-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="096f1-189">Ustaw hello logowania ryzyka poziomu próg (niski, średni lub wysoki) wyzwalaną hello zasad:</span><span class="sxs-lookup"><span data-stu-id="096f1-189">Set hello sign-in risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="096f1-190">![Zasady logowania ryzyka](./media/active-directory-identityprotection/1016.png "logowania zasad ryzyka")</span><span class="sxs-lookup"><span data-stu-id="096f1-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="096f1-191">Toobe formanty hello zestaw wymuszane w przypadku wyzwala hello zasad:</span><span class="sxs-lookup"><span data-stu-id="096f1-191">Set hello controls toobe enforced when hello policy triggers:</span></span>  

    <span data-ttu-id="096f1-192">![Zasady logowania ryzyka](./media/active-directory-identityprotection/1017.png "logowania zasad ryzyka")</span><span class="sxs-lookup"><span data-stu-id="096f1-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="096f1-193">Przełącz stan hello zasad:</span><span class="sxs-lookup"><span data-stu-id="096f1-193">Switch hello state of your policy:</span></span>

    <span data-ttu-id="096f1-194">![Rejestracja usługi MFA](./media/active-directory-identityprotection/403.png "rejestracji usługi MFA")</span><span class="sxs-lookup"><span data-stu-id="096f1-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="096f1-195">Przegląd i ocena wpływu zmiany przed jej aktywowaniem hello:</span><span class="sxs-lookup"><span data-stu-id="096f1-195">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="096f1-196">![Zasady logowania ryzyka](./media/active-directory-identityprotection/1018.png "logowania zasad ryzyka")</span><span class="sxs-lookup"><span data-stu-id="096f1-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-tooknow"></a><span data-ttu-id="096f1-197">Co należy tooknow</span><span class="sxs-lookup"><span data-stu-id="096f1-197">What you need tooknow</span></span>
<span data-ttu-id="096f1-198">Można skonfigurować uwierzytelnianie wieloskładnikowe toorequire zasad logowania zagrożenia zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="096f1-198">You can configure a sign-in risk security policy toorequire multi-factor authentication:</span></span>

<span data-ttu-id="096f1-199">![Zasady logowania ryzyka](./media/active-directory-identityprotection/1017.png "logowania zasad ryzyka")</span><span class="sxs-lookup"><span data-stu-id="096f1-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="096f1-200">Jednak ze względu na bezpieczeństwo, to ustawienie działa tylko dla użytkowników, które zostały już zarejestrowane w usłudze Multi-Factor authentication.</span><span class="sxs-lookup"><span data-stu-id="096f1-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="096f1-201">Jeśli uwierzytelnianie wieloskładnikowe toorequire warunku hello jest spełniony dla użytkownika, który nie jest jeszcze zarejestrowany w usłudze Multi-Factor authentication, użytkownik hello jest zablokowany.</span><span class="sxs-lookup"><span data-stu-id="096f1-201">If hello condition toorequire multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, hello user is blocked.</span></span>

<span data-ttu-id="096f1-202">Najlepszym rozwiązaniem Jeśli chcesz, aby uwierzytelnianie wieloskładnikowe toorequire ryzykowne logowania, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="096f1-202">As a best practice, if you want toorequire multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="096f1-203">Włącz hello [zasady rejestracji usługi Multi-Factor authentication](#multi-factor-authentication-registration-policy) dla hello odpowiednich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="096f1-203">Enable hello [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for hello affected users.</span></span>
2. <span data-ttu-id="096f1-204">Wymagaj hello wpływ na użytkowników toologin w tooperform-ryzykowne sesji rejestracji usługi MFA</span><span class="sxs-lookup"><span data-stu-id="096f1-204">Require hello affected users toologin in a non-risky session tooperform a MFA registration</span></span>

<span data-ttu-id="096f1-205">Wykonanie tych kroków gwarantuje, że uwierzytelnianie wieloskładnikowe jest wymagany dla ryzykownych logowanie.</span><span class="sxs-lookup"><span data-stu-id="096f1-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="096f1-206">Najlepsze praktyki</span><span class="sxs-lookup"><span data-stu-id="096f1-206">Best practices</span></span>
<span data-ttu-id="096f1-207">Wybieranie **wysokiej** próg zmniejsza hello liczby zasad wyzwoleniu i minimalizuje hello toousers wpływu.</span><span class="sxs-lookup"><span data-stu-id="096f1-207">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>  

<span data-ttu-id="096f1-208">Jednak nie obejmuje **małej** i **średni** logowania oznaczona flagą narażone na powitania zasad, które nie mogą blokować osoba atakująca możliwości wykorzystania złamany tożsamości.</span><span class="sxs-lookup"><span data-stu-id="096f1-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from hello policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="096f1-209">Gdy ustawienie hello zasad,</span><span class="sxs-lookup"><span data-stu-id="096f1-209">When setting hello policy,</span></span>

* <span data-ttu-id="096f1-210">Wyklucz użytkowników, którzy nie / nie można wprowadzić uwierzytelnianie wieloskładnikowe</span><span class="sxs-lookup"><span data-stu-id="096f1-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="096f1-211">Wyklucz użytkowników, których Włączanie hello zasad nie jest praktyczne ustawień regionalnych (na przykład nie toohelpdesk dostępu)</span><span class="sxs-lookup"><span data-stu-id="096f1-211">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="096f1-212">Wyklucz użytkowników, którzy są prawdopodobnie toogenerate wiele alarmów false (deweloperów, analityków zabezpieczeń)</span><span class="sxs-lookup"><span data-stu-id="096f1-212">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="096f1-213">Użyj **wysokiej** próg podczas początkowej zasad zbiorczego, lub jeśli należy zminimalizować problemy, które zostały odebrane przez użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="096f1-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="096f1-214">Użyj **małej** progu, jeśli organizacja wymaga wyższego poziomu bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="096f1-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="096f1-215">Wybieranie **małej** próg wprowadzono dodatkowe użytkownika logowania wyzwania, ale zwiększyć bezpieczeństwo.</span><span class="sxs-lookup"><span data-stu-id="096f1-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="096f1-216">Hello zalecane domyślne dla większości organizacji jest tooconfigure regułę **średni** toostrike próg kompromis między użyteczność i zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="096f1-216">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="096f1-217">zasady logowania ryzyka Hello jest:</span><span class="sxs-lookup"><span data-stu-id="096f1-217">hello sign-in risk policy is:</span></span>

* <span data-ttu-id="096f1-218">Ruch przeglądarki tooall zastosowane i logowania korzystających z nowoczesnego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="096f1-218">Applied tooall browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="096f1-219">Nie zastosowano tooapplications przy użyciu starszych protokołów zabezpieczeń przez wyłączenie punktu końcowego usługi WS-Trust hello pod IDP hello federacyjne, takie jak usługi AD FS.</span><span class="sxs-lookup"><span data-stu-id="096f1-219">Not applied tooapplications using older security protocols by disabling hello WS-Trust endpoint at hello federated IDP, such as ADFS.</span></span>

<span data-ttu-id="096f1-220">Witaj **zdarzenia o podwyższonym ryzyku** w konsoli Identity Protection hello zawiera listę wszystkich zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="096f1-220">hello **Risk Events** page in hello Identity Protection console lists all events:</span></span>

* <span data-ttu-id="096f1-221">Ta zasada została zastosowana do</span><span class="sxs-lookup"><span data-stu-id="096f1-221">This policy was applied to</span></span>
* <span data-ttu-id="096f1-222">Można sprawdzić działanie hello i określenia, czy akcja hello się odpowiednie lub nie</span><span class="sxs-lookup"><span data-stu-id="096f1-222">You can review hello activity and determine whether hello action was appropriate or not</span></span>

<span data-ttu-id="096f1-223">Omówienie hello dotyczące środowiska użytkownika, zobacz:</span><span class="sxs-lookup"><span data-stu-id="096f1-223">For an overview of hello related user experience, see:</span></span>

* [<span data-ttu-id="096f1-224">Ryzykowne odzyskiwania logowania</span><span class="sxs-lookup"><span data-stu-id="096f1-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="096f1-225">Ryzykowne logowania zablokowane</span><span class="sxs-lookup"><span data-stu-id="096f1-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="096f1-226">Logowanie, korzystając z usługi Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="096f1-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="096f1-227">**okno dialogowe konfiguracji pokrewne hello tooopen**:</span><span class="sxs-lookup"><span data-stu-id="096f1-227">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="096f1-228">Na powitania **Azure AD Identity Protection** bloku w hello **Konfiguruj** kliknij **logowania zasad ryzyka**.</span><span class="sxs-lookup"><span data-stu-id="096f1-228">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="096f1-229">![Zasady użytkownika ridk](./media/active-directory-identityprotection/1014.png "zasady ridk użytkownika")</span><span class="sxs-lookup"><span data-stu-id="096f1-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="096f1-230">Użytkownicy oflagowani w związku z ryzykiem</span><span class="sxs-lookup"><span data-stu-id="096f1-230">Users flagged for risk</span></span>

<span data-ttu-id="096f1-231">Wszystkie aktywne [ryzyka zdarzenia](active-directory-identity-protection-risk-events.md) zostały wykryte przez usługę Azure Active Directory dla użytkownika współtworzyć tooa pojęcie logiczne o nazwie użytkownika ryzyka.</span><span class="sxs-lookup"><span data-stu-id="096f1-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute tooa logical concept called user risk.</span></span> <span data-ttu-id="096f1-232">Użytkownik oznaczona flagą ryzyko jest wskaźnikiem dla konta użytkownika, który może być zagrożone.</span><span class="sxs-lookup"><span data-stu-id="096f1-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![Użytkownicy oflagowani w związku z ryzykiem](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="096f1-234">Poziom ryzyka użytkownika</span><span class="sxs-lookup"><span data-stu-id="096f1-234">User risk level</span></span>

<span data-ttu-id="096f1-235">Poziom ryzyka użytkownika będzie wskazywać (wysoki, średni lub niski) prawdopodobieństwo hello tożsamości użytkownika hello został złamany.</span><span class="sxs-lookup"><span data-stu-id="096f1-235">A user risk level is an indication (High, Medium, or Low) of hello likelihood that hello user’s identity has been compromised.</span></span> <span data-ttu-id="096f1-236">Jego jest obliczany na podstawie zdarzeń hello ryzyka użytkownika, które są skojarzone z tożsamości użytkownika.</span><span class="sxs-lookup"><span data-stu-id="096f1-236">It is calculated based on hello user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="096f1-237">Witaj stan zdarzenia ryzyko jest **Active** lub **zamknięte**.</span><span class="sxs-lookup"><span data-stu-id="096f1-237">hello status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="096f1-238">Tylko ryzyka zdarzenia, które są **Active** współtworzenia obliczania poziomu ryzyka użytkownika toohello.</span><span class="sxs-lookup"><span data-stu-id="096f1-238">Only risk events that are **Active** contribute toohello user risk level calculation.</span></span>

<span data-ttu-id="096f1-239">poziom ryzyka użytkownika Hello jest obliczana przy użyciu hello następujące dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="096f1-239">hello user risk level is calculated using hello following inputs:</span></span>

* <span data-ttu-id="096f1-240">Zdarzenia aktywne ryzyka wpływające na powitania użytkownika</span><span class="sxs-lookup"><span data-stu-id="096f1-240">Active risk events impacting hello user</span></span>
* <span data-ttu-id="096f1-241">Poziom ryzyka tych zdarzeń</span><span class="sxs-lookup"><span data-stu-id="096f1-241">Risk level of these events</span></span>
* <span data-ttu-id="096f1-242">Określa, czy wykonano wszystkie akcje naprawcze wykonane</span><span class="sxs-lookup"><span data-stu-id="096f1-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="096f1-243">![Ryzyko użytkownika](./media/active-directory-identityprotection/1031.png "zagrożeń użytkownika")</span><span class="sxs-lookup"><span data-stu-id="096f1-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="096f1-244">Użyj hello użytkownika ryzyka poziomy toocreate zasad dostępu warunkowego blokujące ryzykowne użytkownikom logowanie lub Wymuś je toosecurely zmienić swoje hasło.</span><span class="sxs-lookup"><span data-stu-id="096f1-244">You can use hello user risk levels toocreate conditional access policies that block risky users from signing in, or force them toosecurely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="096f1-245">Zamknięcie zdarzenia o podwyższonym ryzyku ręcznie</span><span class="sxs-lookup"><span data-stu-id="096f1-245">Closing risk events manually</span></span>

<span data-ttu-id="096f1-246">W większości przypadków będzie wykonać akcje korygowania, takich jak zdarzenia Zamknij ryzyka tooautomatically resetowania hasła bezpiecznego.</span><span class="sxs-lookup"><span data-stu-id="096f1-246">In most cases, you will take remediation actions such as a secure password reset tooautomatically close risk events.</span></span> <span data-ttu-id="096f1-247">Jednak to może nie być możliwe.</span><span class="sxs-lookup"><span data-stu-id="096f1-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="096f1-248">Dotyczy, na przykład Witaj, gdy:</span><span class="sxs-lookup"><span data-stu-id="096f1-248">This is, for example, hello case, when:</span></span>

* <span data-ttu-id="096f1-249">Użytkownik z zdarzenia Active ryzyka został usunięty.</span><span class="sxs-lookup"><span data-stu-id="096f1-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="096f1-250">Badanie wykaże, że zdarzenie zagrożenia zgłoszony został wykonać przez wiarygodnego użytkownika hello</span><span class="sxs-lookup"><span data-stu-id="096f1-250">An investigation reveals that a reported risk event has been perform by hello legitimate user</span></span>

<span data-ttu-id="096f1-251">Ponieważ zdarzenia ryzyka, które są **Active** współtworzenia toohello użytkownika ryzyka obliczeń, może być toomanually obniżyć poziom ryzyka zamknięcie zdarzenia o podwyższonym ryzyku ręcznie.</span><span class="sxs-lookup"><span data-stu-id="096f1-251">Because risk events that are **Active** contribute toohello user risk calculation, you may have toomanually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="096f1-252">Podczas przebiegu hello dochodzenia można wybrać tootake żadnego z tych akcji toochange hello stan zdarzenia ryzyka:</span><span class="sxs-lookup"><span data-stu-id="096f1-252">During hello course of investigation, you can choose tootake any of these actions toochange hello status of a risk event:</span></span>

<span data-ttu-id="096f1-253">![Akcje](./media/active-directory-identityprotection/34.png "akcje")</span><span class="sxs-lookup"><span data-stu-id="096f1-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="096f1-254">**Rozwiąż** — Jeśli po zbadaniu zdarzenia ryzyka, trwało akcji korygowania odpowiednie poza ochrony tożsamości i uważasz, że zdarzenie ryzyka hello należy traktować jako zamknięte zdarzenie hello Oznacz jako rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="096f1-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that hello risk event should be considered closed, mark hello event as Resolved.</span></span> <span data-ttu-id="096f1-255">Zdarzenia rozwiązane ustawi tooClosed stan hello ryzyka zdarzeń i zdarzenia ryzyka hello przyczynia się już toouser ryzyka.</span><span class="sxs-lookup"><span data-stu-id="096f1-255">Resolved events will set hello risk event’s status tooClosed and hello risk event will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="096f1-256">**Oznacz jako fałszywie dodatnich** — w niektórych przypadkach można zbadać zdarzenia ryzyka i wykryć, czy został niepoprawnie oznaczone jako ryzykowne.</span><span class="sxs-lookup"><span data-stu-id="096f1-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="096f1-257">Można ograniczyć liczbę hello takimi wystąpieniami przez oznaczenie zdarzeń ryzyka hello jako fałszywie dodatnich.</span><span class="sxs-lookup"><span data-stu-id="096f1-257">You can help reduce hello number of such occurrences by marking hello risk event as False-positive.</span></span> <span data-ttu-id="096f1-258">Dzięki temu maszyny hello uczenia algorytmów tooimprove hello klasyfikacji podobnych zdarzeń w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="096f1-258">This will help hello machine learning algorithms tooimprove hello classification of similar events in hello future.</span></span> <span data-ttu-id="096f1-259">Stan Hello fałszywie dodatnich zdarzeń jest zbyt**zamknięte** i nie wpływają one toouser ryzyka.</span><span class="sxs-lookup"><span data-stu-id="096f1-259">hello status of false-positive events is too**Closed** and they will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="096f1-260">**Ignoruj** — Jeśli nie miały żadnych działań korygujących, ale mają hello usunięty z listy active hello toobe zdarzenia ryzyka, można oznaczyć zdarzeniem ryzyka Ignoruj i stan zdarzenia hello zostaną zamknięte.</span><span class="sxs-lookup"><span data-stu-id="096f1-260">**Ignore** - If you have not taken any remediation action, but want hello risk event toobe removed from hello active list, you can mark a risk event Ignore and hello event status will be Closed.</span></span> <span data-ttu-id="096f1-261">Zignorowano zdarzenia nie przyczyniają się toouser ryzyka.</span><span class="sxs-lookup"><span data-stu-id="096f1-261">Ignored events do not contribute toouser risk.</span></span> <span data-ttu-id="096f1-262">Tej opcji należy używać tylko w niezwykłych okolicznościach.</span><span class="sxs-lookup"><span data-stu-id="096f1-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="096f1-263">**Uaktywnij ponownie** -ryzyka zdarzenia, które zostały ręcznie zamknięty (przez wybranie **rozwiązać**, **wynik fałszywie dodatni**, lub **Ignoruj**) można ponownie uaktywnić, ustawienie hello zdarzenia stanu z powrotem zbyt**Active**.</span><span class="sxs-lookup"><span data-stu-id="096f1-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting hello event status back too**Active**.</span></span> <span data-ttu-id="096f1-264">Zdarzenia ponownie uaktywnione ryzyka współtworzenia obliczania poziomu ryzyka użytkownika toohello.</span><span class="sxs-lookup"><span data-stu-id="096f1-264">Reactivated risk events contribute toohello user risk level calculation.</span></span> <span data-ttu-id="096f1-265">Nie można ponownie uaktywnić zamknięte przy użyciu funkcji korygowania (takie jak resetowania hasła bezpiecznego) zdarzenia ryzyka.</span><span class="sxs-lookup"><span data-stu-id="096f1-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="096f1-266">**okno dialogowe konfiguracji pokrewne hello tooopen**:</span><span class="sxs-lookup"><span data-stu-id="096f1-266">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="096f1-267">Na powitania **Azure AD Identity Protection** bloku, w obszarze **zbadaj**, kliknij przycisk **ryzyka zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="096f1-267">On hello **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="096f1-268">![Resetowania hasła ręczne](./media/active-directory-identityprotection/1002.png "resetowania hasła ręczne")</span><span class="sxs-lookup"><span data-stu-id="096f1-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="096f1-269">W hello **ryzyka zdarzenia** kliknij zagrożenie.</span><span class="sxs-lookup"><span data-stu-id="096f1-269">In hello **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="096f1-270">![Resetowania hasła ręczne](./media/active-directory-identityprotection/1003.png "resetowania hasła ręczne")</span><span class="sxs-lookup"><span data-stu-id="096f1-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="096f1-271">W bloku ryzyka hello kliknij prawym przyciskiem myszy przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="096f1-271">On hello risk blade, right-click a user.</span></span>

    <span data-ttu-id="096f1-272">![Resetowania hasła ręczne](./media/active-directory-identityprotection/1004.png "resetowania hasła ręczne")</span><span class="sxs-lookup"><span data-stu-id="096f1-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="096f1-273">Ręczne zamknięcie wszystkich zdarzeń ryzyka dla użytkownika</span><span class="sxs-lookup"><span data-stu-id="096f1-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="096f1-274">Zamiast ręcznie indywidualnie zamknięcie zdarzenia ryzyka dla użytkownika, Azure Active Directory Identity Protection zapewnia także tooclose metody wszystkie zdarzenia dla użytkownika z jednego kliknięcia.</span><span class="sxs-lookup"><span data-stu-id="096f1-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method tooclose all events for a user with one click.</span></span>

<span data-ttu-id="096f1-275">![Akcje](./media/active-directory-identityprotection/2222.png "akcje")</span><span class="sxs-lookup"><span data-stu-id="096f1-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="096f1-276">Po kliknięciu **odrzucić wszystkie zdarzenia**, wszystkie zdarzenia zostaną zamknięte i hello dotyczy użytkownika nie jest już na ryzyko.</span><span class="sxs-lookup"><span data-stu-id="096f1-276">When you click **Dismiss all events**, all events are closed and hello affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="096f1-277">Zdarzenia o podwyższonym ryzyku korygując użytkownika</span><span class="sxs-lookup"><span data-stu-id="096f1-277">Remediating user risk events</span></span>

<span data-ttu-id="096f1-278">Korygowanie jest toosecure akcji tożsamości lub urządzeń, które wcześniej podejrzenia lub znane toobe naruszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="096f1-278">A remediation is an action toosecure an identity or a device that was previously suspected or known toobe compromised.</span></span> <span data-ttu-id="096f1-279">Akcja korygowania przywraca hello tożsamości lub urządzenie tooa bezpieczne i usuwa poprzednie zdarzenia ryzyko związane z tożsamości hello lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="096f1-279">A remediation action restores hello identity or device tooa safe state, and resolves previous risk events associated with hello identity or device.</span></span>

<span data-ttu-id="096f1-280">zdarzenia o podwyższonym ryzyku użytkownika tooremediate, można:</span><span class="sxs-lookup"><span data-stu-id="096f1-280">tooremediate user risk events, you can:</span></span>

* <span data-ttu-id="096f1-281">Wykonaj ręcznie zdarzenia ryzyka bezpieczne hasło resetowania tooremediate użytkownika</span><span class="sxs-lookup"><span data-stu-id="096f1-281">Perform a secure password reset tooremediate user risk events manually</span></span>
* <span data-ttu-id="096f1-282">Konfigurowanie toomitigate zasad użytkownika zagrożenia zabezpieczeń lub automatycznie korygować zdarzenia o podwyższonym ryzyku użytkownika</span><span class="sxs-lookup"><span data-stu-id="096f1-282">Configure a user risk security policy toomitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="096f1-283">Ponowne instalowanie obrazu hello zainfekowanych urządzeń</span><span class="sxs-lookup"><span data-stu-id="096f1-283">Re-image hello infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="096f1-284">Resetowanie ręczne bezpiecznego hasła</span><span class="sxs-lookup"><span data-stu-id="096f1-284">Manual secure password reset</span></span>
<span data-ttu-id="096f1-285">Bezpieczne hasło jest skuteczne korygowania w przypadku wielu zdarzeń ryzyka i wykonywana, automatycznie powoduje zamknięcie zdarzenia o podwyższonym ryzyku i ponownie oblicza poziom ryzyka hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="096f1-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates hello user risk level.</span></span> <span data-ttu-id="096f1-286">Możesz użyć hello Identity Protection pulpitu nawigacyjnego tooinitiate resetowania hasła dla użytkownika ryzykowne.</span><span class="sxs-lookup"><span data-stu-id="096f1-286">You can use hello Identity Protection dashboard tooinitiate a password reset for a risky user.</span></span>

<span data-ttu-id="096f1-287">określone okno Hello zapewnia dwie różne metody tooreset hasła:</span><span class="sxs-lookup"><span data-stu-id="096f1-287">hello related dialog provides two different methods tooreset a password:</span></span>

<span data-ttu-id="096f1-288">**Zresetuj hasło** — wybierz tę opcję **wymagają hasła hello użytkownika tooreset** tooallow hello odzyskiwania tooself użytkownika, jeśli użytkownik hello został zarejestrowany w usłudze Multi-Factor authentication.</span><span class="sxs-lookup"><span data-stu-id="096f1-288">**Reset password** - Select **Require hello user tooreset their password** tooallow hello user tooself-recover if hello user has registered for multi-factor authentication.</span></span> <span data-ttu-id="096f1-289">Podczas użytkownika hello następnym logowaniu użytkownik hello będzie toosolve wymagane uwierzytelnianie wieloskładnikowe pomyślnie testu i następnie, wymuszony toochange hello hasła.</span><span class="sxs-lookup"><span data-stu-id="096f1-289">During hello user's next sign-in, hello user will be required toosolve a multi-factor authentication challenge successfully and then, forced toochange hello password.</span></span> <span data-ttu-id="096f1-290">Ta opcja jest niedostępna, jeśli hello konto użytkownika nie jest już zarejestrowany uwierzytelnianie wieloskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="096f1-290">This option isn't available if hello user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="096f1-291">**Hasło tymczasowe** — wybierz tę opcję **wygenerować hasło tymczasowe** tooimmediately unieważnienie hello istniejące hasło, a następnie utwórz nowe hasło tymczasowe hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="096f1-291">**Temporary password** - Select **Generate a temporary password** tooimmediately invalidate hello existing password, and create a new temporary password for hello user.</span></span> <span data-ttu-id="096f1-292">Wyślij hello nowe hasło tymczasowe tooan alternatywny adres e-mail użytkownika hello lub Menedżera toohello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="096f1-292">Send hello new temporary password tooan alternate email address for hello user or toohello user's manager.</span></span> <span data-ttu-id="096f1-293">Ponieważ hasło hello jest tymczasowy, użytkownik hello będzie toochange zostanie wyświetlony monit o hasło hello podawane podczas logowania.</span><span class="sxs-lookup"><span data-stu-id="096f1-293">Because hello password is temporary, hello user will be prompted toochange hello password upon sign-in.</span></span>

<span data-ttu-id="096f1-294">![Zasady](./media/active-directory-identityprotection/1005.png "zasad")</span><span class="sxs-lookup"><span data-stu-id="096f1-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="096f1-295">**okno dialogowe konfiguracji pokrewne hello tooopen**:</span><span class="sxs-lookup"><span data-stu-id="096f1-295">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="096f1-296">Na powitania **Azure AD Identity Protection** bloku, kliknij przycisk **użytkownicy oflagowani ryzyka**.</span><span class="sxs-lookup"><span data-stu-id="096f1-296">On hello **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="096f1-297">![Resetowania hasła ręczne](./media/active-directory-identityprotection/1006.png "resetowania hasła ręczne")</span><span class="sxs-lookup"><span data-stu-id="096f1-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="096f1-298">Z listy hello użytkowników wybierz użytkownika z ryzyka co najmniej jednego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="096f1-298">From hello list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="096f1-299">![Resetowania hasła ręczne](./media/active-directory-identityprotection/1007.png "resetowania hasła ręczne")</span><span class="sxs-lookup"><span data-stu-id="096f1-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="096f1-300">W bloku użytkownika hello, kliknij **resetowania hasła**.</span><span class="sxs-lookup"><span data-stu-id="096f1-300">On hello user blade, click **Reset password**.</span></span>

    <span data-ttu-id="096f1-301">![Resetowania hasła ręczne](./media/active-directory-identityprotection/1008.png "resetowania hasła ręczne")</span><span class="sxs-lookup"><span data-stu-id="096f1-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="096f1-302">Zasady zabezpieczeń użytkownika ryzyka</span><span class="sxs-lookup"><span data-stu-id="096f1-302">User risk security policy</span></span>
<span data-ttu-id="096f1-303">Zasady zabezpieczeń użytkownika ryzyko jest zasady dostępu warunkowego, które ocenia hello ryzyka tooa poziomu określonego użytkownika, a następnie stosuje akcje korygowania i środki zaradcze, na podstawie wstępnie zdefiniowane warunki i zasady.</span><span class="sxs-lookup"><span data-stu-id="096f1-303">A user risk security policy is a conditional access policy that evaluates hello risk level tooa specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="096f1-304">![Zasady użytkownika ridk](./media/active-directory-identityprotection/1009.png "zasady ridk użytkownika")</span><span class="sxs-lookup"><span data-stu-id="096f1-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="096f1-305">Azure AD Identity Protection pomaga w zarządzaniu łagodzenia hello i korygowania oflagowane ryzyka, umożliwiając użytkownikom:</span><span class="sxs-lookup"><span data-stu-id="096f1-305">Azure AD Identity Protection helps you manage hello mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="096f1-306">Ustaw hello użytkowników i grup hello zasady ma zastosowanie do:</span><span class="sxs-lookup"><span data-stu-id="096f1-306">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="096f1-307">![Zasady użytkownika ridk](./media/active-directory-identityprotection/1010.png "zasady ridk użytkownika")</span><span class="sxs-lookup"><span data-stu-id="096f1-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="096f1-308">Ustaw hello użytkownika ryzyka poziomu próg (niski, średni lub wysoki) wyzwalaną hello zasad:</span><span class="sxs-lookup"><span data-stu-id="096f1-308">Set hello user risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="096f1-309">![Zasady użytkownika ridk](./media/active-directory-identityprotection/1011.png "zasady ridk użytkownika")</span><span class="sxs-lookup"><span data-stu-id="096f1-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="096f1-310">Toobe formanty hello zestaw wymuszane w przypadku wyzwala hello zasad:</span><span class="sxs-lookup"><span data-stu-id="096f1-310">Set hello controls toobe enforced when hello policy triggers:</span></span>

    <span data-ttu-id="096f1-311">![Zasady użytkownika ridk](./media/active-directory-identityprotection/1012.png "zasady ridk użytkownika")</span><span class="sxs-lookup"><span data-stu-id="096f1-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="096f1-312">Przełącz stan hello zasad:</span><span class="sxs-lookup"><span data-stu-id="096f1-312">Switch hello state of your policy:</span></span>

    <span data-ttu-id="096f1-313">![Zasady użytkownika ridk](./media/active-directory-identityprotection/403.png "rejestracji usługi MFA")</span><span class="sxs-lookup"><span data-stu-id="096f1-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="096f1-314">Przegląd i ocena wpływu zmiany przed jej aktywowaniem hello:</span><span class="sxs-lookup"><span data-stu-id="096f1-314">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="096f1-315">![Zasady użytkownika ridk](./media/active-directory-identityprotection/1013.png "zasady ridk użytkownika")</span><span class="sxs-lookup"><span data-stu-id="096f1-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="096f1-316">Wybieranie **wysokiej** próg zmniejsza hello liczby zasad wyzwoleniu i minimalizuje hello toousers wpływu.</span><span class="sxs-lookup"><span data-stu-id="096f1-316">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>
<span data-ttu-id="096f1-317">Jednak nie obejmuje **małej** i **średni** użytkowników oznaczona flagą narażone na powitania zasad, które mogą nie zapewnić tożsamości lub urządzenia, który zostały wcześniej podejrzanych lub znane toobe naruszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="096f1-317">However, it excludes **Low** and **Medium** users flagged for risk from hello policy, which may not secure identities or devices that were previously suspected or known toobe compromised.</span></span>

<span data-ttu-id="096f1-318">Gdy ustawienie hello zasad,</span><span class="sxs-lookup"><span data-stu-id="096f1-318">When setting hello policy,</span></span>

* <span data-ttu-id="096f1-319">Wyklucz użytkowników, którzy są prawdopodobnie toogenerate wiele alarmów false (deweloperów, analityków zabezpieczeń)</span><span class="sxs-lookup"><span data-stu-id="096f1-319">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="096f1-320">Wyklucz użytkowników, których Włączanie hello zasad nie jest praktyczne ustawień regionalnych (na przykład nie toohelpdesk dostępu)</span><span class="sxs-lookup"><span data-stu-id="096f1-320">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="096f1-321">Użyj **wysokiej** próg podczas początkowej zasad zbiorczego, lub jeśli należy zminimalizować problemy, które zostały odebrane przez użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="096f1-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="096f1-322">Użyj **małej** progu, jeśli organizacja wymaga wyższego poziomu bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="096f1-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="096f1-323">Wybieranie **małej** próg wprowadzono dodatkowe użytkownika logowania wyzwania, ale zwiększyć bezpieczeństwo.</span><span class="sxs-lookup"><span data-stu-id="096f1-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="096f1-324">Hello zalecane domyślne dla większości organizacji jest tooconfigure regułę **średni** toostrike próg kompromis między użyteczność i zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="096f1-324">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="096f1-325">Omówienie hello dotyczące środowiska użytkownika, zobacz:</span><span class="sxs-lookup"><span data-stu-id="096f1-325">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="096f1-326">[Złamania zabezpieczeń konta przepływu odzyskiwania](active-directory-identityprotection-flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="096f1-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="096f1-327">[Naruszone zablokowano konto przepływu](active-directory-identityprotection-flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="096f1-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="096f1-328">**okno dialogowe konfiguracji pokrewne hello tooopen**:</span><span class="sxs-lookup"><span data-stu-id="096f1-328">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="096f1-329">Na powitania **Azure AD Identity Protection** bloku w hello **Konfiguruj** kliknij **zasad ryzyka użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="096f1-329">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="096f1-330">![Zasady użytkownika ridk](./media/active-directory-identityprotection/1009.png "zasady ridk użytkownika")</span><span class="sxs-lookup"><span data-stu-id="096f1-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="096f1-331">Zmniejszenia zdarzenia o podwyższonym ryzyku użytkownika</span><span class="sxs-lookup"><span data-stu-id="096f1-331">Mitigating user risk events</span></span>
<span data-ttu-id="096f1-332">Administratorzy mogą ustawić użytkowników tooblock zasad zabezpieczeń ryzyka użytkownika podczas logowania, w zależności od poziomu zagrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="096f1-332">Administrators can set a user risk security policy tooblock users upon sign-in depending on hello risk level.</span></span>

<span data-ttu-id="096f1-333">Blokowanie logowania:</span><span class="sxs-lookup"><span data-stu-id="096f1-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="096f1-334">Uniemożliwia hello wygenerowanie nowego zdarzenia ryzyka użytkownika dla użytkownika hello, których to dotyczy</span><span class="sxs-lookup"><span data-stu-id="096f1-334">Prevents hello generation of new user risk events for hello affected user</span></span>
* <span data-ttu-id="096f1-335">Umożliwia administratorom toomanually Skoryguj hello ryzyka zdarzenia mające wpływ na tożsamości użytkownika hello i przywrócić stan bezpiecznego tooa</span><span class="sxs-lookup"><span data-stu-id="096f1-335">Enables administrators toomanually remediate hello risk events affecting hello user's identity and restore it tooa secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="096f1-336">Zasady rejestracji usługi Multi-Factor authentication</span><span class="sxs-lookup"><span data-stu-id="096f1-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="096f1-337">Uwierzytelnianie wieloskładnikowe platformy Azure jest to metoda weryfikacji tożsamości, która wymaga stosowania hello więcej niż tylko nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="096f1-337">Azure multi-factor authentication is a method of verifying who you are that requires hello use of more than just a username and password.</span></span> <span data-ttu-id="096f1-338">Zapewnia drugą warstwę logowania toouser zabezpieczeń i transakcji.</span><span class="sxs-lookup"><span data-stu-id="096f1-338">It provides a second layer of security toouser sign-ins and transactions.</span></span>  
<span data-ttu-id="096f1-339">Firma Microsoft zaleca wymagane uwierzytelnianie wieloskładnikowe platformy Azure logowania użytkownika, ponieważ jego:</span><span class="sxs-lookup"><span data-stu-id="096f1-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="096f1-340">Zapewnia silne uwierzytelnianie za pomocą różnych opcji weryfikacji łatwe</span><span class="sxs-lookup"><span data-stu-id="096f1-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="096f1-341">Odgrywa kluczową rolę w celu przygotowania tooprotect Twojej organizacji i odzyskanie dokonywania konta</span><span class="sxs-lookup"><span data-stu-id="096f1-341">Plays a key role in preparing your organization tooprotect and recover from account compromises</span></span>

<span data-ttu-id="096f1-342">![Zasady użytkownika ridk](./media/active-directory-identityprotection/1019.png "zasady ridk użytkownika")</span><span class="sxs-lookup"><span data-stu-id="096f1-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="096f1-343">Aby uzyskać więcej informacji, zobacz [co to jest uwierzytelnianie wieloskładnikowe Azure?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="096f1-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="096f1-344">Azure AD Identity Protection pomaga w zarządzaniu wdrożenie hello rejestracji usługi Multi-Factor authentication przez skonfigurowanie zasad, które umożliwia:</span><span class="sxs-lookup"><span data-stu-id="096f1-344">Azure AD Identity Protection helps you manage hello roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="096f1-345">Ustaw hello użytkowników i grup hello zasady ma zastosowanie do:</span><span class="sxs-lookup"><span data-stu-id="096f1-345">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="096f1-346">![Zasady MFA](./media/active-directory-identityprotection/1020.png "zasad MFA")</span><span class="sxs-lookup"><span data-stu-id="096f1-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="096f1-347">Toobe formanty hello zestaw wymuszane w przypadku zasad hello wyzwala::</span><span class="sxs-lookup"><span data-stu-id="096f1-347">Set hello controls toobe enforced when hello policy triggers::</span></span>  

    <span data-ttu-id="096f1-348">![Zasady MFA](./media/active-directory-identityprotection/1021.png "zasad MFA")</span><span class="sxs-lookup"><span data-stu-id="096f1-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="096f1-349">Przełącz stan hello zasad:</span><span class="sxs-lookup"><span data-stu-id="096f1-349">Switch hello state of your policy:</span></span>

    <span data-ttu-id="096f1-350">![Zasady MFA](./media/active-directory-identityprotection/403.png "zasad MFA")</span><span class="sxs-lookup"><span data-stu-id="096f1-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="096f1-351">Wyświetl bieżący stan rejestracji hello:</span><span class="sxs-lookup"><span data-stu-id="096f1-351">View hello current registration status:</span></span>

    <span data-ttu-id="096f1-352">![Zasady MFA](./media/active-directory-identityprotection/1022.png "zasad MFA")</span><span class="sxs-lookup"><span data-stu-id="096f1-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="096f1-353">Omówienie hello dotyczące środowiska użytkownika, zobacz:</span><span class="sxs-lookup"><span data-stu-id="096f1-353">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="096f1-354">[Uwierzytelnianie wieloskładnikowe rejestracji przepływu](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="096f1-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="096f1-355">[Logowanie napotyka przy użyciu usługi Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span><span class="sxs-lookup"><span data-stu-id="096f1-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="096f1-356">**okno dialogowe konfiguracji pokrewne hello tooopen**:</span><span class="sxs-lookup"><span data-stu-id="096f1-356">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="096f1-357">Na powitania **Azure AD Identity Protection** bloku w hello **Konfiguruj** kliknij **rejestracji usługi Multi-Factor authentication**.</span><span class="sxs-lookup"><span data-stu-id="096f1-357">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="096f1-358">![Zasady MFA](./media/active-directory-identityprotection/1019.png "zasad MFA")</span><span class="sxs-lookup"><span data-stu-id="096f1-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="096f1-359">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="096f1-359">Next steps</span></span>
* [<span data-ttu-id="096f1-360">Kanał 9: Usługi Azure AD i Pokaż tożsamości: Podgląd ochrony tożsamości</span><span class="sxs-lookup"><span data-stu-id="096f1-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="096f1-361">Włączenie ochrony tożsamości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="096f1-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="096f1-362">Luk w zabezpieczeniach wykrywanych przez usługę Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="096f1-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="096f1-363">Zdarzenia o podwyższonym ryzyku Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="096f1-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="096f1-364">Azure Active Directory Identity Protection powiadomienia</span><span class="sxs-lookup"><span data-stu-id="096f1-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="096f1-365">Azure podręcznikowym ochronę tożsamości w usłudze Active Directory</span><span class="sxs-lookup"><span data-stu-id="096f1-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="096f1-366">Azure Active Directory Identity Protection słownik</span><span class="sxs-lookup"><span data-stu-id="096f1-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="096f1-367">Logowanie, korzystając z usługi Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="096f1-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="096f1-368">Azure Active Directory Identity Protection — jak toounblock użytkowników</span><span class="sxs-lookup"><span data-stu-id="096f1-368">Azure Active Directory Identity Protection - How toounblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="096f1-369">Wprowadzenie do usługi Azure Active Directory Identity Protection oraz Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="096f1-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
