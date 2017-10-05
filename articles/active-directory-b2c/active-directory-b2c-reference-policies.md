---
title: "Usługi Azure Active Directory B2C: Wbudowane zasady | Dokumentacja firmy Microsoft"
description: "Temat w ramach rozszerzalnych zasad usługi Azure Active Directory B2C i o sposobach tworzenia różnych typów zasad"
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: daad3af089afdf76b930053728bb11a5cf4c2a92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a><span data-ttu-id="3c498-103">Usługi Azure Active Directory B2C: Wbudowane zasady</span><span class="sxs-lookup"><span data-stu-id="3c498-103">Azure Active Directory B2C: Built-in policies</span></span>


<span data-ttu-id="3c498-104">Rozszerzona platforma zasad usługi Azure Active Directory (Azure AD) B2C jest siły podstawowe usługi.</span><span class="sxs-lookup"><span data-stu-id="3c498-104">The extensible policy framework of Azure Active Directory (Azure AD) B2C is the core strength of the service.</span></span> <span data-ttu-id="3c498-105">Zasady pełni opisano funkcje tożsamości konsumentów takich jak konta, logowania lub edytowanie profilu.</span><span class="sxs-lookup"><span data-stu-id="3c498-105">Policies fully describe consumer identity experiences such as sign-up, sign-in, or profile editing.</span></span> <span data-ttu-id="3c498-106">Na przykład zasad rejestracji umożliwia kontrolowanie zachowania, konfigurując następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="3c498-106">For instance, a sign-up policy allows you to control behaviors by configuring the following settings:</span></span>

* <span data-ttu-id="3c498-107">Typy kont (kont społecznościowych takimi jak Facebook) lub kont lokalnych, takie jak adresy e-mail, których klienci mogą korzystać zalogowania się do aplikacji</span><span class="sxs-lookup"><span data-stu-id="3c498-107">Account types (social accounts such as Facebook or local accounts such as email addresses) that consumers can use to sign up for the application</span></span>
* <span data-ttu-id="3c498-108">Atrybuty (na przykład imię, kod pocztowy i rozmiarze buta) mają być zbierane od konsumenta podczas tworzenia konta</span><span class="sxs-lookup"><span data-stu-id="3c498-108">Attributes (for example, first name, postal code, and shoe size) to be collected from the consumer during sign-up</span></span>
* <span data-ttu-id="3c498-109">Korzystanie z usługi Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3c498-109">Use of Azure Multi-Factor Authentication</span></span>
* <span data-ttu-id="3c498-110">Wygląd i działanie wszystkie strony</span><span class="sxs-lookup"><span data-stu-id="3c498-110">The look and feel of all sign-up pages</span></span>
* <span data-ttu-id="3c498-111">Informacje (które manifesty jako oświadczenia w tokenie) czy po otrzymaniu kiedy zasad, uruchom zakończenie</span><span class="sxs-lookup"><span data-stu-id="3c498-111">Information (which manifests as claims in a token) that the application receives when the policy run finishes</span></span>

<span data-ttu-id="3c498-112">Można utworzyć wiele zasad o różnych typach w dzierżawie i używać ich w aplikacji, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="3c498-112">You can create multiple policies of different types in your tenant and use them in your applications as needed.</span></span> <span data-ttu-id="3c498-113">Zasady mogą być ponownie używane w aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="3c498-113">Policies can be reused across applications.</span></span> <span data-ttu-id="3c498-114">Tego rodzaju elastyczności umożliwia deweloperom definiowanie i modyfikowanie środowiska tożsamości użytkownika z minimalnym lub Brak zmian do ich kodu.</span><span class="sxs-lookup"><span data-stu-id="3c498-114">This flexibility enables developers to define and modify consumer identity experiences with minimal or no changes to their code.</span></span>

<span data-ttu-id="3c498-115">Zasady są dostępne do użycia przy użyciu interfejsu dewelopera proste.</span><span class="sxs-lookup"><span data-stu-id="3c498-115">Policies are available for use via a simple developer interface.</span></span> <span data-ttu-id="3c498-116">Wyzwala zasady przy użyciu standardowego żądania uwierzytelniania HTTP (przekazywanie parametru zasad w żądaniu) i otrzymuje token dostosowane odpowiedzi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c498-116">Your application triggers a policy by using a standard HTTP authentication request (passing a policy parameter in the request) and receives a customized token as response.</span></span> <span data-ttu-id="3c498-117">Jedyną różnicą między żądań, które wywołują zasad logowania i żądań, które wywołują zasad rejestracji jest na przykład nazwę zasad, która jest używana w "p" parametru ciągu zapytania:</span><span class="sxs-lookup"><span data-stu-id="3c498-117">For example, the only difference between requests that invoke a sign-up policy and requests that invoke a sign-in policy is the policy name that's used in the "p" query string parameter:</span></span>

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

<span data-ttu-id="3c498-118">Aby uzyskać więcej informacji na temat framework zasad, zobacz [ten wpis w blogu dotyczące usługi Azure AD B2C na Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c498-118">For more information about the policy framework, see [this blog post about Azure AD B2C on the Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span></span>

## <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="3c498-119">Tworzenie zasad rejestracji i logowania</span><span class="sxs-lookup"><span data-stu-id="3c498-119">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="3c498-120">Ta zasada obsługuje zarówno konsumenta rejestracji i logowania, korzystając z pojedynczą konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="3c498-120">This policy handles both consumer sign-up & sign-in experiences with a single configuration.</span></span> <span data-ttu-id="3c498-121">Konsumenci są doprowadziło do prawej ścieżki (rejestracji lub logowania), w zależności od kontekstu.</span><span class="sxs-lookup"><span data-stu-id="3c498-121">Consumers are led down the right path (sign-up or sign-in) depending on the context.</span></span> <span data-ttu-id="3c498-122">Omówiono także zawartość tokenów, które otrzymają aplikacji po pomyślnej napędza rejestracje lub logowania.  Przykład kodu dla zasad rejestracji i logowania jest [dostępne tutaj](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="3c498-122">It also describes the contents of tokens that the application will receive upon successful sign-ups or sign-ins.  A code sample for the sign-up or sign-in policy is [available here](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>  <span data-ttu-id="3c498-123">Jest zalecane w przypadku użycia tej zasady protokołu zasad rejestracji i logowania zasad.</span><span class="sxs-lookup"><span data-stu-id="3c498-123">It is recommened that you use this policy over a sign-up policy and sign-in policy.</span></span>  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a><span data-ttu-id="3c498-124">Tworzenie zasad rejestracji</span><span class="sxs-lookup"><span data-stu-id="3c498-124">Create a sign-up policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a><span data-ttu-id="3c498-125">Tworzenie zasad logowania</span><span class="sxs-lookup"><span data-stu-id="3c498-125">Create a sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a><span data-ttu-id="3c498-126">Utwórz profil edytowanie zasad</span><span class="sxs-lookup"><span data-stu-id="3c498-126">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a><span data-ttu-id="3c498-127">Utwórz zasady resetowania hasła</span><span class="sxs-lookup"><span data-stu-id="3c498-127">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a><span data-ttu-id="3c498-128">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="3c498-128">Frequently asked questions</span></span>

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a><span data-ttu-id="3c498-129">Jak połączyć zasady rejestracji lub logowania za pomocą zasad resetowania hasła</span><span class="sxs-lookup"><span data-stu-id="3c498-129">How do I link a sign-up or sign-in policy with a password reset policy?</span></span>
<span data-ttu-id="3c498-130">Podczas tworzenia zasady rejestracji i logowania (za pomocą kont lokalnych), zobacz **nie pamiętam hasła?** łącza na pierwszej stronie środowisko.</span><span class="sxs-lookup"><span data-stu-id="3c498-130">When you create a sign-up or sign-in policy (with local accounts), you see a **Forgot password?** link on the first page of the experience.</span></span> <span data-ttu-id="3c498-131">Kliknięcie tego łącza nie automatycznie wyzwalacza hasła zasady resetowania.</span><span class="sxs-lookup"><span data-stu-id="3c498-131">Clicking this link doesn't automatically trigger a password reset policy.</span></span> 

<span data-ttu-id="3c498-132">Zamiast tego kodu błędu  **`AADB2C90118`**  jest zwracana do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c498-132">Instead, the error code **`AADB2C90118`** is returned to your app.</span></span> <span data-ttu-id="3c498-133">Twoja aplikacja powinna obsługiwać tego kodu błędu za pomocą zasad resetowania hasła określone.</span><span class="sxs-lookup"><span data-stu-id="3c498-133">Your app needs to handle this error code by invoking a specific password reset policy.</span></span> <span data-ttu-id="3c498-134">Aby uzyskać więcej informacji, zobacz [przykład przedstawiający metodę łączenia zasad](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span><span class="sxs-lookup"><span data-stu-id="3c498-134">For more information, see a [sample that demonstrates the approach of linking policies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span></span>

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a><span data-ttu-id="3c498-135">Należy użyć zasad rejestracji i logowania lub zasad rejestracji i logowania zasady?</span><span class="sxs-lookup"><span data-stu-id="3c498-135">Should I use a sign-up or sign-in policy or a sign-up policy and a sign-in policy?</span></span>
<span data-ttu-id="3c498-136">Zalecane jest użycie zasad rejestracji lub logowania za pośrednictwem zasad rejestracji i logowania zasad.</span><span class="sxs-lookup"><span data-stu-id="3c498-136">We recommend that you use a sign-up or sign-in policy over a sign-up policy and a sign-in policy.</span></span>  

<span data-ttu-id="3c498-137">Zasady rejestracji i logowania ma więcej możliwości niż zasad logowania.</span><span class="sxs-lookup"><span data-stu-id="3c498-137">The sign-up or sign-in policy has more capabilities than the sign-in policy.</span></span> <span data-ttu-id="3c498-138">Również umożliwia dostosowywanie interfejsu użytkownika strony i ma lepszą obsługę lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="3c498-138">It also enables you to use page UI customization and has better support for localization.</span></span> 

<span data-ttu-id="3c498-139">Nie należy do zlokalizowania zasad tylko potrzeby znakowania możliwości personalizacji i mają hasła, zaleca się zasad logowania resetowania wbudowanych.</span><span class="sxs-lookup"><span data-stu-id="3c498-139">The sign-in policy is recommended if you don't need to localize your policies, only need minor customization capabilities for branding, and want password reset built into it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c498-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3c498-140">Next steps</span></span>
* [<span data-ttu-id="3c498-141">Token sesji i konfiguracji rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3c498-141">Token, session, and single sign-on configuration</span></span>](active-directory-b2c-token-session-sso.md)
* [<span data-ttu-id="3c498-142">Wyłączyć weryfikację wiadomości e-mail podczas tworzenia konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="3c498-142">Disable email verification during consumer sign-up</span></span>](active-directory-b2c-reference-disable-ev.md)

