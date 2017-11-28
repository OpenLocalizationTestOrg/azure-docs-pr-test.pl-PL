---
title: "Usługa Azure Active Directory B2C: Opis zasad niestandardowych hello początkowego pakietu | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="6a0da-103">Opis zasad niestandardowych hello hello Azure AD B2C zasady niestandardowe początkowego pakietu</span><span class="sxs-lookup"><span data-stu-id="6a0da-103">Understanding hello custom policies of hello Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="6a0da-104">Ta sekcja zawiera listę wszystkich elementów podstawowych hello hello B2C_1A_base zasady, które pochodzą z hello **pakiet początkowy** i która jest wykorzystywana do tworzenia własnych zasad za pomocą hello dziedziczenie hello *B2C_1A_base_ rozszerzenia zasad*.</span><span class="sxs-lookup"><span data-stu-id="6a0da-104">This section lists all hello core elements of hello B2C_1A_base policy that comes with hello **Starter Pack** and that is leveraged for authoring your own policies through hello inheritance of hello *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="6a0da-105">Tak on więcej szczególnie skupia się na powitania już zdefiniowane oświadczeń, typów, przekształcenia oświadczeń, definicje zawartości, dostawców oświadczeń z ich profile technicznych i hello podróże użytkownika core.</span><span class="sxs-lookup"><span data-stu-id="6a0da-105">As such, it more particularly focusses on hello already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and hello core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a0da-106">Microsoft nie udziela żadnych gwarancji, wyrażonych lub domniemanych, względem toohello informacje podane poniżej.</span><span class="sxs-lookup"><span data-stu-id="6a0da-106">Microsoft makes no warranties, express or implied, with respect toohello information provided hereafter.</span></span> <span data-ttu-id="6a0da-107">Zmiany mogą być wprowadzane w dowolnym momencie przed upływem terminu GA w czasie GA lub po.</span><span class="sxs-lookup"><span data-stu-id="6a0da-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="6a0da-108">Zarówno własnych zasad i hello B2C_1A_base_extensions zasad można zastąpić te definicje i rozszerzyć te zasady nadrzędnego zgodnie z potrzebami, podając te dodatkowe.</span><span class="sxs-lookup"><span data-stu-id="6a0da-108">Both your own policies and hello B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="6a0da-109">Witaj podstawowe elementy hello *zasad B2C_1A_base* są typy oświadczeń, przekształcenia oświadczeń i definicje zawartości.</span><span class="sxs-lookup"><span data-stu-id="6a0da-109">hello core elements of hello *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="6a0da-110">Te elementy można toobe wrażliwych, do którego odwołuje się własnych zasad, a także jak hello *zasad B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="6a0da-110">These elements can susceptible toobe referenced in your own policies as well as in hello *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="6a0da-111">Schematy oświadczeń</span><span class="sxs-lookup"><span data-stu-id="6a0da-111">Claims schemas</span></span>

<span data-ttu-id="6a0da-112">Oświadczenia to schematów jest podzielone na trzy części:</span><span class="sxs-lookup"><span data-stu-id="6a0da-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="6a0da-113">Pierwsza sekcja Lista oświadczeń minimalna hello, które są wymagane dla toowork podróże użytkownika hello poprawnie.</span><span class="sxs-lookup"><span data-stu-id="6a0da-113">A first section that lists hello minimum claims that are required for hello user journeys toowork properly.</span></span>
2.  <span data-ttu-id="6a0da-114">Druga sekcja list hello oświadczenia wymagane dla parametrów ciągu zapytania, a inne toobe specjalne parametry przekazane tooother dostawców oświadczeń, szczególnie login.microsoftonline.com do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="6a0da-114">A second section that lists hello claims required for query string parameters and other special parameters toobe passed tooother claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="6a0da-115">**Nie Modyfikuj tych oświadczeń**.</span><span class="sxs-lookup"><span data-stu-id="6a0da-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="6a0da-116">I po pewnym czasie trzeci sekcja, która wyświetla wszelkie dodatkowe, opcjonalne oświadczenia, które mogą być zbierane od użytkownika hello przechowywanych w katalogu hello i wysłane w tokenach podczas logowania.</span><span class="sxs-lookup"><span data-stu-id="6a0da-116">And eventually a third section that lists any additional, optional claims that can be collected from hello user, stored in hello directory and sent in tokens during sign in.</span></span> <span data-ttu-id="6a0da-117">W tej sekcji można dodawać nowych oświadczeń toobe typu zbierane od użytkownika hello i/lub wysyłane w tokenie hello.</span><span class="sxs-lookup"><span data-stu-id="6a0da-117">New claims type toobe collected from hello user and/or sent in hello token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a0da-118">Schemat oświadczeń Hello zawiera ograniczenia dotyczące określonych oświadczeń, takich jak nazwy użytkowników i hasła.</span><span class="sxs-lookup"><span data-stu-id="6a0da-118">hello claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="6a0da-119">Hello zasady zaufania Framework (TF) traktuje usługi Azure AD jako innego dostawcy oświadczeń i wszystkie jego ograniczenia są modelowany w hello premium zasad.</span><span class="sxs-lookup"><span data-stu-id="6a0da-119">hello Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in hello premium policy.</span></span> <span data-ttu-id="6a0da-120">Zasady można być zmodyfikowane tooadd więcej ograniczeń, lub użyj innego dostawcy oświadczeń do magazynu poświadczeń, który ma własną ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="6a0da-120">A policy could be modified tooadd more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="6a0da-121">Poniżej przedstawiono typy oświadczeń dostępne Hello.</span><span class="sxs-lookup"><span data-stu-id="6a0da-121">hello available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-hello-user-journeys"></a><span data-ttu-id="6a0da-122">Oświadczenia, które są wymagane dla hello podróże użytkownika</span><span class="sxs-lookup"><span data-stu-id="6a0da-122">Claims that are required for hello user journeys</span></span>

<span data-ttu-id="6a0da-123">powitania po oświadczenia są wymagane dla użytkownika podróże toowork prawidłowo:</span><span class="sxs-lookup"><span data-stu-id="6a0da-123">hello following claims are required for user journeys toowork properly:</span></span>

| <span data-ttu-id="6a0da-124">Typ oświadczenia</span><span class="sxs-lookup"><span data-stu-id="6a0da-124">Claims type</span></span> | <span data-ttu-id="6a0da-125">Opis</span><span class="sxs-lookup"><span data-stu-id="6a0da-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="6a0da-126">*Nazwa użytkownika*</span><span class="sxs-lookup"><span data-stu-id="6a0da-126">*UserId*</span></span> | <span data-ttu-id="6a0da-127">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="6a0da-127">Username</span></span> |
| <span data-ttu-id="6a0da-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="6a0da-128">*signInName*</span></span> | <span data-ttu-id="6a0da-129">Zaloguj się w nazwie</span><span class="sxs-lookup"><span data-stu-id="6a0da-129">Sign in name</span></span> |
| <span data-ttu-id="6a0da-130">*dla identyfikatora dzierżawcy*</span><span class="sxs-lookup"><span data-stu-id="6a0da-130">*tenantId*</span></span> | <span data-ttu-id="6a0da-131">Identyfikator dzierżawy (ID) hello obiektu użytkownika w usłudze Azure AD B2C w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="6a0da-131">Tenant identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="6a0da-132">*Identyfikator obiektu*</span><span class="sxs-lookup"><span data-stu-id="6a0da-132">*objectId*</span></span> | <span data-ttu-id="6a0da-133">Identyfikator obiektu (ID) hello obiektu użytkownika w usłudze Azure AD B2C w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="6a0da-133">Object identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="6a0da-134">*hasło*</span><span class="sxs-lookup"><span data-stu-id="6a0da-134">*password*</span></span> | <span data-ttu-id="6a0da-135">Hasło</span><span class="sxs-lookup"><span data-stu-id="6a0da-135">Password</span></span> |
| <span data-ttu-id="6a0da-136">*NoweHasło*</span><span class="sxs-lookup"><span data-stu-id="6a0da-136">*newPassword*</span></span> | |
| <span data-ttu-id="6a0da-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="6a0da-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="6a0da-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="6a0da-138">*passwordPolicies*</span></span> | <span data-ttu-id="6a0da-139">Zasady haseł używanych przez siły hasła toodetermine Premium usługi Azure AD B2C, wygaśnięcia itp.</span><span class="sxs-lookup"><span data-stu-id="6a0da-139">Password policies used by Azure AD B2C Premium toodetermine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="6a0da-140">*Sub*</span><span class="sxs-lookup"><span data-stu-id="6a0da-140">*sub*</span></span> | |
| <span data-ttu-id="6a0da-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="6a0da-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="6a0da-142">*identityProvider*</span><span class="sxs-lookup"><span data-stu-id="6a0da-142">*identityProvider*</span></span> | |
| <span data-ttu-id="6a0da-143">*Nazwa wyświetlana*</span><span class="sxs-lookup"><span data-stu-id="6a0da-143">*displayName*</span></span> | |
| <span data-ttu-id="6a0da-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="6a0da-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="6a0da-145">Numer telefonu użytkownika</span><span class="sxs-lookup"><span data-stu-id="6a0da-145">User's telephone number</span></span> |
| <span data-ttu-id="6a0da-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="6a0da-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="6a0da-147">*Adres e-mail*</span><span class="sxs-lookup"><span data-stu-id="6a0da-147">*email*</span></span> | <span data-ttu-id="6a0da-148">Adres e-mail, które mogą być używane toocontact hello użytkownika</span><span class="sxs-lookup"><span data-stu-id="6a0da-148">Email address that can be used toocontact hello user</span></span> |
| <span data-ttu-id="6a0da-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="6a0da-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="6a0da-150">Adres e-mail, który hello użytkownika można użyć toosign w</span><span class="sxs-lookup"><span data-stu-id="6a0da-150">Email address that hello user can use toosign in</span></span> |
| <span data-ttu-id="6a0da-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="6a0da-151">*otherMails*</span></span> | <span data-ttu-id="6a0da-152">Adresy e-mail, które mogą być używane toocontact hello użytkownika</span><span class="sxs-lookup"><span data-stu-id="6a0da-152">Email addresses that can be used toocontact hello user</span></span> |
| <span data-ttu-id="6a0da-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="6a0da-153">*userPrincipalName*</span></span> | <span data-ttu-id="6a0da-154">Nazwa użytkownika zapisaną w hello Premium usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="6a0da-154">Username as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="6a0da-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="6a0da-155">*upnUserName*</span></span> | <span data-ttu-id="6a0da-156">Nazwa użytkownika do tworzenia głównej nazwy użytkownika</span><span class="sxs-lookup"><span data-stu-id="6a0da-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="6a0da-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="6a0da-157">*mailNickName*</span></span> | <span data-ttu-id="6a0da-158">Nazwa użytkownika poczty nick zapisanymi hello Premium usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="6a0da-158">User's mail nick name as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="6a0da-159">*newUser*</span><span class="sxs-lookup"><span data-stu-id="6a0da-159">*newUser*</span></span> | |
| <span data-ttu-id="6a0da-160">*Wykonano SelfAsserted — dane wejściowe*</span><span class="sxs-lookup"><span data-stu-id="6a0da-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="6a0da-161">Oświadczenie, które określa, czy atrybuty zostały pobrane z hello użytkownika</span><span class="sxs-lookup"><span data-stu-id="6a0da-161">Claim that specifies whether attributes were collected from hello user</span></span> |
| <span data-ttu-id="6a0da-162">*Wykonano PhoneFactor — dane wejściowe*</span><span class="sxs-lookup"><span data-stu-id="6a0da-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="6a0da-163">Oświadczenie, które określa, czy nowy numer telefonu został zebrany hello użytkownika</span><span class="sxs-lookup"><span data-stu-id="6a0da-163">Claim that specifies whether a new phone number was collected from hello user</span></span> |
| <span data-ttu-id="6a0da-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="6a0da-164">*authenticationSource*</span></span> | <span data-ttu-id="6a0da-165">Określa, czy uwierzytelnienia użytkownika hello społecznościowych dostawcy tożsamości, login.microsoftonline.com lub konto lokalne</span><span class="sxs-lookup"><span data-stu-id="6a0da-165">Specifies whether hello user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="6a0da-166">Oświadczenia wymagane w celu parametrów ciągu zapytania i inne parametry specjalne</span><span class="sxs-lookup"><span data-stu-id="6a0da-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="6a0da-167">Witaj następujące oświadczenia są wymagane toopass na dostawców oświadczeń tooother specjalne parametry (w tym niektórych parametrów ciągu zapytania):</span><span class="sxs-lookup"><span data-stu-id="6a0da-167">hello following claims are required toopass on special parameters (including some query string parameters) tooother claims providers:</span></span>

| <span data-ttu-id="6a0da-168">Typ oświadczenia</span><span class="sxs-lookup"><span data-stu-id="6a0da-168">Claims type</span></span> | <span data-ttu-id="6a0da-169">Opis</span><span class="sxs-lookup"><span data-stu-id="6a0da-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="6a0da-170">*nux*</span><span class="sxs-lookup"><span data-stu-id="6a0da-170">*nux*</span></span> | <span data-ttu-id="6a0da-171">Specjalne parametr przekazany do konta lokalnego uwierzytelniania toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6a0da-171">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="6a0da-172">*Asystent łączności sieciowej*</span><span class="sxs-lookup"><span data-stu-id="6a0da-172">*nca*</span></span> | <span data-ttu-id="6a0da-173">Specjalne parametr przekazany do konta lokalnego uwierzytelniania toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6a0da-173">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="6a0da-174">*wiersz*</span><span class="sxs-lookup"><span data-stu-id="6a0da-174">*prompt*</span></span> | <span data-ttu-id="6a0da-175">Specjalne parametr przekazany do konta lokalnego uwierzytelniania toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6a0da-175">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="6a0da-176">*mkt*</span><span class="sxs-lookup"><span data-stu-id="6a0da-176">*mkt*</span></span> | <span data-ttu-id="6a0da-177">Specjalne parametr przekazany do konta lokalnego uwierzytelniania toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6a0da-177">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="6a0da-178">*LC*</span><span class="sxs-lookup"><span data-stu-id="6a0da-178">*lc*</span></span> | <span data-ttu-id="6a0da-179">Specjalne parametr przekazany do konta lokalnego uwierzytelniania toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6a0da-179">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="6a0da-180">*Typ grant_type*</span><span class="sxs-lookup"><span data-stu-id="6a0da-180">*grant_type*</span></span> | <span data-ttu-id="6a0da-181">Specjalne parametr przekazany do konta lokalnego uwierzytelniania toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6a0da-181">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="6a0da-182">*zakres*</span><span class="sxs-lookup"><span data-stu-id="6a0da-182">*scope*</span></span> | <span data-ttu-id="6a0da-183">Specjalne parametr przekazany do konta lokalnego uwierzytelniania toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6a0da-183">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="6a0da-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="6a0da-184">*client_id*</span></span> | <span data-ttu-id="6a0da-185">Specjalne parametr przekazany do konta lokalnego uwierzytelniania toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6a0da-185">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="6a0da-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="6a0da-186">*objectIdFromSession*</span></span> | <span data-ttu-id="6a0da-187">Parametr systemu hello domyślne sesji zarządzania dostawcy tooindicate który hello identyfikator obiektu ma zostały pobrane z sesji rejestracji Jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6a0da-187">Parameter provided by hello default session management provider tooindicate that hello object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="6a0da-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="6a0da-188">*isActiveMFASession*</span></span> | <span data-ttu-id="6a0da-189">Parametr dostarczanej przez hello MFA sesji zarządzania tooindicate, które użytkownik hello ma aktywnej sesji usługi MFA</span><span class="sxs-lookup"><span data-stu-id="6a0da-189">Parameter provided by hello MFA session management tooindicate that hello user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="6a0da-190">Dodatkowe oświadczenia (opcjonalnie), które mogą być zbierane</span><span class="sxs-lookup"><span data-stu-id="6a0da-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="6a0da-191">następujące Hello oświadczeń są dodatkowe oświadczenia, które mogą być zbierane od użytkowników hello przechowywanych w katalogu hello i wysyłane w tokenie hello.</span><span class="sxs-lookup"><span data-stu-id="6a0da-191">hello following claims are additional claims that can be collected from hello users, stored in hello directory, and sent in hello token.</span></span> <span data-ttu-id="6a0da-192">Zgodnie z opisem przed, dodatkowe oświadczenia mogą być dodawane toothis listy.</span><span class="sxs-lookup"><span data-stu-id="6a0da-192">As outlined before, additional claims can be added toothis list.</span></span>

| <span data-ttu-id="6a0da-193">Typ oświadczenia</span><span class="sxs-lookup"><span data-stu-id="6a0da-193">Claims type</span></span> | <span data-ttu-id="6a0da-194">Opis</span><span class="sxs-lookup"><span data-stu-id="6a0da-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="6a0da-195">*Imię*</span><span class="sxs-lookup"><span data-stu-id="6a0da-195">*givenName*</span></span> | <span data-ttu-id="6a0da-196">Imię użytkownika (znanej także jako nazwa pierwszej)</span><span class="sxs-lookup"><span data-stu-id="6a0da-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="6a0da-197">*nazwisko*</span><span class="sxs-lookup"><span data-stu-id="6a0da-197">*surname*</span></span> | <span data-ttu-id="6a0da-198">Nazwisko użytkownika (znanej także jako nazwa rodziny lub nazwisko)</span><span class="sxs-lookup"><span data-stu-id="6a0da-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="6a0da-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="6a0da-199">*Extension_picture*</span></span> | <span data-ttu-id="6a0da-200">Obraz użytkownika z społecznego</span><span class="sxs-lookup"><span data-stu-id="6a0da-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="6a0da-201">Przekształcenia oświadczeń</span><span class="sxs-lookup"><span data-stu-id="6a0da-201">Claim transformations</span></span>

<span data-ttu-id="6a0da-202">przekształcenia oświadczeń dostępnych Hello są wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="6a0da-202">hello available claim transformations are listed below.</span></span>

| <span data-ttu-id="6a0da-203">Przekształcania oświadczeń</span><span class="sxs-lookup"><span data-stu-id="6a0da-203">Claim transformation</span></span> | <span data-ttu-id="6a0da-204">Opis</span><span class="sxs-lookup"><span data-stu-id="6a0da-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="6a0da-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="6a0da-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="6a0da-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="6a0da-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="6a0da-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="6a0da-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="6a0da-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="6a0da-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="6a0da-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="6a0da-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="6a0da-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="6a0da-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="6a0da-211">Definicje zawartości</span><span class="sxs-lookup"><span data-stu-id="6a0da-211">Content definitions</span></span>

<span data-ttu-id="6a0da-212">W tej sekcji opisano hello definicje zawartości już zadeklarowany w hello *B2C_1A_base* zasad.</span><span class="sxs-lookup"><span data-stu-id="6a0da-212">This section describes hello content definitions already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="6a0da-213">Te definicje zawartości są podatne toobe odwołania, przesłonięcia i/lub rozszerzony zgodnie z potrzebami w własnych zasad, a także jak hello *B2C_1A_base_extensions* zasad.</span><span class="sxs-lookup"><span data-stu-id="6a0da-213">These content definitions are susceptible toobe referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="6a0da-214">Dostawcy oświadczeń</span><span class="sxs-lookup"><span data-stu-id="6a0da-214">Claims provider</span></span> | <span data-ttu-id="6a0da-215">Opis</span><span class="sxs-lookup"><span data-stu-id="6a0da-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="6a0da-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="6a0da-216">*Facebook*</span></span> | |
| <span data-ttu-id="6a0da-217">*Logowanie konta lokalnego*</span><span class="sxs-lookup"><span data-stu-id="6a0da-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="6a0da-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="6a0da-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="6a0da-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="6a0da-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="6a0da-220">*Samodzielnie potwierdzony*</span><span class="sxs-lookup"><span data-stu-id="6a0da-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="6a0da-221">*Konto lokalne*</span><span class="sxs-lookup"><span data-stu-id="6a0da-221">*Local Account*</span></span> | |
| <span data-ttu-id="6a0da-222">*Zarządzanie sesjami*</span><span class="sxs-lookup"><span data-stu-id="6a0da-222">*Session Management*</span></span> | |
| <span data-ttu-id="6a0da-223">*Aparat zasad Trustframework*</span><span class="sxs-lookup"><span data-stu-id="6a0da-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="6a0da-224">*TechnicalProfiles*</span><span class="sxs-lookup"><span data-stu-id="6a0da-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="6a0da-225">*Wystawca tokenu*</span><span class="sxs-lookup"><span data-stu-id="6a0da-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="6a0da-226">Profile techniczne</span><span class="sxs-lookup"><span data-stu-id="6a0da-226">Technical profiles</span></span>

<span data-ttu-id="6a0da-227">W tej sekcji przedstawiono hello profile techniczne już zadeklarowana dla dostawcy oświadczeń w hello *B2C_1A_base* zasad.</span><span class="sxs-lookup"><span data-stu-id="6a0da-227">This section depicts hello technical profiles already declared per claim provider in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="6a0da-228">Te profile techniczne są wrażliwych toobe dalsze odwołuje się do, przesłonięcia i/lub rozszerzony zgodnie z potrzebami w własnych zasad, a także jak hello *B2C_1A_base_extensions* zasad.</span><span class="sxs-lookup"><span data-stu-id="6a0da-228">These technical profiles are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="6a0da-229">Profile techniczne dla usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="6a0da-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="6a0da-230">Profil techniczne</span><span class="sxs-lookup"><span data-stu-id="6a0da-230">Technical profile</span></span> | <span data-ttu-id="6a0da-231">Opis</span><span class="sxs-lookup"><span data-stu-id="6a0da-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="6a0da-232">*Facebook OAUTH*</span><span class="sxs-lookup"><span data-stu-id="6a0da-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="6a0da-233">Profile techniczne dla lokalnego konta logowanie</span><span class="sxs-lookup"><span data-stu-id="6a0da-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="6a0da-234">Profil techniczne</span><span class="sxs-lookup"><span data-stu-id="6a0da-234">Technical profile</span></span> | <span data-ttu-id="6a0da-235">Opis</span><span class="sxs-lookup"><span data-stu-id="6a0da-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="6a0da-236">*Logowania nieinterakcyjnego*</span><span class="sxs-lookup"><span data-stu-id="6a0da-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="6a0da-237">Profile techniczne dla aplikacji Phone Factor</span><span class="sxs-lookup"><span data-stu-id="6a0da-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="6a0da-238">Profil techniczne</span><span class="sxs-lookup"><span data-stu-id="6a0da-238">Technical profile</span></span> | <span data-ttu-id="6a0da-239">Opis</span><span class="sxs-lookup"><span data-stu-id="6a0da-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="6a0da-240">*Dane wejściowe PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="6a0da-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="6a0da-241">*PhoneFactor InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="6a0da-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="6a0da-242">*Sprawdź PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="6a0da-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="6a0da-243">Profile techniczne dotyczące usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a0da-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="6a0da-244">Profil techniczne</span><span class="sxs-lookup"><span data-stu-id="6a0da-244">Technical profile</span></span> | <span data-ttu-id="6a0da-245">Opis</span><span class="sxs-lookup"><span data-stu-id="6a0da-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="6a0da-246">*Typowe usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="6a0da-246">*AAD-Common*</span></span> | <span data-ttu-id="6a0da-247">Profil techniczne uwzględnionych hello innych profilów techniczne AAD xxx</span><span class="sxs-lookup"><span data-stu-id="6a0da-247">Technical profile included by hello other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="6a0da-248">*UserWriteUsingAlternativeSecurityId usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="6a0da-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="6a0da-249">Profil techniczne dla logowania społecznościowych</span><span class="sxs-lookup"><span data-stu-id="6a0da-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="6a0da-250">*UserReadUsingAlternativeSecurityId usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="6a0da-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="6a0da-251">Profil techniczne dla logowania społecznościowych</span><span class="sxs-lookup"><span data-stu-id="6a0da-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="6a0da-252">*AAD-UserReadUsingAlternativeSecurityId-brak błędu*</span><span class="sxs-lookup"><span data-stu-id="6a0da-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="6a0da-253">Profil techniczne dla logowania społecznościowych</span><span class="sxs-lookup"><span data-stu-id="6a0da-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="6a0da-254">*UserWritePasswordUsingLogonEmail usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="6a0da-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="6a0da-255">Profil techniczne dla kont lokalnych</span><span class="sxs-lookup"><span data-stu-id="6a0da-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="6a0da-256">*UserReadUsingEmailAddress usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="6a0da-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="6a0da-257">Profil techniczne dla kont lokalnych</span><span class="sxs-lookup"><span data-stu-id="6a0da-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="6a0da-258">*UserWriteProfileUsingObjectId usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="6a0da-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="6a0da-259">Profil techniczne aktualizowania rekordu użytkownika przy użyciu objectId</span><span class="sxs-lookup"><span data-stu-id="6a0da-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="6a0da-260">*UserWritePhoneNumberUsingObjectId usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="6a0da-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="6a0da-261">Profil techniczne aktualizowania rekordu użytkownika przy użyciu objectId</span><span class="sxs-lookup"><span data-stu-id="6a0da-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="6a0da-262">*UserWritePasswordUsingObjectId usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="6a0da-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="6a0da-263">Profil techniczne aktualizowania rekordu użytkownika przy użyciu objectId</span><span class="sxs-lookup"><span data-stu-id="6a0da-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="6a0da-264">*UserReadUsingObjectId usługi AAD*</span><span class="sxs-lookup"><span data-stu-id="6a0da-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="6a0da-265">Techniczne profilu jest używane tooread danych po uwierzytelnia użytkownika</span><span class="sxs-lookup"><span data-stu-id="6a0da-265">Technical profile is used tooread data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="6a0da-266">Profile techniczne dla potwierdzone samoobsługowego</span><span class="sxs-lookup"><span data-stu-id="6a0da-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="6a0da-267">Profil techniczne</span><span class="sxs-lookup"><span data-stu-id="6a0da-267">Technical profile</span></span> | <span data-ttu-id="6a0da-268">Opis</span><span class="sxs-lookup"><span data-stu-id="6a0da-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="6a0da-269">*Społecznego SelfAsserted*</span><span class="sxs-lookup"><span data-stu-id="6a0da-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="6a0da-270">*SelfAsserted ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="6a0da-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="6a0da-271">Profile techniczne dla lokalnego konta</span><span class="sxs-lookup"><span data-stu-id="6a0da-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="6a0da-272">Profil techniczne</span><span class="sxs-lookup"><span data-stu-id="6a0da-272">Technical profile</span></span> | <span data-ttu-id="6a0da-273">Opis</span><span class="sxs-lookup"><span data-stu-id="6a0da-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="6a0da-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="6a0da-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="6a0da-275">Profile techniczne dla sesji zarządzania</span><span class="sxs-lookup"><span data-stu-id="6a0da-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="6a0da-276">Profil techniczne</span><span class="sxs-lookup"><span data-stu-id="6a0da-276">Technical profile</span></span> | <span data-ttu-id="6a0da-277">Opis</span><span class="sxs-lookup"><span data-stu-id="6a0da-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="6a0da-278">*Operacja SM*</span><span class="sxs-lookup"><span data-stu-id="6a0da-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="6a0da-279">*SM AAD*</span><span class="sxs-lookup"><span data-stu-id="6a0da-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="6a0da-280">*SM SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="6a0da-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="6a0da-281">Nazwa profilu jest są używane toodisambiguate AAD sesji między logowania się i zaloguj się</span><span class="sxs-lookup"><span data-stu-id="6a0da-281">Profile name is being used toodisambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="6a0da-282">*SM SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="6a0da-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="6a0da-283">*UWIERZYTELNIANIE WIELOSKŁADNIKOWE SM*</span><span class="sxs-lookup"><span data-stu-id="6a0da-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="6a0da-284">Profile techniczne dla TechnicalProfiles aparatu zasad Trustframework</span><span class="sxs-lookup"><span data-stu-id="6a0da-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="6a0da-285">Obecnie brak techniczne profilów są definiowane dla hello **TechnicalProfiles aparatu zasad Trustframework** dostawcy oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="6a0da-285">Currently, no technical profiles are defined for hello **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="6a0da-286">Profile techniczne dla wystawcy tokenów</span><span class="sxs-lookup"><span data-stu-id="6a0da-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="6a0da-287">Profil techniczne</span><span class="sxs-lookup"><span data-stu-id="6a0da-287">Technical profile</span></span> | <span data-ttu-id="6a0da-288">Opis</span><span class="sxs-lookup"><span data-stu-id="6a0da-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="6a0da-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="6a0da-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="6a0da-290">Podróże użytkownika</span><span class="sxs-lookup"><span data-stu-id="6a0da-290">User journeys</span></span>

<span data-ttu-id="6a0da-291">W tej sekcji przedstawiono podróże użytkownika hello już zadeklarowany w hello *B2C_1A_base* zasad.</span><span class="sxs-lookup"><span data-stu-id="6a0da-291">This section depicts hello user journeys already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="6a0da-292">Te podróże użytkownika są wrażliwych toobe dalsze odwołuje się do, przesłonięcia i/lub rozszerzony zgodnie z potrzebami w własnych zasad, a także jak hello *B2C_1A_base_extensions* zasad.</span><span class="sxs-lookup"><span data-stu-id="6a0da-292">These user journeys are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="6a0da-293">Przebieg użytkownika</span><span class="sxs-lookup"><span data-stu-id="6a0da-293">User journey</span></span> | <span data-ttu-id="6a0da-294">Opis</span><span class="sxs-lookup"><span data-stu-id="6a0da-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="6a0da-295">*Rejestracja*</span><span class="sxs-lookup"><span data-stu-id="6a0da-295">*SignUp*</span></span> | |
| <span data-ttu-id="6a0da-296">*Logowanie*</span><span class="sxs-lookup"><span data-stu-id="6a0da-296">*SignIn*</span></span> | |
| <span data-ttu-id="6a0da-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="6a0da-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="6a0da-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="6a0da-298">*EditProfile*</span></span> | |
| <span data-ttu-id="6a0da-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="6a0da-299">*PasswordReset*</span></span> | |
