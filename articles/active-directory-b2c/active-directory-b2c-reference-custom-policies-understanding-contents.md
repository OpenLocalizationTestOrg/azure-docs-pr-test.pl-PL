---
title: "Usługa Azure Active Directory B2C: Opis zasady niestandardowe pakietu starter | Dokumentacja firmy Microsoft"
description: "Temat dotyczący zasad niestandardowych usługi Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 9847bcfcc139a769847678c1cca6a8b9c3a30e93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-the-custom-policies-of-the-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="1a69e-103">Opis zasad niestandardowych początkowego pakietu Azure AD B2C niestandardowych zasad</span><span class="sxs-lookup"><span data-stu-id="1a69e-103">Understanding the custom policies of the Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="1a69e-104">Ta sekcja zawiera listę wszystkich elementów podstawowych zasad B2C_1A_base, który jest dostarczany z **pakiet początkowy** i która jest wykorzystywana do tworzenia własnych zasad za pomocą dziedziczenia obiektu *B2C_1A_base_extensions zasad* .</span><span class="sxs-lookup"><span data-stu-id="1a69e-104">This section lists all the core elements of the B2C_1A_base policy that comes with the **Starter Pack** and that is leveraged for authoring your own policies through the inheritance of the *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="1a69e-105">Tak on bardziej szczegółowo skupia się na typy oświadczeń już zdefiniowane, przekształcenia oświadczeń, definicje zawartości, dostawców oświadczeń z ich profile technicznych i podróże użytkownika core.</span><span class="sxs-lookup"><span data-stu-id="1a69e-105">As such, it more particularly focusses on the already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and the core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a69e-106">Microsoft nie udziela żadnych gwarancji, wprost względem z informacji podanych poniżej lub.</span><span class="sxs-lookup"><span data-stu-id="1a69e-106">Microsoft makes no warranties, express or implied, with respect to the information provided hereafter.</span></span> <span data-ttu-id="1a69e-107">Zmiany mogą być wprowadzane w dowolnym momencie przed upływem terminu GA w czasie GA lub po.</span><span class="sxs-lookup"><span data-stu-id="1a69e-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="1a69e-108">Zarówno własnych zasad, jak i zasady B2C_1A_base_extensions można zastąpić te definicje i rozszerzyć te zasady nadrzędnego zgodnie z potrzebami, podając te dodatkowe.</span><span class="sxs-lookup"><span data-stu-id="1a69e-108">Both your own policies and the B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="1a69e-109">Elementy podstawowe *zasad B2C_1A_base* są typy oświadczeń, przekształcenia oświadczeń i definicje zawartości.</span><span class="sxs-lookup"><span data-stu-id="1a69e-109">The core elements of the *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="1a69e-110">Te elementy można wrażliwych odwoływać się do własnych zasad, a także jako w *zasad B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="1a69e-110">These elements can susceptible to be referenced in your own policies as well as in the *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="1a69e-111">Schematy oświadczeń</span><span class="sxs-lookup"><span data-stu-id="1a69e-111">Claims schemas</span></span>

<span data-ttu-id="1a69e-112">Oświadczenia to schematów jest podzielone na trzy części:</span><span class="sxs-lookup"><span data-stu-id="1a69e-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="1a69e-113">Pierwsza sekcja wymieniono minimalne oświadczenia, które są wymagane dla podróże użytkownika do poprawnego działania.</span><span class="sxs-lookup"><span data-stu-id="1a69e-113">A first section that lists the minimum claims that are required for the user journeys to work properly.</span></span>
2.  <span data-ttu-id="1a69e-114">Drugiej sekcji lista oświadczeń wymagany w przypadku parametrów ciągu zapytania i inne specjalne parametry do przekazania do innych dostawców oświadczeń, szczególnie login.microsoftonline.com do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="1a69e-114">A second section that lists the claims required for query string parameters and other special parameters to be passed to other claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="1a69e-115">**Nie Modyfikuj tych oświadczeń**.</span><span class="sxs-lookup"><span data-stu-id="1a69e-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="1a69e-116">I po pewnym czasie trzeci sekcja, która wyświetla wszelkie dodatkowe, opcjonalne oświadczenia, które mogą być zbierane od użytkownika, przechowywane w katalogu i wysłane w tokenach podczas logowania.</span><span class="sxs-lookup"><span data-stu-id="1a69e-116">And eventually a third section that lists any additional, optional claims that can be collected from the user, stored in the directory and sent in tokens during sign in.</span></span> <span data-ttu-id="1a69e-117">W tej sekcji można dodać nowy typ oświadczenia zbierane od użytkownika i/lub w tokenie.</span><span class="sxs-lookup"><span data-stu-id="1a69e-117">New claims type to be collected from the user and/or sent in the token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a69e-118">Schemat oświadczeń zawiera ograniczenia dotyczące określonych oświadczeń, takich jak nazwy użytkowników i hasła.</span><span class="sxs-lookup"><span data-stu-id="1a69e-118">The claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="1a69e-119">Zasady zaufania Framework (TF) traktuje usługi Azure AD jako innego dostawcy oświadczeń i wszystkie jego ograniczenia są modelowany w zasadach premium.</span><span class="sxs-lookup"><span data-stu-id="1a69e-119">The Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in the premium policy.</span></span> <span data-ttu-id="1a69e-120">Aby dodać więcej ograniczeń, lub użyj innego dostawcy oświadczeń dla magazynu poświadczeń, który ma własną ograniczenia mogły zostać zmodyfikowane zasady.</span><span class="sxs-lookup"><span data-stu-id="1a69e-120">A policy could be modified to add more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="1a69e-121">Poniżej przedstawiono typy oświadczeń dostępne.</span><span class="sxs-lookup"><span data-stu-id="1a69e-121">The available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-the-user-journeys"></a><span data-ttu-id="1a69e-122">Oświadczenia, które są wymagane w przypadku podróży użytkownika</span><span class="sxs-lookup"><span data-stu-id="1a69e-122">Claims that are required for the user journeys</span></span>

<span data-ttu-id="1a69e-123">Następujące oświadczenia są wymagane dla użytkownika podróże do poprawnego działania:</span><span class="sxs-lookup"><span data-stu-id="1a69e-123">The following claims are required for user journeys to work properly:</span></span>

| <span data-ttu-id="1a69e-124">Typ oświadczenia</span><span class="sxs-lookup"><span data-stu-id="1a69e-124">Claims type</span></span> | <span data-ttu-id="1a69e-125">Opis</span><span class="sxs-lookup"><span data-stu-id="1a69e-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="1a69e-126">*Nazwa użytkownika*</span><span class="sxs-lookup"><span data-stu-id="1a69e-126">*UserId*</span></span> | <span data-ttu-id="1a69e-127">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="1a69e-127">Username</span></span> |
| <span data-ttu-id="1a69e-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="1a69e-128">*signInName*</span></span> | <span data-ttu-id="1a69e-129">Zaloguj się w nazwie</span><span class="sxs-lookup"><span data-stu-id="1a69e-129">Sign in name</span></span> |
| <span data-ttu-id="1a69e-130">*dla identyfikatora dzierżawcy*</span><span class="sxs-lookup"><span data-stu-id="1a69e-130">*tenantId*</span></span> | <span data-ttu-id="1a69e-131">Identyfikator dzierżawy (ID) obiektu użytkownika w usłudze Azure AD B2C w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="1a69e-131">Tenant identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="1a69e-132">*Identyfikator obiektu*</span><span class="sxs-lookup"><span data-stu-id="1a69e-132">*objectId*</span></span> | <span data-ttu-id="1a69e-133">Identyfikator obiektu (ID) obiektu użytkownika w usłudze Azure AD B2C w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="1a69e-133">Object identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="1a69e-134">*hasło*</span><span class="sxs-lookup"><span data-stu-id="1a69e-134">*password*</span></span> | <span data-ttu-id="1a69e-135">Hasło</span><span class="sxs-lookup"><span data-stu-id="1a69e-135">Password</span></span> |
| <span data-ttu-id="1a69e-136">*NoweHasło*</span><span class="sxs-lookup"><span data-stu-id="1a69e-136">*newPassword*</span></span> | |
| <span data-ttu-id="1a69e-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="1a69e-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="1a69e-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="1a69e-138">*passwordPolicies*</span></span> | <span data-ttu-id="1a69e-139">Zasady haseł używane przez usługi Azure AD B2C Premium do określenia siły hasła, wygaśnięcia itp.</span><span class="sxs-lookup"><span data-stu-id="1a69e-139">Password policies used by Azure AD B2C Premium to determine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="1a69e-140">*Sub*</span><span class="sxs-lookup"><span data-stu-id="1a69e-140">*sub*</span></span> | |
| <span data-ttu-id="1a69e-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="1a69e-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="1a69e-142">*identityProvider*</span><span class="sxs-lookup"><span data-stu-id="1a69e-142">*identityProvider*</span></span> | |
| <span data-ttu-id="1a69e-143">*Nazwa wyświetlana*</span><span class="sxs-lookup"><span data-stu-id="1a69e-143">*displayName*</span></span> | |
| <span data-ttu-id="1a69e-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="1a69e-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="1a69e-145">Numer telefonu użytkownika</span><span class="sxs-lookup"><span data-stu-id="1a69e-145">User's telephone number</span></span> |
| <span data-ttu-id="1a69e-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="1a69e-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="1a69e-147">*Adres e-mail*</span><span class="sxs-lookup"><span data-stu-id="1a69e-147">*email*</span></span> | <span data-ttu-id="1a69e-148">Adres e-mail, który może służyć do kontaktowania się z użytkownika</span><span class="sxs-lookup"><span data-stu-id="1a69e-148">Email address that can be used to contact the user</span></span> |
| <span data-ttu-id="1a69e-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="1a69e-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="1a69e-150">Adres e-mail, który użytkownik może użyć do logowania</span><span class="sxs-lookup"><span data-stu-id="1a69e-150">Email address that the user can use to sign in</span></span> |
| <span data-ttu-id="1a69e-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="1a69e-151">*otherMails*</span></span> | <span data-ttu-id="1a69e-152">Adresy e-mail, które mogą być używane do kontaktu użytkownik</span><span class="sxs-lookup"><span data-stu-id="1a69e-152">Email addresses that can be used to contact the user</span></span> |
| <span data-ttu-id="1a69e-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="1a69e-153">*userPrincipalName*</span></span> | <span data-ttu-id="1a69e-154">Nazwa użytkownika zapisaną w warstwie Premium usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="1a69e-154">Username as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="1a69e-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="1a69e-155">*upnUserName*</span></span> | <span data-ttu-id="1a69e-156">Nazwa użytkownika do tworzenia głównej nazwy użytkownika</span><span class="sxs-lookup"><span data-stu-id="1a69e-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="1a69e-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="1a69e-157">*mailNickName*</span></span> | <span data-ttu-id="1a69e-158">Nazwa użytkownika poczty nick przechowywanej w usłudze Azure AD B2C — wersja Premium</span><span class="sxs-lookup"><span data-stu-id="1a69e-158">User's mail nick name as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="1a69e-159">*newUser*</span><span class="sxs-lookup"><span data-stu-id="1a69e-159">*newUser*</span></span> | |
| <span data-ttu-id="1a69e-160">*Wykonano SelfAsserted — dane wejściowe*</span><span class="sxs-lookup"><span data-stu-id="1a69e-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="1a69e-161">Oświadczenie, które określa, czy atrybuty zostały zebrane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="1a69e-161">Claim that specifies whether attributes were collected from the user</span></span> |
| <span data-ttu-id="1a69e-162">*Wykonano PhoneFactor — dane wejściowe*</span><span class="sxs-lookup"><span data-stu-id="1a69e-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="1a69e-163">Oświadczenie, które określa, czy nowy numer telefonu został zebrany przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="1a69e-163">Claim that specifies whether a new phone number was collected from the user</span></span> |
| <span data-ttu-id="1a69e-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="1a69e-164">*authenticationSource*</span></span> | <span data-ttu-id="1a69e-165">Określa, czy użytkownik został uwierzytelniony w społecznościowych dostawcy tożsamości, login.microsoftonline.com lub lokalnego konta</span><span class="sxs-lookup"><span data-stu-id="1a69e-165">Specifies whether the user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="1a69e-166">Oświadczenia wymagane w celu parametrów ciągu zapytania i inne parametry specjalne</span><span class="sxs-lookup"><span data-stu-id="1a69e-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="1a69e-167">Następujące oświadczenia są wymagane do przekazania na specjalne parametry (w tym niektórych parametrów ciągu zapytania) do innych dostawców oświadczeń:</span><span class="sxs-lookup"><span data-stu-id="1a69e-167">The following claims are required to pass on special parameters (including some query string parameters) to other claims providers:</span></span>

| <span data-ttu-id="1a69e-168">Typ oświadczenia</span><span class="sxs-lookup"><span data-stu-id="1a69e-168">Claims type</span></span> | <span data-ttu-id="1a69e-169">Opis</span><span class="sxs-lookup"><span data-stu-id="1a69e-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="1a69e-170">*nux*</span><span class="sxs-lookup"><span data-stu-id="1a69e-170">*nux*</span></span> | <span data-ttu-id="1a69e-171">Specjalne parametr przekazany do uwierzytelniania konta lokalnego do login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="1a69e-171">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="1a69e-172">*Asystent łączności sieciowej*</span><span class="sxs-lookup"><span data-stu-id="1a69e-172">*nca*</span></span> | <span data-ttu-id="1a69e-173">Specjalne parametr przekazany do uwierzytelniania konta lokalnego do login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="1a69e-173">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="1a69e-174">*wiersz*</span><span class="sxs-lookup"><span data-stu-id="1a69e-174">*prompt*</span></span> | <span data-ttu-id="1a69e-175">Specjalne parametr przekazany do uwierzytelniania konta lokalnego do login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="1a69e-175">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="1a69e-176">*mkt*</span><span class="sxs-lookup"><span data-stu-id="1a69e-176">*mkt*</span></span> | <span data-ttu-id="1a69e-177">Specjalne parametr przekazany do uwierzytelniania konta lokalnego do login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="1a69e-177">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="1a69e-178">*LC*</span><span class="sxs-lookup"><span data-stu-id="1a69e-178">*lc*</span></span> | <span data-ttu-id="1a69e-179">Specjalne parametr przekazany do uwierzytelniania konta lokalnego do login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="1a69e-179">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="1a69e-180">*Typ grant_type*</span><span class="sxs-lookup"><span data-stu-id="1a69e-180">*grant_type*</span></span> | <span data-ttu-id="1a69e-181">Specjalne parametr przekazany do uwierzytelniania konta lokalnego do login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="1a69e-181">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="1a69e-182">*zakres*</span><span class="sxs-lookup"><span data-stu-id="1a69e-182">*scope*</span></span> | <span data-ttu-id="1a69e-183">Specjalne parametr przekazany do uwierzytelniania konta lokalnego do login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="1a69e-183">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="1a69e-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="1a69e-184">*client_id*</span></span> | <span data-ttu-id="1a69e-185">Specjalne parametr przekazany do uwierzytelniania konta lokalnego do login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="1a69e-185">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="1a69e-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="1a69e-186">*objectIdFromSession*</span></span> | <span data-ttu-id="1a69e-187">Parametr udostępniane przez dostawcę zarządzania sesji domyślnej, aby wskazać, że identyfikator obiektu zostały pobrane z sesji rejestracji Jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1a69e-187">Parameter provided by the default session management provider to indicate that the object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="1a69e-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="1a69e-188">*isActiveMFASession*</span></span> | <span data-ttu-id="1a69e-189">Udostępniony parametr przez Zarządzanie sesjami MFA wskazująca, czy użytkownik ma aktywnej sesji usługi MFA</span><span class="sxs-lookup"><span data-stu-id="1a69e-189">Parameter provided by the MFA session management to indicate that the user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="1a69e-190">Dodatkowe oświadczenia (opcjonalnie), które mogą być zbierane</span><span class="sxs-lookup"><span data-stu-id="1a69e-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="1a69e-191">Następujące oświadczenia są dodatkowe oświadczenia, które mogą być zebrane od użytkowników, przechowywane w katalogu i wysłane w tokenie.</span><span class="sxs-lookup"><span data-stu-id="1a69e-191">The following claims are additional claims that can be collected from the users, stored in the directory, and sent in the token.</span></span> <span data-ttu-id="1a69e-192">Zgodnie z opisem przed, dodatkowe oświadczeń można dodać do tej listy.</span><span class="sxs-lookup"><span data-stu-id="1a69e-192">As outlined before, additional claims can be added to this list.</span></span>

| <span data-ttu-id="1a69e-193">Typ oświadczenia</span><span class="sxs-lookup"><span data-stu-id="1a69e-193">Claims type</span></span> | <span data-ttu-id="1a69e-194">Opis</span><span class="sxs-lookup"><span data-stu-id="1a69e-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="1a69e-195">*Imię*</span><span class="sxs-lookup"><span data-stu-id="1a69e-195">*givenName*</span></span> | <span data-ttu-id="1a69e-196">Imię użytkownika (znanej także jako nazwa pierwszej)</span><span class="sxs-lookup"><span data-stu-id="1a69e-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="1a69e-197">*nazwisko*</span><span class="sxs-lookup"><span data-stu-id="1a69e-197">*surname*</span></span> | <span data-ttu-id="1a69e-198">Nazwisko użytkownika (znanej także jako nazwa rodziny lub nazwisko)</span><span class="sxs-lookup"><span data-stu-id="1a69e-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="1a69e-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="1a69e-199">*Extension_picture*</span></span> | <span data-ttu-id="1a69e-200">Obraz użytkownika z społecznego</span><span class="sxs-lookup"><span data-stu-id="1a69e-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="1a69e-201">Przekształcenia oświadczeń</span><span class="sxs-lookup"><span data-stu-id="1a69e-201">Claim transformations</span></span>

<span data-ttu-id="1a69e-202">Przekształcenia oświadczeń dostępne są wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="1a69e-202">The available claim transformations are listed below.</span></span>

| <span data-ttu-id="1a69e-203">Przekształcania oświadczeń</span><span class="sxs-lookup"><span data-stu-id="1a69e-203">Claim transformation</span></span> | <span data-ttu-id="1a69e-204">Opis</span><span class="sxs-lookup"><span data-stu-id="1a69e-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="1a69e-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="1a69e-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="1a69e-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="1a69e-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="1a69e-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="1a69e-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="1a69e-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="1a69e-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="1a69e-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="1a69e-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="1a69e-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="1a69e-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="1a69e-211">Definicje zawartości</span><span class="sxs-lookup"><span data-stu-id="1a69e-211">Content definitions</span></span>

<span data-ttu-id="1a69e-212">W tej sekcji opisano zawartości definicje już zadeklarowany w *B2C_1A_base* zasad.</span><span class="sxs-lookup"><span data-stu-id="1a69e-212">This section describes the content definitions already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="1a69e-213">Te definicje zawartości są podatne na odwołuje się do, przesłonięcia i rozszerzony w własnych zasad, a także jako w miarę potrzeb *B2C_1A_base_extensions* zasad.</span><span class="sxs-lookup"><span data-stu-id="1a69e-213">These content definitions are susceptible to be referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="1a69e-214">Dostawcy oświadczeń</span><span class="sxs-lookup"><span data-stu-id="1a69e-214">Claims provider</span></span> | <span data-ttu-id="1a69e-215">Opis</span><span class="sxs-lookup"><span data-stu-id="1a69e-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="1a69e-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="1a69e-216">*Facebook*</span></span> | |
| <span data-ttu-id="1a69e-217">*Logowanie konta lokalnego*</span><span class="sxs-lookup"><span data-stu-id="1a69e-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="1a69e-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="1a69e-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="1a69e-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="1a69e-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="1a69e-220">*Samodzielnie potwierdzony*</span><span class="sxs-lookup"><span data-stu-id="1a69e-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="1a69e-221">*Konto lokalne*</span><span class="sxs-lookup"><span data-stu-id="1a69e-221">*Local Account*</span></span> | |
| <span data-ttu-id="1a69e-222">*Zarządzanie sesjami*</span><span class="sxs-lookup"><span data-stu-id="1a69e-222">*Session Management*</span></span> | |
| <span data-ttu-id="1a69e-223">*Aparat zasad Trustframework*</span><span class="sxs-lookup"><span data-stu-id="1a69e-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="1a69e-224">*TechnicalProfiles*</span><span class="sxs-lookup"><span data-stu-id="1a69e-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="1a69e-225">*Wystawca tokenu*</span><span class="sxs-lookup"><span data-stu-id="1a69e-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="1a69e-226">Profile techniczne</span><span class="sxs-lookup"><span data-stu-id="1a69e-226">Technical profiles</span></span>

<span data-ttu-id="1a69e-227">W tej sekcji przedstawiono techniczne profile już zadeklarowana dla dostawcy oświadczeń w *B2C_1A_base* zasad.</span><span class="sxs-lookup"><span data-stu-id="1a69e-227">This section depicts the technical profiles already declared per claim provider in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="1a69e-228">Te profile techniczne są podatne na dalsze odwołuje się do, zastąpiona, i/lub być rozszerzony w własnych zasad, a także jako w miarę potrzeb *B2C_1A_base_extensions* zasad.</span><span class="sxs-lookup"><span data-stu-id="1a69e-228">These technical profiles are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="1a69e-229">Profile techniczne dla usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="1a69e-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="1a69e-230">Profil techniczne</span><span class="sxs-lookup"><span data-stu-id="1a69e-230">Technical profile</span></span> | <span data-ttu-id="1a69e-231">Opis</span><span class="sxs-lookup"><span data-stu-id="1a69e-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="1a69e-232">*Facebook OAUTH*</span><span class="sxs-lookup"><span data-stu-id="1a69e-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="1a69e-233">Profile techniczne dla lokalnego konta logowanie</span><span class="sxs-lookup"><span data-stu-id="1a69e-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="1a69e-234">Profil techniczne</span><span class="sxs-lookup"><span data-stu-id="1a69e-234">Technical profile</span></span> | <span data-ttu-id="1a69e-235">Opis</span><span class="sxs-lookup"><span data-stu-id="1a69e-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="1a69e-236">*Logowania nieinterakcyjnego*</span><span class="sxs-lookup"><span data-stu-id="1a69e-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="1a69e-237">Profile techniczne dla aplikacji Phone Factor</span><span class="sxs-lookup"><span data-stu-id="1a69e-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="1a69e-238">Profil techniczne</span><span class="sxs-lookup"><span data-stu-id="1a69e-238">Technical profile</span></span> | <span data-ttu-id="1a69e-239">Opis</span><span class="sxs-lookup"><span data-stu-id="1a69e-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="1a69e-240">*Dane wejściowe PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="1a69e-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="1a69e-241">*PhoneFactor InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="1a69e-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="1a69e-242">*Sprawdź PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="1a69e-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="1a69e-243">Profile techniczne dotyczące usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a69e-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="1a69e-244">Profil techniczne</span><span class="sxs-lookup"><span data-stu-id="1a69e-244">Technical profile</span></span> | <span data-ttu-id="1a69e-245">Opis</span><span class="sxs-lookup"><span data-stu-id="1a69e-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="1a69e-246">*Typowe usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="1a69e-246">*AAD-Common*</span></span> | <span data-ttu-id="1a69e-247">Techniczne dołączonego przez innych profilów techniczne AAD xxx profilu</span><span class="sxs-lookup"><span data-stu-id="1a69e-247">Technical profile included by the other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="1a69e-248">*UserWriteUsingAlternativeSecurityId usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="1a69e-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="1a69e-249">Profil techniczne dla logowania społecznościowych</span><span class="sxs-lookup"><span data-stu-id="1a69e-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="1a69e-250">*UserReadUsingAlternativeSecurityId usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="1a69e-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="1a69e-251">Profil techniczne dla logowania społecznościowych</span><span class="sxs-lookup"><span data-stu-id="1a69e-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="1a69e-252">*AAD-UserReadUsingAlternativeSecurityId-brak błędu*</span><span class="sxs-lookup"><span data-stu-id="1a69e-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="1a69e-253">Profil techniczne dla logowania społecznościowych</span><span class="sxs-lookup"><span data-stu-id="1a69e-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="1a69e-254">*UserWritePasswordUsingLogonEmail usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="1a69e-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="1a69e-255">Profil techniczne dla kont lokalnych</span><span class="sxs-lookup"><span data-stu-id="1a69e-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="1a69e-256">*UserReadUsingEmailAddress usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="1a69e-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="1a69e-257">Profil techniczne dla kont lokalnych</span><span class="sxs-lookup"><span data-stu-id="1a69e-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="1a69e-258">*UserWriteProfileUsingObjectId usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="1a69e-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="1a69e-259">Profil techniczne aktualizowania rekordu użytkownika przy użyciu objectId</span><span class="sxs-lookup"><span data-stu-id="1a69e-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="1a69e-260">*UserWritePhoneNumberUsingObjectId usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="1a69e-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="1a69e-261">Profil techniczne aktualizowania rekordu użytkownika przy użyciu objectId</span><span class="sxs-lookup"><span data-stu-id="1a69e-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="1a69e-262">*UserWritePasswordUsingObjectId usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="1a69e-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="1a69e-263">Profil techniczne aktualizowania rekordu użytkownika przy użyciu objectId</span><span class="sxs-lookup"><span data-stu-id="1a69e-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="1a69e-264">*UserReadUsingObjectId usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="1a69e-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="1a69e-265">Techniczne profil jest używany do odczytywania danych po uwierzytelnia użytkownika</span><span class="sxs-lookup"><span data-stu-id="1a69e-265">Technical profile is used to read data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="1a69e-266">Profile techniczne dla potwierdzone samoobsługowego</span><span class="sxs-lookup"><span data-stu-id="1a69e-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="1a69e-267">Profil techniczne</span><span class="sxs-lookup"><span data-stu-id="1a69e-267">Technical profile</span></span> | <span data-ttu-id="1a69e-268">Opis</span><span class="sxs-lookup"><span data-stu-id="1a69e-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="1a69e-269">*Społecznego SelfAsserted*</span><span class="sxs-lookup"><span data-stu-id="1a69e-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="1a69e-270">*SelfAsserted ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="1a69e-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="1a69e-271">Profile techniczne dla lokalnego konta</span><span class="sxs-lookup"><span data-stu-id="1a69e-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="1a69e-272">Profil techniczne</span><span class="sxs-lookup"><span data-stu-id="1a69e-272">Technical profile</span></span> | <span data-ttu-id="1a69e-273">Opis</span><span class="sxs-lookup"><span data-stu-id="1a69e-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="1a69e-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="1a69e-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="1a69e-275">Profile techniczne dla sesji zarządzania</span><span class="sxs-lookup"><span data-stu-id="1a69e-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="1a69e-276">Profil techniczne</span><span class="sxs-lookup"><span data-stu-id="1a69e-276">Technical profile</span></span> | <span data-ttu-id="1a69e-277">Opis</span><span class="sxs-lookup"><span data-stu-id="1a69e-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="1a69e-278">*Operacja SM*</span><span class="sxs-lookup"><span data-stu-id="1a69e-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="1a69e-279">*SM AAD*</span><span class="sxs-lookup"><span data-stu-id="1a69e-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="1a69e-280">*SM SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="1a69e-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="1a69e-281">Nazwa profilu jest używana do odróżniania sesji AAD między logowania się i zaloguj się</span><span class="sxs-lookup"><span data-stu-id="1a69e-281">Profile name is being used to disambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="1a69e-282">*SM SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="1a69e-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="1a69e-283">*UWIERZYTELNIANIE WIELOSKŁADNIKOWE SM*</span><span class="sxs-lookup"><span data-stu-id="1a69e-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="1a69e-284">Profile techniczne dla TechnicalProfiles aparatu zasad Trustframework</span><span class="sxs-lookup"><span data-stu-id="1a69e-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="1a69e-285">Obecnie brak techniczne profilów są definiowane dla **TechnicalProfiles aparatu zasad Trustframework** dostawcy oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="1a69e-285">Currently, no technical profiles are defined for the **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="1a69e-286">Profile techniczne dla wystawcy tokenów</span><span class="sxs-lookup"><span data-stu-id="1a69e-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="1a69e-287">Profil techniczne</span><span class="sxs-lookup"><span data-stu-id="1a69e-287">Technical profile</span></span> | <span data-ttu-id="1a69e-288">Opis</span><span class="sxs-lookup"><span data-stu-id="1a69e-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="1a69e-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="1a69e-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="1a69e-290">Podróże użytkownika</span><span class="sxs-lookup"><span data-stu-id="1a69e-290">User journeys</span></span>

<span data-ttu-id="1a69e-291">W tej sekcji przedstawiono podróże użytkownik już zadeklarowany w *B2C_1A_base* zasad.</span><span class="sxs-lookup"><span data-stu-id="1a69e-291">This section depicts the user journeys already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="1a69e-292">Te podróże użytkownika są podatne na dalsze odwołuje się do, zastąpiona, i/lub być rozszerzony w własnych zasad, a także jako w miarę potrzeb *B2C_1A_base_extensions* zasad.</span><span class="sxs-lookup"><span data-stu-id="1a69e-292">These user journeys are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="1a69e-293">Przebieg użytkownika</span><span class="sxs-lookup"><span data-stu-id="1a69e-293">User journey</span></span> | <span data-ttu-id="1a69e-294">Opis</span><span class="sxs-lookup"><span data-stu-id="1a69e-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="1a69e-295">*Rejestracja*</span><span class="sxs-lookup"><span data-stu-id="1a69e-295">*SignUp*</span></span> | |
| <span data-ttu-id="1a69e-296">*Logowanie*</span><span class="sxs-lookup"><span data-stu-id="1a69e-296">*SignIn*</span></span> | |
| <span data-ttu-id="1a69e-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="1a69e-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="1a69e-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="1a69e-298">*EditProfile*</span></span> | |
| <span data-ttu-id="1a69e-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="1a69e-299">*PasswordReset*</span></span> | |
