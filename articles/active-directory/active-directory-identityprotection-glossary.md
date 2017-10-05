---
title: "Słownik ochrony tożsamości usługi Azure Active Directory | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 2cf64925cff9a78cf83532a1cfd231f7a1d98304
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a><span data-ttu-id="3bb52-104">Słownik ochrony tożsamości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3bb52-104">Azure Active Directory Identity Protection Glossary</span></span>
### <a name="at-risk-user"></a><span data-ttu-id="3bb52-105">Zagrożone (użytkownika)</span><span class="sxs-lookup"><span data-stu-id="3bb52-105">At risk (User)</span></span>
<span data-ttu-id="3bb52-106">Użytkownik z jednego lub wielu zdarzeń active ryzyka.</span><span class="sxs-lookup"><span data-stu-id="3bb52-106">A user with one or more active risk events.</span></span> 

### <a name="atypical-sign-in-location"></a><span data-ttu-id="3bb52-107">Nietypowe logowania w lokalizacji</span><span class="sxs-lookup"><span data-stu-id="3bb52-107">Atypical sign-in location</span></span>
<span data-ttu-id="3bb52-108">Logowania z lokalizacji geograficznej, które nie są typowe dla określonego użytkownika, podobnych użytkowników lub dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="3bb52-108">A sign-in from a geographic location that is not typical for the specific user, similar users, or the tenant.</span></span>

### <a name="azure-ad-identity-protection"></a><span data-ttu-id="3bb52-109">Usługa Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3bb52-109">Azure AD Identity Protection</span></span>
<span data-ttu-id="3bb52-110">Moduł zabezpieczeń usługi Azure Active Directory, która udostępnia skonsolidowany wgląd w zdarzenia o podwyższonym ryzyku i potencjalnych luk w zabezpieczeniach wpływających na tożsamości organizacji.</span><span class="sxs-lookup"><span data-stu-id="3bb52-110">A security module of Azure Active Directory that provides a consolidated view into risk events and potential vulnerabilities affecting an organization’s identities.</span></span>

### <a name="conditional-access"></a><span data-ttu-id="3bb52-111">Dostęp warunkowy</span><span class="sxs-lookup"><span data-stu-id="3bb52-111">Conditional access</span></span>
<span data-ttu-id="3bb52-112">Zasady zabezpieczenia dostępu do zasobów.</span><span class="sxs-lookup"><span data-stu-id="3bb52-112">A policy for securing access to resources.</span></span> <span data-ttu-id="3bb52-113">Zasady dostępu warunkowego są przechowywane w usłudze Azure Active Directory i są oceniane przez usługę Azure AD przed udzieleniem im dostępu do zasobu.</span><span class="sxs-lookup"><span data-stu-id="3bb52-113">Conditional access rules are stored in the Azure Active Directory and are evaluated by Azure AD before granting access to the resource.</span></span>  <span data-ttu-id="3bb52-114">Przykład reguły obejmują, ograniczanie dostępu na podstawie lokalizacji użytkownika metodę uwierzytelniania użytkownika lub kondycji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="3bb52-114">Example rules include restricting access based on user location, device health or user authentication method.</span></span>

### <a name="credentials"></a><span data-ttu-id="3bb52-115">Poświadczenia</span><span class="sxs-lookup"><span data-stu-id="3bb52-115">Credentials</span></span>
<span data-ttu-id="3bb52-116">Informacje, która zawiera identyfikator i potwierdzenie identyfikatora, który jest używany do uzyskania dostępu do lokalnego i zasobów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="3bb52-116">Information that includes identification and proof of identification that is used to gain access to local and network resources.</span></span> <span data-ttu-id="3bb52-117">Przykładami poświadczeń są nazwy użytkownika i hasła, karty inteligentne i certyfikaty.</span><span class="sxs-lookup"><span data-stu-id="3bb52-117">Examples of credentials are user names and passwords, smart cards, and certificates.</span></span>

### <a name="event"></a><span data-ttu-id="3bb52-118">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="3bb52-118">Event</span></span>
<span data-ttu-id="3bb52-119">Rekord działania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3bb52-119">A record of an activity in Azure Active Directory.</span></span>

### <a name="false-positive-risk-event"></a><span data-ttu-id="3bb52-120">Fałszywie dodatnich (ryzyka zdarzenie)</span><span class="sxs-lookup"><span data-stu-id="3bb52-120">False-positive (risk event)</span></span>
<span data-ttu-id="3bb52-121">Stan zdarzenia ryzyka ustawionych ręcznie przez użytkownika ochronę tożsamości, informujący, że zdarzenie ryzyka została zbadana i został niepoprawnie oznaczone jako zdarzenie ryzyka.</span><span class="sxs-lookup"><span data-stu-id="3bb52-121">A risk event status set manually by an Identity Protection user, indicating that the risk event was investigated and was incorrectly flagged as a risk event.</span></span>

### <a name="identity"></a><span data-ttu-id="3bb52-122">Tożsamość</span><span class="sxs-lookup"><span data-stu-id="3bb52-122">Identity</span></span>
<span data-ttu-id="3bb52-123">Osoba lub podmiot, należy sprawdzić za pomocą uwierzytelniania na podstawie kryteriów, takie jak hasła lub certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="3bb52-123">A person or entity that must be verified by means of authentication, based on criteria such as password or a certificate.</span></span>

### <a name="identity-risk-event"></a><span data-ttu-id="3bb52-124">Zdarzenie ryzyka tożsamości</span><span class="sxs-lookup"><span data-stu-id="3bb52-124">Identity risk event</span></span>
<span data-ttu-id="3bb52-125">Zdarzenie usługi AAD został oznaczony jako nietypowych przez ochronę tożsamości, która może wskazywać, że naruszono tożsamości.</span><span class="sxs-lookup"><span data-stu-id="3bb52-125">AAD event that was flagged as anomalous by Identity Protection, and may indicate that an identity has been compromised.</span></span>

### <a name="ignored-risk-event"></a><span data-ttu-id="3bb52-126">Ignorowane (ryzyka zdarzenie)</span><span class="sxs-lookup"><span data-stu-id="3bb52-126">Ignored (risk event)</span></span>
<span data-ttu-id="3bb52-127">Stan zdarzenia ryzyka ustawionych ręcznie przez użytkownika ochronę tożsamości, wskazujący, że zdarzenia ryzyko jest zamknięte bez podejmowania działań korygujących.</span><span class="sxs-lookup"><span data-stu-id="3bb52-127">A risk event status set manually by an Identity Protection user, indicating that the risk event is closed without taking a remediation action.</span></span>

### <a name="impossible-travel-from-atypical-locations"></a><span data-ttu-id="3bb52-128">Niemożliwa podróż z nietypowych lokalizacji</span><span class="sxs-lookup"><span data-stu-id="3bb52-128">Impossible travel from atypical locations</span></span>
<span data-ttu-id="3bb52-129">Zdarzenie ryzyka, wyzwalane po wykryciu dwukrotnego zalogowania do tego samego użytkownika, gdzie jest co najmniej jeden z nich z nietypowych lokalizacji logowania, a czas między sesje logowania jest krótszy niż minimalny czas, jaki zajmuje się fizycznie przesyłane między tymi lokacjami.</span><span class="sxs-lookup"><span data-stu-id="3bb52-129">A risk event triggered when two sign-ins for the same user are detected, where at least one of them is from an atypical sign-in location, and where the time between the sign-ins is shorter than the minimum time it would take to physically travel between these locations.</span></span>  

### <a name="investigation"></a><span data-ttu-id="3bb52-130">Badanie</span><span class="sxs-lookup"><span data-stu-id="3bb52-130">Investigation</span></span>
<span data-ttu-id="3bb52-131">Proces oceny działania, dzienników i inne istotne informacje powiązane ze zdarzeniem ryzyka zdecydować, czy korygowania lub ograniczenie kroki są niezbędne, określić, czy i jak tożsamość zostało naruszone i zrozumieć korzystania ze złamanymi zabezpieczeniami tożsamości.</span><span class="sxs-lookup"><span data-stu-id="3bb52-131">The process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary, understand if and how the identity was compromised, and understand how the compromised identity was used.</span></span>

### <a name="leaked-credentials"></a><span data-ttu-id="3bb52-132">Ujawnione poświadczenia</span><span class="sxs-lookup"><span data-stu-id="3bb52-132">Leaked credentials</span></span>
<span data-ttu-id="3bb52-133">Zdarzenie ryzyka, wyzwalane, gdy bieżące poświadczenia użytkownika (nazwy użytkownika i hasło) znajdują się publicznie opublikowane w sieci web ciemny, przez naszych pracowników naukowo-badawczych.</span><span class="sxs-lookup"><span data-stu-id="3bb52-133">A risk event triggered when current user credentials (user name and password) are found posted publicly in the Dark   web by our researchers.</span></span>

### <a name="mitigation"></a><span data-ttu-id="3bb52-134">Środki zaradcze</span><span class="sxs-lookup"><span data-stu-id="3bb52-134">Mitigation</span></span>
<span data-ttu-id="3bb52-135">Akcja celu ograniczenie lub wyeliminowanie osoba atakująca możliwość wykorzystania złamany tożsamości lub urządzenia bez przywrócenia tożsamości lub urządzenie to bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="3bb52-135">An action to limit or eliminate the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="3bb52-136">Środki zaradcze nie można rozpoznać poprzednie zdarzenia ryzyko związane z tożsamości lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="3bb52-136">A mitigation does not resolve previous risk events associated with the identity or device.</span></span>

### <a name="multi-factor-authentication"></a><span data-ttu-id="3bb52-137">Uwierzytelnianie wieloskładnikowe</span><span class="sxs-lookup"><span data-stu-id="3bb52-137">Multi-factor authentication</span></span>
<span data-ttu-id="3bb52-138">Metoda uwierzytelniania, która wymaga dwóch lub więcej metod uwierzytelniania, które mogą obejmować coś użytkownik ma taki certyfikat; coś użytkownik wie, takie jak nazwy użytkowników, hasła lub wyrażenia przebiegu; Atrybuty fizyczne, takie jak odcisk palca; i atrybuty osobistych, takich jak osobiste podpisu.</span><span class="sxs-lookup"><span data-stu-id="3bb52-138">An authentication method that requires two or more authentication methods, which may include something the user has, such a certificate; something the user knows, such as user names, passwords, or pass phrases; physical attributes, such as a thumbprint; and personal attributes, such as a personal signature.</span></span>

### <a name="offline-detection"></a><span data-ttu-id="3bb52-139">Wykrywanie w trybie offline</span><span class="sxs-lookup"><span data-stu-id="3bb52-139">Offline detection</span></span>
<span data-ttu-id="3bb52-140">Wykrywanie anomalii i oceny ryzyka zdarzenia, takie jak próba logowania po fakcie, dla każdego zdarzenia, która została już wykonana.</span><span class="sxs-lookup"><span data-stu-id="3bb52-140">The detection of anomalies and evaluation of the risk of an event such as sign-in attempt after the fact, for an event that has already happened.</span></span>

### <a name="policy-condition"></a><span data-ttu-id="3bb52-141">Stan zasad</span><span class="sxs-lookup"><span data-stu-id="3bb52-141">Policy condition</span></span>
<span data-ttu-id="3bb52-142">Część zasad zabezpieczeń, który definiuje jednostek (grup, użytkownicy, aplikacje, platformy urządzeń, Stany urządzeń, zakresy adresów IP, typy klientów) uwzględnionych w zasadach lub wykluczone z niego.</span><span class="sxs-lookup"><span data-stu-id="3bb52-142">A part of a security policy which defines the entities (groups, users, apps, device platforms, Device states, IP ranges, client types) included in the policy or excluded from it.</span></span>

### <a name="policy-rule"></a><span data-ttu-id="3bb52-143">Reguła zasad</span><span class="sxs-lookup"><span data-stu-id="3bb52-143">Policy rule</span></span>
<span data-ttu-id="3bb52-144">Część zasad zabezpieczeń, który opisuje okoliczności, które spowoduje wywołanie zasad i akcje wykonywane po wyzwoleniu zasady.</span><span class="sxs-lookup"><span data-stu-id="3bb52-144">The part of a security policy which describes the circumstances that would trigger the policy, and the actions taken when the policy is triggered.</span></span>

### <a name="prevention"></a><span data-ttu-id="3bb52-145">Zapobieganie</span><span class="sxs-lookup"><span data-stu-id="3bb52-145">Prevention</span></span>
<span data-ttu-id="3bb52-146">Działania w celu zapobieżenia szkody w organizacji za pomocą nadużycia tożsamości lub urządzenia podejrzanych lub znać naruszenia.</span><span class="sxs-lookup"><span data-stu-id="3bb52-146">An action to prevent damage to the organization through abuse of an identity or device suspected or know to be compromised.</span></span> <span data-ttu-id="3bb52-147">Akcji związanych z zapobieganiem nie zabezpieczyć urządzenia lub tożsamości, a nie rozwiązuje poprzednie zdarzenia ryzyka.</span><span class="sxs-lookup"><span data-stu-id="3bb52-147">A prevention action does not secure the device or identity, and does not resolve previous risk events.</span></span>

### <a name="privileged-user"></a><span data-ttu-id="3bb52-148">Uprzywilejowane (użytkownika)</span><span class="sxs-lookup"><span data-stu-id="3bb52-148">Privileged (user)</span></span>
<span data-ttu-id="3bb52-149">Użytkownik, który w czasie zdarzenia ryzyka, ma uprawnienia administratora stałych lub tymczasowych do co najmniej jednego zasobu w usłudze Active Directory, takie jak Administrator globalny, Administrator rozliczeń, Administrator usługi, administrator użytkownika i hasło administratora.</span><span class="sxs-lookup"><span data-stu-id="3bb52-149">A user that at the time of a risk event, had permanent or temporary admin permissions to one or more resource in Azure Active Directory, such as a Global Administrator, Billing Administrator, Service Administrator, User administrator, and Password Administrator.</span></span> 

### <a name="real-time"></a><span data-ttu-id="3bb52-150">W czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="3bb52-150">Real-time</span></span>
<span data-ttu-id="3bb52-151">Zobacz wykrywanie w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="3bb52-151">See Real-time detection.</span></span>

### <a name="real-time-detection"></a><span data-ttu-id="3bb52-152">Wykrywanie w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="3bb52-152">Real-time detection</span></span>
<span data-ttu-id="3bb52-153">Wykrywanie anomalii i oceny ryzyka zdarzenia, takie jak prób logowania przed zdarzeniem można kontynuować.</span><span class="sxs-lookup"><span data-stu-id="3bb52-153">The detection of anomalies and evaluation of the risk of an event such as sign-in attempt before the event is allowed to proceed.</span></span>

### <a name="remediated-risk-event"></a><span data-ttu-id="3bb52-154">Skorygowane (ryzyka zdarzenie)</span><span class="sxs-lookup"><span data-stu-id="3bb52-154">Remediated (risk event)</span></span>
<span data-ttu-id="3bb52-155">Stan zdarzenia ryzyka ustawione automatycznie ochrony tożsamości i wskazujący, że zdarzenia ryzyka korygowania przy użyciu akcji korygowania standardowe dla tego typu zdarzenia ryzyka.</span><span class="sxs-lookup"><span data-stu-id="3bb52-155">A risk event status set automatically by Identity Protection, indicating that the risk event was remediated using the standard remediation action for this type of risk event.</span></span> <span data-ttu-id="3bb52-156">Na przykład po zresetowaniu hasła użytkownika wielu zdarzeń ryzyka, które wskazują, że zostało naruszone poprzednich haseł są rozwiązywane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="3bb52-156">For example, when the user password is reset, many risk events that indicate that the previous password was compromised are automatically remediated.</span></span>

### <a name="remediation"></a><span data-ttu-id="3bb52-157">Korygowania</span><span class="sxs-lookup"><span data-stu-id="3bb52-157">Remediation</span></span>
<span data-ttu-id="3bb52-158">Akcja do zabezpieczania tożsamości lub urządzeń, które zostały wcześniej podejrzanych lub znane naruszenia.</span><span class="sxs-lookup"><span data-stu-id="3bb52-158">An action to secure an identity or a device that were previously suspected or known to be compromised.</span></span> <span data-ttu-id="3bb52-159">Akcja korygowania przywraca tożsamości lub urządzenie to bezpieczne i usuwa poprzednie zdarzenia ryzyko związane z tożsamości lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="3bb52-159">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

### <a name="resolved-risk-event"></a><span data-ttu-id="3bb52-160">Rozwiązany (ryzyka zdarzenie)</span><span class="sxs-lookup"><span data-stu-id="3bb52-160">Resolved (risk event)</span></span>
<span data-ttu-id="3bb52-161">Stan zdarzenia ryzyka ustawionych ręcznie przez użytkownika ochronę tożsamości, wskazujący, że użytkownik miał akcji korygowania odpowiednie poza ochrony tożsamości i że zdarzenia ryzyka należy traktować jako zamknięte.</span><span class="sxs-lookup"><span data-stu-id="3bb52-161">A risk event status set manually by an Identity Protection user, indicating that the user took an appropriate remediation action outside Identity Protection, and that the risk event should be considered closed.</span></span>

### <a name="risk-event-status"></a><span data-ttu-id="3bb52-162">Stan zdarzenia ryzyka</span><span class="sxs-lookup"><span data-stu-id="3bb52-162">Risk event status</span></span>
<span data-ttu-id="3bb52-163">Właściwości zdarzenia ryzyka, wskazującą, czy zdarzenie jest aktywne, a jeśli zamknięte, przyczynę zamknięcia go.</span><span class="sxs-lookup"><span data-stu-id="3bb52-163">A property of a risk event, indicating whether the event is active, and if closed, the reason for closing it.</span></span>

### <a name="risk-event-type"></a><span data-ttu-id="3bb52-164">Typ zdarzenia ryzyka</span><span class="sxs-lookup"><span data-stu-id="3bb52-164">Risk event type</span></span>
<span data-ttu-id="3bb52-165">Kategoria zdarzenia ryzyka, wskazujący typ anomalii, który spowodował zdarzenie uważane za ryzykowne.</span><span class="sxs-lookup"><span data-stu-id="3bb52-165">A category for the risk event, indicating the type of anomaly that caused the event to be considered risky.</span></span>

### <a name="risk-level-risk-event"></a><span data-ttu-id="3bb52-166">Poziom ryzyka (ryzyka zdarzenie)</span><span class="sxs-lookup"><span data-stu-id="3bb52-166">Risk level (risk event)</span></span>
<span data-ttu-id="3bb52-167">Wskazanie (wysoki, średni lub niski) priorytetu zdarzenia ryzyka, aby ułatwić użytkownikom ochronę tożsamości priorytetów działania podjęte w celu zmniejszenia ryzyka do organizacji.</span><span class="sxs-lookup"><span data-stu-id="3bb52-167">An indication (High, Medium, or Low) of the severity of the risk event to help Identity Protection users prioritize the actions they take to reduce the risk to their organization.</span></span> 

### <a name="risk-level-sign-in"></a><span data-ttu-id="3bb52-168">Poziom ryzyka (logowanie)</span><span class="sxs-lookup"><span data-stu-id="3bb52-168">Risk level (sign-in)</span></span>
<span data-ttu-id="3bb52-169">Wskazanie (wysoki, średni lub niski) prawdopodobieństwo, że dla określonych logowania, ktoś próbuje użyć tożsamość użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3bb52-169">An indication (High, Medium, or Low) of the likelihood that for a specific sign-in, someone else is attempting to use the user’s identity.</span></span>

### <a name="risk-level-user-compromise"></a><span data-ttu-id="3bb52-170">Poziom ryzyka (naruszenia zabezpieczeń użytkownika)</span><span class="sxs-lookup"><span data-stu-id="3bb52-170">Risk level (user compromise)</span></span>
<span data-ttu-id="3bb52-171">Wskazanie (wysoki, średni lub niski) prawdopodobieństwo, że naruszono tożsamości.</span><span class="sxs-lookup"><span data-stu-id="3bb52-171">An indication (High, Medium, or Low) of the likelihood that an identity has been compromised.</span></span>

### <a name="risk-level-vulnerability"></a><span data-ttu-id="3bb52-172">Poziom ryzyka (luki w zabezpieczeniach)</span><span class="sxs-lookup"><span data-stu-id="3bb52-172">Risk level (vulnerability)</span></span>
<span data-ttu-id="3bb52-173">Wskazanie (wysoki, średni lub niski) ważności luki w zabezpieczeniach, aby ułatwić użytkownikom ochronę tożsamości priorytetów działania podjęte w celu zmniejszenia ryzyka do organizacji.</span><span class="sxs-lookup"><span data-stu-id="3bb52-173">An indication (High, Medium, or Low) of the severity of the vulnerability to help Identity Protection users prioritize the actions they take to reduce the risk to their organization.</span></span>

### <a name="secure-identity"></a><span data-ttu-id="3bb52-174">Secure (tożsamości)</span><span class="sxs-lookup"><span data-stu-id="3bb52-174">Secure (identity)</span></span>
<span data-ttu-id="3bb52-175">Należy podjąć akcję naprawczą, takie jak zmiany hasła lub ponownej instalacji systemu do przywrócenia tożsamości potencjalnie złamany do stanu, który nie został naruszony maszyny.</span><span class="sxs-lookup"><span data-stu-id="3bb52-175">Take remediation action such as a password change or machine reimaging to restore a potentially compromised identity to an uncompromised state.</span></span>

### <a name="security-policy"></a><span data-ttu-id="3bb52-176">Zasady zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="3bb52-176">Security policy</span></span>
<span data-ttu-id="3bb52-177">Kolekcja reguł zasad i warunek.</span><span class="sxs-lookup"><span data-stu-id="3bb52-177">A collection of policy rules and condition.</span></span> <span data-ttu-id="3bb52-178">Zasady można zastosować do jednostek, takich jak użytkownicy, grupy aplikacji, urządzeń, platformy urządzeń, Stany urządzeń, zakresy adresów IP i Auth2.0 typy klientów.</span><span class="sxs-lookup"><span data-stu-id="3bb52-178">A policy can be applied to entities such as users, groups, apps, devices, device platforms, device states, IP ranges, and Auth2.0 client types.</span></span> <span data-ttu-id="3bb52-179">Gdy jest włączona, zostanie ona potraktowana zawsze, gdy jednostka uwzględnionych w zasadach jest wystawiony token dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="3bb52-179">When a policy is enabled, it is evaluated whenever an entity included in the policy is issued a token for a resource.</span></span>

### <a name="sign-in-v"></a><span data-ttu-id="3bb52-180">Zaloguj się (v)</span><span class="sxs-lookup"><span data-stu-id="3bb52-180">Sign in (v)</span></span>
<span data-ttu-id="3bb52-181">Do uwierzytelniania tożsamości w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3bb52-181">To authenticate to an identity in Azure Active Directory.</span></span>

### <a name="sign-in-n"></a><span data-ttu-id="3bb52-182">Logowania (n)</span><span class="sxs-lookup"><span data-stu-id="3bb52-182">Sign-in (n)</span></span>
<span data-ttu-id="3bb52-183">Proces lub akcji uwierzytelniania tożsamości w usłudze Azure Active Directory i zdarzenia, który przechwytuje tej operacji.</span><span class="sxs-lookup"><span data-stu-id="3bb52-183">The process or action of authenticating an identity in Azure Active Directory, and the event that captures this operation.</span></span>

### <a name="sign-in-from-anonymous-ip-address"></a><span data-ttu-id="3bb52-184">Logowania z anonimowych adresów IP</span><span class="sxs-lookup"><span data-stu-id="3bb52-184">Sign-in from anonymous IP address</span></span>
<span data-ttu-id="3bb52-185">Zdarzenie ryzyka wyzwalane po pomyślnym zalogowaniu z adresu IP, który został zidentyfikowany jako adres IP anonimowy serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="3bb52-185">A risk event triggered after a successful sign-in from IP address that has been identified as an anonymous proxy IP address.</span></span>

### <a name="sign-in-from-infected-device"></a><span data-ttu-id="3bb52-186">Logowania z zainfekowanych urządzeń</span><span class="sxs-lookup"><span data-stu-id="3bb52-186">Sign-in from infected device</span></span>
<span data-ttu-id="3bb52-187">Zdarzenie ryzyka, wyzwalane, gdy logowania pochodzi z adresu IP, w których jest używane przez jedną lub więcej urządzeń ze złamanymi zabezpieczeniami, które aktywnie próby komunikacji z serwerem botów.</span><span class="sxs-lookup"><span data-stu-id="3bb52-187">A risk event triggered when a sign-in originates from an IP address which is known to be used by one or more compromised devices, which are actively attempting to communicate with a bot server.</span></span>

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a><span data-ttu-id="3bb52-188">Logowania z adresów IP związanych z podejrzanymi działaniami</span><span class="sxs-lookup"><span data-stu-id="3bb52-188">Sign-in from IP address with suspicious activity</span></span>
<span data-ttu-id="3bb52-189">Zdarzenie ryzyka wyzwalane po pomyślnym logowanie z adresu IP adresów z dużej liczby nieudanych prób logowania na wielu kontach użytkowników w krótkim przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="3bb52-189">A risk event triggered after a successful sign-in from an IP address with a high number of failed login attempts across multiple user accounts over a short period of time.</span></span>

### <a name="sign-in-from-unfamiliar-location"></a><span data-ttu-id="3bb52-190">Logowania z nieznanych lokalizacji</span><span class="sxs-lookup"><span data-stu-id="3bb52-190">Sign-in from unfamiliar location</span></span>
<span data-ttu-id="3bb52-191">Zdarzenie ryzyka, wyzwalane, gdy użytkownik pomyślnie loguje się z nowej lokalizacji (adresu IP, szerokości geograficznej/długości i ASN).</span><span class="sxs-lookup"><span data-stu-id="3bb52-191">A risk event triggered when a user successfully signs in from a new location (IP, Latitude/Longitude and ASN).</span></span>

### <a name="sign-in-risk"></a><span data-ttu-id="3bb52-192">Ryzyko logowania</span><span class="sxs-lookup"><span data-stu-id="3bb52-192">Sign-in risk</span></span>
<span data-ttu-id="3bb52-193">Zobacz ryzyka poziom (logowanie)</span><span class="sxs-lookup"><span data-stu-id="3bb52-193">See Risk level (sign-in)</span></span>

### <a name="sign-in-risk-policy"></a><span data-ttu-id="3bb52-194">Zasady logowania ryzyka</span><span class="sxs-lookup"><span data-stu-id="3bb52-194">Sign-in risk policy</span></span>
<span data-ttu-id="3bb52-195">Zasady dostępu warunkowego, która ocenia ryzyko dla określonych logowanie i stosuje środki zaradcze, na podstawie wstępnie zdefiniowane warunki i zasady.</span><span class="sxs-lookup"><span data-stu-id="3bb52-195">A conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="user-compromise-risk"></a><span data-ttu-id="3bb52-196">Ryzyko naruszenia zabezpieczeń użytkownika</span><span class="sxs-lookup"><span data-stu-id="3bb52-196">User compromise risk</span></span>
<span data-ttu-id="3bb52-197">Zobacz ryzyka poziom (naruszenia zabezpieczeń użytkownika)</span><span class="sxs-lookup"><span data-stu-id="3bb52-197">See Risk level (user compromise)</span></span>

### <a name="user-risk"></a><span data-ttu-id="3bb52-198">Ryzyko użytkownika</span><span class="sxs-lookup"><span data-stu-id="3bb52-198">User risk</span></span>
<span data-ttu-id="3bb52-199">Zobacz ryzyka poziom (naruszenia zabezpieczeń użytkownika).</span><span class="sxs-lookup"><span data-stu-id="3bb52-199">See Risk level (user compromise).</span></span>

### <a name="user-risk-policy"></a><span data-ttu-id="3bb52-200">Zasady użytkownika ryzyka</span><span class="sxs-lookup"><span data-stu-id="3bb52-200">User risk policy</span></span>
<span data-ttu-id="3bb52-201">Zasady dostępu warunkowego, która uwzględnia przy logowaniu i stosuje środki zaradcze, na podstawie wstępnie zdefiniowane warunki i zasady.</span><span class="sxs-lookup"><span data-stu-id="3bb52-201">A conditional access policy that considers the sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="users-flagged-for-risk"></a><span data-ttu-id="3bb52-202">Użytkownicy oflagowani w związku z ryzykiem</span><span class="sxs-lookup"><span data-stu-id="3bb52-202">Users flagged for risk</span></span>
<span data-ttu-id="3bb52-203">Użytkownicy, którzy mają zdarzenia ryzyka, które są aktywne lub skorygowanych</span><span class="sxs-lookup"><span data-stu-id="3bb52-203">Users that have risk events which are either active or remediated</span></span>

### <a name="vulnerability"></a><span data-ttu-id="3bb52-204">Luki w zabezpieczeniach</span><span class="sxs-lookup"><span data-stu-id="3bb52-204">Vulnerability</span></span>
<span data-ttu-id="3bb52-205">Konfiguracja lub warunku w usłudze Azure Active Directory, co sprawia, że katalog jest podatna na luki w zabezpieczeniach i zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="3bb52-205">A configuration or condition in Azure Active Directory which makes the directory susceptible to exploits or threats.</span></span>

## <a name="see-also"></a><span data-ttu-id="3bb52-206">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="3bb52-206">See also</span></span>
* [<span data-ttu-id="3bb52-207">Ochronę tożsamości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3bb52-207">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

