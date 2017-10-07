---
title: "aaaAzure słownik ochrony tożsamości w usłudze Active Directory | Dokumentacja firmy Microsoft"
description: "Słownik ochrony tożsamości usługi Azure Active Directory"
services: active-directory
keywords: "ochronę tożsamości usługi Azure active directory, usługa cloud app discovery, zarządzanie aplikacjami, zabezpieczeń, ryzyka, poziom ryzyka, luki w zabezpieczeniach, zasady zabezpieczeń, słownik"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 833119a5-33d6-4482-adda-fa35218c72c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ff2e96d20e2a3f1df24b78e66be5a0c6807e60a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a><span data-ttu-id="e1a56-104">Słownik ochrony tożsamości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1a56-104">Azure Active Directory Identity Protection Glossary</span></span>
### <a name="at-risk-user"></a><span data-ttu-id="e1a56-105">Zagrożone (użytkownika)</span><span class="sxs-lookup"><span data-stu-id="e1a56-105">At risk (User)</span></span>
<span data-ttu-id="e1a56-106">Użytkownik z jednego lub wielu zdarzeń active ryzyka.</span><span class="sxs-lookup"><span data-stu-id="e1a56-106">A user with one or more active risk events.</span></span> 

### <a name="atypical-sign-in-location"></a><span data-ttu-id="e1a56-107">Nietypowe logowania w lokalizacji</span><span class="sxs-lookup"><span data-stu-id="e1a56-107">Atypical sign-in location</span></span>
<span data-ttu-id="e1a56-108">Logowania z lokalizacji geograficznej, które nie są typowe dla określonego użytkownika hello, podobne użytkowników lub hello dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="e1a56-108">A sign-in from a geographic location that is not typical for hello specific user, similar users, or hello tenant.</span></span>

### <a name="azure-ad-identity-protection"></a><span data-ttu-id="e1a56-109">Usługa Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e1a56-109">Azure AD Identity Protection</span></span>
<span data-ttu-id="e1a56-110">Moduł zabezpieczeń usługi Azure Active Directory, która udostępnia skonsolidowany wgląd w zdarzenia o podwyższonym ryzyku i potencjalnych luk w zabezpieczeniach wpływających na tożsamości organizacji.</span><span class="sxs-lookup"><span data-stu-id="e1a56-110">A security module of Azure Active Directory that provides a consolidated view into risk events and potential vulnerabilities affecting an organization’s identities.</span></span>

### <a name="conditional-access"></a><span data-ttu-id="e1a56-111">Dostęp warunkowy</span><span class="sxs-lookup"><span data-stu-id="e1a56-111">Conditional access</span></span>
<span data-ttu-id="e1a56-112">Zasady dotyczące zabezpieczania tooresources dostępu.</span><span class="sxs-lookup"><span data-stu-id="e1a56-112">A policy for securing access tooresources.</span></span> <span data-ttu-id="e1a56-113">Zasady dostępu warunkowego są przechowywane w hello Azure Active Directory i są oceniane przez usługę Azure AD przed udzieleniem im dostępu do zasobów toohello.</span><span class="sxs-lookup"><span data-stu-id="e1a56-113">Conditional access rules are stored in hello Azure Active Directory and are evaluated by Azure AD before granting access toohello resource.</span></span>  <span data-ttu-id="e1a56-114">Przykład reguły obejmują, ograniczanie dostępu na podstawie lokalizacji użytkownika metodę uwierzytelniania użytkownika lub kondycji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e1a56-114">Example rules include restricting access based on user location, device health or user authentication method.</span></span>

### <a name="credentials"></a><span data-ttu-id="e1a56-115">Poświadczenia</span><span class="sxs-lookup"><span data-stu-id="e1a56-115">Credentials</span></span>
<span data-ttu-id="e1a56-116">Informacje, która zawiera identyfikator i potwierdzenie identyfikatora, który jest używany toogain dostępu toolocal i zasobów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="e1a56-116">Information that includes identification and proof of identification that is used toogain access toolocal and network resources.</span></span> <span data-ttu-id="e1a56-117">Przykładami poświadczeń są nazwy użytkownika i hasła, karty inteligentne i certyfikaty.</span><span class="sxs-lookup"><span data-stu-id="e1a56-117">Examples of credentials are user names and passwords, smart cards, and certificates.</span></span>

### <a name="event"></a><span data-ttu-id="e1a56-118">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="e1a56-118">Event</span></span>
<span data-ttu-id="e1a56-119">Rekord działania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e1a56-119">A record of an activity in Azure Active Directory.</span></span>

### <a name="false-positive-risk-event"></a><span data-ttu-id="e1a56-120">Fałszywie dodatnich (ryzyka zdarzenie)</span><span class="sxs-lookup"><span data-stu-id="e1a56-120">False-positive (risk event)</span></span>
<span data-ttu-id="e1a56-121">Stan zdarzenia ryzyka ustawionych ręcznie przez użytkownika ochronę tożsamości, wskazującą zdarzenie ryzyka hello została zbadana i został niepoprawnie oznaczone jako zdarzenie ryzyka.</span><span class="sxs-lookup"><span data-stu-id="e1a56-121">A risk event status set manually by an Identity Protection user, indicating that hello risk event was investigated and was incorrectly flagged as a risk event.</span></span>

### <a name="identity"></a><span data-ttu-id="e1a56-122">Tożsamość</span><span class="sxs-lookup"><span data-stu-id="e1a56-122">Identity</span></span>
<span data-ttu-id="e1a56-123">Osoba lub podmiot, należy sprawdzić za pomocą uwierzytelniania na podstawie kryteriów, takie jak hasła lub certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e1a56-123">A person or entity that must be verified by means of authentication, based on criteria such as password or a certificate.</span></span>

### <a name="identity-risk-event"></a><span data-ttu-id="e1a56-124">Zdarzenie ryzyka tożsamości</span><span class="sxs-lookup"><span data-stu-id="e1a56-124">Identity risk event</span></span>
<span data-ttu-id="e1a56-125">Zdarzenie usługi AAD został oznaczony jako nietypowych przez ochronę tożsamości, która może wskazywać, że naruszono tożsamości.</span><span class="sxs-lookup"><span data-stu-id="e1a56-125">AAD event that was flagged as anomalous by Identity Protection, and may indicate that an identity has been compromised.</span></span>

### <a name="ignored-risk-event"></a><span data-ttu-id="e1a56-126">Ignorowane (ryzyka zdarzenie)</span><span class="sxs-lookup"><span data-stu-id="e1a56-126">Ignored (risk event)</span></span>
<span data-ttu-id="e1a56-127">Stan zdarzenia ryzyka ustawionych ręcznie przez użytkownika ochronę tożsamości, wskazujący, że zdarzenie ryzyka hello jest zamknięty bez podejmowania działań korygujących.</span><span class="sxs-lookup"><span data-stu-id="e1a56-127">A risk event status set manually by an Identity Protection user, indicating that hello risk event is closed without taking a remediation action.</span></span>

### <a name="impossible-travel-from-atypical-locations"></a><span data-ttu-id="e1a56-128">Niemożliwa podróż z nietypowych lokalizacji</span><span class="sxs-lookup"><span data-stu-id="e1a56-128">Impossible travel from atypical locations</span></span>
<span data-ttu-id="e1a56-129">To zdarzenie ryzyka wyzwalane, gdy dwa logowania dla hello tego samego użytkownika zostaną wykryte, gdy co najmniej jeden z nich jest z nietypowych lokalizacji logowania, a w przypadku, gdy hello czas między logowania hello jest krótszy niż minimalny hello czasu zajmie toophysically przesyłane między tymi lokalizacje.</span><span class="sxs-lookup"><span data-stu-id="e1a56-129">A risk event triggered when two sign-ins for hello same user are detected, where at least one of them is from an atypical sign-in location, and where hello time between hello sign-ins is shorter than hello minimum time it would take toophysically travel between these locations.</span></span>  

### <a name="investigation"></a><span data-ttu-id="e1a56-130">Badanie</span><span class="sxs-lookup"><span data-stu-id="e1a56-130">Investigation</span></span>
<span data-ttu-id="e1a56-131">Witaj proces oceny hello działań, dzienniki i inne istotne informacje związane z tooa ryzyka zdarzeń toodecide czy korygowania lub migracji kroki są niezbędne, zrozumieć czy i jak tożsamość hello zostało naruszone i wiedzieć, jak hello. użyto tożsamości ze złamanymi zabezpieczeniami.</span><span class="sxs-lookup"><span data-stu-id="e1a56-131">hello process of reviewing hello activities, logs, and other relevant information related tooa risk event toodecide whether remediation or mitigation steps are necessary, understand if and how hello identity was compromised, and understand how hello compromised identity was used.</span></span>

### <a name="leaked-credentials"></a><span data-ttu-id="e1a56-132">Ujawnione poświadczenia</span><span class="sxs-lookup"><span data-stu-id="e1a56-132">Leaked credentials</span></span>
<span data-ttu-id="e1a56-133">To zdarzenie ryzyka wyzwalane, gdy znajdują się bieżące poświadczenia użytkownika (nazwy użytkownika i hasło) publikowane publicznie hello ciemny sieci web przez naszych pracowników naukowo-badawczych.</span><span class="sxs-lookup"><span data-stu-id="e1a56-133">A risk event triggered when current user credentials (user name and password) are found posted publicly in hello Dark   web by our researchers.</span></span>

### <a name="mitigation"></a><span data-ttu-id="e1a56-134">Środki zaradcze</span><span class="sxs-lookup"><span data-stu-id="e1a56-134">Mitigation</span></span>
<span data-ttu-id="e1a56-135">Toolimit akcji lub wyeliminowanie możliwości hello tooexploit atakująca złamany tożsamości lub urządzenia bez przywracania hello tożsamości lub urządzenie tooa bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="e1a56-135">An action toolimit or eliminate hello ability of an attacker tooexploit a compromised identity or device without restoring hello identity or device tooa safe state.</span></span> <span data-ttu-id="e1a56-136">Środki zaradcze nie można rozpoznać poprzednie zdarzenia ryzyko związane z tożsamości hello lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e1a56-136">A mitigation does not resolve previous risk events associated with hello identity or device.</span></span>

### <a name="multi-factor-authentication"></a><span data-ttu-id="e1a56-137">Uwierzytelnianie wieloskładnikowe</span><span class="sxs-lookup"><span data-stu-id="e1a56-137">Multi-factor authentication</span></span>
<span data-ttu-id="e1a56-138">Metoda uwierzytelniania, która wymaga dwóch lub więcej metod uwierzytelniania, które mogą obejmować coś, co użytkownik hello ma taki certyfikat; coś zna hello użytkownika, takie jak nazwy użytkowników, hasła lub wyrażenia przebiegu; Atrybuty fizyczne, takie jak odcisk palca; i atrybuty osobistych, takich jak osobiste podpisu.</span><span class="sxs-lookup"><span data-stu-id="e1a56-138">An authentication method that requires two or more authentication methods, which may include something hello user has, such a certificate; something hello user knows, such as user names, passwords, or pass phrases; physical attributes, such as a thumbprint; and personal attributes, such as a personal signature.</span></span>

### <a name="offline-detection"></a><span data-ttu-id="e1a56-139">Wykrywanie w trybie offline</span><span class="sxs-lookup"><span data-stu-id="e1a56-139">Offline detection</span></span>
<span data-ttu-id="e1a56-140">Witaj wykrywanie anomalii i oceny ryzyka hello zdarzenia, takie jak próba logowania po fakcie hello na zdarzenie, która została już wykonana.</span><span class="sxs-lookup"><span data-stu-id="e1a56-140">hello detection of anomalies and evaluation of hello risk of an event such as sign-in attempt after hello fact, for an event that has already happened.</span></span>

### <a name="policy-condition"></a><span data-ttu-id="e1a56-141">Stan zasad</span><span class="sxs-lookup"><span data-stu-id="e1a56-141">Policy condition</span></span>
<span data-ttu-id="e1a56-142">Część zasad zabezpieczeń, który definiuje hello jednostek (grup, użytkownicy, aplikacje, platformy urządzeń, Stany urządzeń, zakresy adresów IP, typy klientów) zawartych w zasadach hello lub wykluczone z niego.</span><span class="sxs-lookup"><span data-stu-id="e1a56-142">A part of a security policy which defines hello entities (groups, users, apps, device platforms, Device states, IP ranges, client types) included in hello policy or excluded from it.</span></span>

### <a name="policy-rule"></a><span data-ttu-id="e1a56-143">Reguła zasad</span><span class="sxs-lookup"><span data-stu-id="e1a56-143">Policy rule</span></span>
<span data-ttu-id="e1a56-144">część Hello zasady zabezpieczeń, które opisano hello okoliczności, które spowoduje wywołanie hello zasad i hello akcje podjęte po wyzwoleniu hello zasad.</span><span class="sxs-lookup"><span data-stu-id="e1a56-144">hello part of a security policy which describes hello circumstances that would trigger hello policy, and hello actions taken when hello policy is triggered.</span></span>

### <a name="prevention"></a><span data-ttu-id="e1a56-145">Zapobieganie</span><span class="sxs-lookup"><span data-stu-id="e1a56-145">Prevention</span></span>
<span data-ttu-id="e1a56-146">Akcja tooprevent uszkodzenia toohello organizacji za pośrednictwem nadużycia tożsamości lub urządzenia podejrzanych lub znać toobe naruszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e1a56-146">An action tooprevent damage toohello organization through abuse of an identity or device suspected or know toobe compromised.</span></span> <span data-ttu-id="e1a56-147">Akcji związanych z zapobieganiem nie zabezpieczyć urządzenia hello lub tożsamości, a nie rozwiązuje poprzednie zdarzenia ryzyka.</span><span class="sxs-lookup"><span data-stu-id="e1a56-147">A prevention action does not secure hello device or identity, and does not resolve previous risk events.</span></span>

### <a name="privileged-user"></a><span data-ttu-id="e1a56-148">Uprzywilejowane (użytkownika)</span><span class="sxs-lookup"><span data-stu-id="e1a56-148">Privileged (user)</span></span>
<span data-ttu-id="e1a56-149">Użytkownik, który w czasie hello zdarzenia ryzyka, ma tooone uprawnienia administratora stałych lub tymczasowych lub więcej zasobów w usłudze Active Directory, takie jak Administrator globalny, Administrator rozliczeń, Administrator usługi, administrator użytkownika i hasło Administrator.</span><span class="sxs-lookup"><span data-stu-id="e1a56-149">A user that at hello time of a risk event, had permanent or temporary admin permissions tooone or more resource in Azure Active Directory, such as a Global Administrator, Billing Administrator, Service Administrator, User administrator, and Password Administrator.</span></span> 

### <a name="real-time"></a><span data-ttu-id="e1a56-150">W czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="e1a56-150">Real-time</span></span>
<span data-ttu-id="e1a56-151">Zobacz wykrywanie w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="e1a56-151">See Real-time detection.</span></span>

### <a name="real-time-detection"></a><span data-ttu-id="e1a56-152">Wykrywanie w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="e1a56-152">Real-time detection</span></span>
<span data-ttu-id="e1a56-153">Witaj wykrywanie anomalii i oceny ryzyka hello zdarzenia, takie jak prób logowania przed zdarzeniem hello jest dozwolone tooproceed.</span><span class="sxs-lookup"><span data-stu-id="e1a56-153">hello detection of anomalies and evaluation of hello risk of an event such as sign-in attempt before hello event is allowed tooproceed.</span></span>

### <a name="remediated-risk-event"></a><span data-ttu-id="e1a56-154">Skorygowane (ryzyka zdarzenie)</span><span class="sxs-lookup"><span data-stu-id="e1a56-154">Remediated (risk event)</span></span>
<span data-ttu-id="e1a56-155">Stan zdarzenia ryzyka ustawione automatycznie ochrony tożsamości i wskazujący, że zdarzenie ryzyka hello korygowania przy użyciu akcji korygowania standardowe powitania dla tego typu zdarzenia ryzyka.</span><span class="sxs-lookup"><span data-stu-id="e1a56-155">A risk event status set automatically by Identity Protection, indicating that hello risk event was remediated using hello standard remediation action for this type of risk event.</span></span> <span data-ttu-id="e1a56-156">Na przykład po zresetowaniu hasła użytkownika hello wiele zdarzeń ryzyka, wskazujące, że zostało naruszone hasło poprzedniej hello są rozwiązywane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="e1a56-156">For example, when hello user password is reset, many risk events that indicate that hello previous password was compromised are automatically remediated.</span></span>

### <a name="remediation"></a><span data-ttu-id="e1a56-157">Korygowania</span><span class="sxs-lookup"><span data-stu-id="e1a56-157">Remediation</span></span>
<span data-ttu-id="e1a56-158">Akcja toosecure tożsamości lub urządzeń, które zostały wcześniej podejrzanych lub znane toobe naruszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e1a56-158">An action toosecure an identity or a device that were previously suspected or known toobe compromised.</span></span> <span data-ttu-id="e1a56-159">Akcja korygowania przywraca hello tożsamości lub urządzenie tooa bezpieczne i usuwa poprzednie zdarzenia ryzyko związane z tożsamości hello lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e1a56-159">A remediation action restores hello identity or device tooa safe state, and resolves previous risk events associated with hello identity or device.</span></span>

### <a name="resolved-risk-event"></a><span data-ttu-id="e1a56-160">Rozwiązany (ryzyka zdarzenie)</span><span class="sxs-lookup"><span data-stu-id="e1a56-160">Resolved (risk event)</span></span>
<span data-ttu-id="e1a56-161">Stan zdarzenia czynnika ryzyka ustawionych ręcznie przez użytkownika ochronę tożsamości, informujący, że użytkownik hello przejął akcji korygowania odpowiednie poza Identity Protection i zdarzenia ryzyka hello należy traktować jako zamknięte.</span><span class="sxs-lookup"><span data-stu-id="e1a56-161">A risk event status set manually by an Identity Protection user, indicating that hello user took an appropriate remediation action outside Identity Protection, and that hello risk event should be considered closed.</span></span>

### <a name="risk-event-status"></a><span data-ttu-id="e1a56-162">Stan zdarzenia ryzyka</span><span class="sxs-lookup"><span data-stu-id="e1a56-162">Risk event status</span></span>
<span data-ttu-id="e1a56-163">Właściwości zdarzenia ryzyka, wskazującą, czy zdarzenia hello jest aktywna oraz czy zamknięte, przyczynę hello jej zamknięcia.</span><span class="sxs-lookup"><span data-stu-id="e1a56-163">A property of a risk event, indicating whether hello event is active, and if closed, hello reason for closing it.</span></span>

### <a name="risk-event-type"></a><span data-ttu-id="e1a56-164">Typ zdarzenia ryzyka</span><span class="sxs-lookup"><span data-stu-id="e1a56-164">Risk event type</span></span>
<span data-ttu-id="e1a56-165">Kategorię hello ryzyko zdarzeń i wskazujący typ hello anomalii powodujący toobe zdarzeń hello uważane za ryzykowne.</span><span class="sxs-lookup"><span data-stu-id="e1a56-165">A category for hello risk event, indicating hello type of anomaly that caused hello event toobe considered risky.</span></span>

### <a name="risk-level-risk-event"></a><span data-ttu-id="e1a56-166">Poziom ryzyka (ryzyka zdarzenie)</span><span class="sxs-lookup"><span data-stu-id="e1a56-166">Risk level (risk event)</span></span>
<span data-ttu-id="e1a56-167">Wskazanie (wysoki, średni lub niski) ważność hello hello ryzyka zdarzeń toohelp ochronę tożsamości użytkowników priorytetów działań hello podejmują tooreduce hello ryzyka tootheir organizacji.</span><span class="sxs-lookup"><span data-stu-id="e1a56-167">An indication (High, Medium, or Low) of hello severity of hello risk event toohelp Identity Protection users prioritize hello actions they take tooreduce hello risk tootheir organization.</span></span> 

### <a name="risk-level-sign-in"></a><span data-ttu-id="e1a56-168">Poziom ryzyka (logowanie)</span><span class="sxs-lookup"><span data-stu-id="e1a56-168">Risk level (sign-in)</span></span>
<span data-ttu-id="e1a56-169">Wskazanie (wysoki, średni lub niski) prawdopodobieństwo hello czy dla określonego logowania, próbuje ktoś toouse hello tożsamości użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e1a56-169">An indication (High, Medium, or Low) of hello likelihood that for a specific sign-in, someone else is attempting toouse hello user’s identity.</span></span>

### <a name="risk-level-user-compromise"></a><span data-ttu-id="e1a56-170">Poziom ryzyka (naruszenia zabezpieczeń użytkownika)</span><span class="sxs-lookup"><span data-stu-id="e1a56-170">Risk level (user compromise)</span></span>
<span data-ttu-id="e1a56-171">Wskazanie (wysoki, średni lub niski) hello prawdopodobieństwo, że naruszono tożsamości.</span><span class="sxs-lookup"><span data-stu-id="e1a56-171">An indication (High, Medium, or Low) of hello likelihood that an identity has been compromised.</span></span>

### <a name="risk-level-vulnerability"></a><span data-ttu-id="e1a56-172">Poziom ryzyka (luki w zabezpieczeniach)</span><span class="sxs-lookup"><span data-stu-id="e1a56-172">Risk level (vulnerability)</span></span>
<span data-ttu-id="e1a56-173">Wskazanie (wysoki, średni lub niski) ważność hello hello luki w zabezpieczeniach toohelp ochronę tożsamości użytkowników priorytetów działań hello podejmują tooreduce hello ryzyka tootheir organizacji.</span><span class="sxs-lookup"><span data-stu-id="e1a56-173">An indication (High, Medium, or Low) of hello severity of hello vulnerability toohelp Identity Protection users prioritize hello actions they take tooreduce hello risk tootheir organization.</span></span>

### <a name="secure-identity"></a><span data-ttu-id="e1a56-174">Secure (tożsamości)</span><span class="sxs-lookup"><span data-stu-id="e1a56-174">Secure (identity)</span></span>
<span data-ttu-id="e1a56-175">Podjąć akcję naprawczą, takie jak zmiany hasła lub ponownej instalacji systemu toorestore stanu tooan, który nie został naruszony potencjalnie złamany tożsamości komputera.</span><span class="sxs-lookup"><span data-stu-id="e1a56-175">Take remediation action such as a password change or machine reimaging toorestore a potentially compromised identity tooan uncompromised state.</span></span>

### <a name="security-policy"></a><span data-ttu-id="e1a56-176">Zasady zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="e1a56-176">Security policy</span></span>
<span data-ttu-id="e1a56-177">Kolekcja reguł zasad i warunek.</span><span class="sxs-lookup"><span data-stu-id="e1a56-177">A collection of policy rules and condition.</span></span> <span data-ttu-id="e1a56-178">Zasady mogą być zastosowane tooentities, takich jak użytkownicy, grupy aplikacji, urządzeń, platformy urządzeń, Stany urządzeń, zakresy adresów IP i Auth2.0 typy klientów.</span><span class="sxs-lookup"><span data-stu-id="e1a56-178">A policy can be applied tooentities such as users, groups, apps, devices, device platforms, device states, IP ranges, and Auth2.0 client types.</span></span> <span data-ttu-id="e1a56-179">Gdy jest włączona, zostanie ona potraktowana zawsze, gdy jednostka uwzględniony w zasadach hello jest wystawiony token dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="e1a56-179">When a policy is enabled, it is evaluated whenever an entity included in hello policy is issued a token for a resource.</span></span>

### <a name="sign-in-v"></a><span data-ttu-id="e1a56-180">Zaloguj się (v)</span><span class="sxs-lookup"><span data-stu-id="e1a56-180">Sign in (v)</span></span>
<span data-ttu-id="e1a56-181">tooauthenticate tooan tożsamość w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e1a56-181">tooauthenticate tooan identity in Azure Active Directory.</span></span>

### <a name="sign-in-n"></a><span data-ttu-id="e1a56-182">Logowania (n)</span><span class="sxs-lookup"><span data-stu-id="e1a56-182">Sign-in (n)</span></span>
<span data-ttu-id="e1a56-183">proces Hello lub akcji uwierzytelniania tożsamości w usłudze Azure Active Directory i hello zdarzeń, który przechwytuje tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e1a56-183">hello process or action of authenticating an identity in Azure Active Directory, and hello event that captures this operation.</span></span>

### <a name="sign-in-from-anonymous-ip-address"></a><span data-ttu-id="e1a56-184">Logowania z anonimowych adresów IP</span><span class="sxs-lookup"><span data-stu-id="e1a56-184">Sign-in from anonymous IP address</span></span>
<span data-ttu-id="e1a56-185">Zdarzenie ryzyka wyzwalane po pomyślnym zalogowaniu z adresu IP, który został zidentyfikowany jako adres IP anonimowy serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="e1a56-185">A risk event triggered after a successful sign-in from IP address that has been identified as an anonymous proxy IP address.</span></span>

### <a name="sign-in-from-infected-device"></a><span data-ttu-id="e1a56-186">Logowania z zainfekowanych urządzeń</span><span class="sxs-lookup"><span data-stu-id="e1a56-186">Sign-in from infected device</span></span>
<span data-ttu-id="e1a56-187">Wyzwalane, gdy logowania pochodzi z adresu IP, w których jest używany przez co najmniej jedno urządzenie ze złamanymi zabezpieczeniami, które próbujesz aktywnie toocommunicate z serwerem botów toobe zdarzenie ryzyka.</span><span class="sxs-lookup"><span data-stu-id="e1a56-187">A risk event triggered when a sign-in originates from an IP address which is known toobe used by one or more compromised devices, which are actively attempting toocommunicate with a bot server.</span></span>

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a><span data-ttu-id="e1a56-188">Logowania z adresów IP związanych z podejrzanymi działaniami</span><span class="sxs-lookup"><span data-stu-id="e1a56-188">Sign-in from IP address with suspicious activity</span></span>
<span data-ttu-id="e1a56-189">Zdarzenie ryzyka wyzwalane po pomyślnym logowanie z adresu IP adresów z dużej liczby nieudanych prób logowania na wielu kontach użytkowników w krótkim przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="e1a56-189">A risk event triggered after a successful sign-in from an IP address with a high number of failed login attempts across multiple user accounts over a short period of time.</span></span>

### <a name="sign-in-from-unfamiliar-location"></a><span data-ttu-id="e1a56-190">Logowania z nieznanych lokalizacji</span><span class="sxs-lookup"><span data-stu-id="e1a56-190">Sign-in from unfamiliar location</span></span>
<span data-ttu-id="e1a56-191">Zdarzenie ryzyka, wyzwalane, gdy użytkownik pomyślnie loguje się z nowej lokalizacji (adresu IP, szerokości geograficznej/długości i ASN).</span><span class="sxs-lookup"><span data-stu-id="e1a56-191">A risk event triggered when a user successfully signs in from a new location (IP, Latitude/Longitude and ASN).</span></span>

### <a name="sign-in-risk"></a><span data-ttu-id="e1a56-192">Ryzyko logowania</span><span class="sxs-lookup"><span data-stu-id="e1a56-192">Sign-in risk</span></span>
<span data-ttu-id="e1a56-193">Zobacz ryzyka poziom (logowanie)</span><span class="sxs-lookup"><span data-stu-id="e1a56-193">See Risk level (sign-in)</span></span>

### <a name="sign-in-risk-policy"></a><span data-ttu-id="e1a56-194">Zasady logowania ryzyka</span><span class="sxs-lookup"><span data-stu-id="e1a56-194">Sign-in risk policy</span></span>
<span data-ttu-id="e1a56-195">Zasady dostępu warunkowego, która ocenia hello ryzyka tooa określonych logowania i stosuje środki zaradcze, na podstawie wstępnie zdefiniowane warunki i zasady.</span><span class="sxs-lookup"><span data-stu-id="e1a56-195">A conditional access policy that evaluates hello risk tooa specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="user-compromise-risk"></a><span data-ttu-id="e1a56-196">Ryzyko naruszenia zabezpieczeń użytkownika</span><span class="sxs-lookup"><span data-stu-id="e1a56-196">User compromise risk</span></span>
<span data-ttu-id="e1a56-197">Zobacz ryzyka poziom (naruszenia zabezpieczeń użytkownika)</span><span class="sxs-lookup"><span data-stu-id="e1a56-197">See Risk level (user compromise)</span></span>

### <a name="user-risk"></a><span data-ttu-id="e1a56-198">Ryzyko użytkownika</span><span class="sxs-lookup"><span data-stu-id="e1a56-198">User risk</span></span>
<span data-ttu-id="e1a56-199">Zobacz ryzyka poziom (naruszenia zabezpieczeń użytkownika).</span><span class="sxs-lookup"><span data-stu-id="e1a56-199">See Risk level (user compromise).</span></span>

### <a name="user-risk-policy"></a><span data-ttu-id="e1a56-200">Zasady użytkownika ryzyka</span><span class="sxs-lookup"><span data-stu-id="e1a56-200">User risk policy</span></span>
<span data-ttu-id="e1a56-201">Zasady dostępu warunkowego, która uwzględnia logowania hello i stosuje środki zaradcze, na podstawie wstępnie zdefiniowane warunki i zasady.</span><span class="sxs-lookup"><span data-stu-id="e1a56-201">A conditional access policy that considers hello sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="users-flagged-for-risk"></a><span data-ttu-id="e1a56-202">Użytkownicy oflagowani w związku z ryzykiem</span><span class="sxs-lookup"><span data-stu-id="e1a56-202">Users flagged for risk</span></span>
<span data-ttu-id="e1a56-203">Użytkownicy, którzy mają zdarzenia ryzyka, które są aktywne lub skorygowanych</span><span class="sxs-lookup"><span data-stu-id="e1a56-203">Users that have risk events which are either active or remediated</span></span>

### <a name="vulnerability"></a><span data-ttu-id="e1a56-204">Luki w zabezpieczeniach</span><span class="sxs-lookup"><span data-stu-id="e1a56-204">Vulnerability</span></span>
<span data-ttu-id="e1a56-205">Konfiguracja lub warunku w usłudze Azure Active Directory, dzięki czemu tooexploits wrażliwych katalogu hello lub zagrożenia.</span><span class="sxs-lookup"><span data-stu-id="e1a56-205">A configuration or condition in Azure Active Directory which makes hello directory susceptible tooexploits or threats.</span></span>

## <a name="see-also"></a><span data-ttu-id="e1a56-206">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="e1a56-206">See also</span></span>
* [<span data-ttu-id="e1a56-207">Ochronę tożsamości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1a56-207">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

