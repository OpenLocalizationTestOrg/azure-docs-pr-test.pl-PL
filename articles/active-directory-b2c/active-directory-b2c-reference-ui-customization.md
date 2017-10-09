---
title: "Dostosowywanie interfejsu użytkownika — usługi Azure AD B2C | Dokumentacja firmy Microsoft"
description: "Temat dotyczący hello funkcje dostosowywania interfejsu użytkownika w usłudze Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 99f5a391-5328-471d-a15c-a2fafafe233d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 04f8c5f1277f8d4409cd10971d22a0ebd2024785
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-customize-hello-azure-ad-b2c-user-interface-ui"></a><span data-ttu-id="beefc-103">Usługa Azure Active Directory B2C: Dostosowywanie hello Azure AD B2C interfejsu użytkownika (UI)</span><span class="sxs-lookup"><span data-stu-id="beefc-103">Azure Active Directory B2C: Customize hello Azure AD B2C user interface (UI)</span></span>

<span data-ttu-id="beefc-104">Środowisko użytkownika jest podstawowym w aplikacji klientów.</span><span class="sxs-lookup"><span data-stu-id="beefc-104">User experience is paramount in a customer facing application.</span></span>  <span data-ttu-id="beefc-105">Zwiększ bazę swoich klientów przez obsługuje tworzenie użytkownika, korzystając z hello wygląd i działanie oznakowanie.</span><span class="sxs-lookup"><span data-stu-id="beefc-105">Grow your customer base by crafting user experiences with hello look and feel of your brand.</span></span> <span data-ttu-id="beefc-106">Usługa Azure Active Directory B2C (Azure AD B2C) umożliwia dostosowanie edycji profilu rejestracji, logowania, i stron z formantem pikseli idealny resetowania hasła.</span><span class="sxs-lookup"><span data-stu-id="beefc-106">Azure Active Directory B2C (Azure AD B2C) lets you customize sign-up, sign-in, profile editing, and password reset pages with pixel-perfect control.</span></span>

> [!NOTE]
> <span data-ttu-id="beefc-107">Witaj strony interfejsu użytkownika funkcji dostosowanie opisane w tym artykule nie ma zastosowania, toohello tylko zasad logowania, jego towarzyszący stronę resetowania hasła i weryfikacyjnych wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="beefc-107">hello page UI customization feature described in this article does not apply toohello sign-in only policy, its accompanying password reset page, and verification emails.</span></span>  <span data-ttu-id="beefc-108">Te funkcje korzystają hello [firmowe funkcji](../active-directory/active-directory-add-company-branding.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="beefc-108">These features use hello [company branding feature](../active-directory/active-directory-add-company-branding.md) instead.</span></span>
>

<span data-ttu-id="beefc-109">W tym artykule omówiono hello następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="beefc-109">This article covers hello following topics:</span></span>

* <span data-ttu-id="beefc-110">Witaj funkcji dostosowywania interfejsu użytkownika strony.</span><span class="sxs-lookup"><span data-stu-id="beefc-110">hello page UI customization feature.</span></span>
* <span data-ttu-id="beefc-111">Narzędzie do przekazywania tooAzure zawartości HTML magazynu obiektów Blob do użycia z funkcją dostosowania interfejsu użytkownika strony hello.</span><span class="sxs-lookup"><span data-stu-id="beefc-111">A tool for uploading HTML content tooAzure Blob Storage for use with hello page UI customization feature.</span></span>
* <span data-ttu-id="beefc-112">Witaj elementów interfejsu użytkownika używanych przez usługę Azure AD B2C, który można dostosować przy użyciu kaskadowych arkuszy stylów (CSS).</span><span class="sxs-lookup"><span data-stu-id="beefc-112">hello UI elements used by Azure AD B2C that you can customize using Cascading Style Sheets (CSS).</span></span>
* <span data-ttu-id="beefc-113">Najlepsze rozwiązania podczas wykonywania tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="beefc-113">Best practices when exercising this feature.</span></span>

## <a name="hello-page-ui-customization-feature"></a><span data-ttu-id="beefc-114">Funkcja dostosowania interfejsu użytkownika strony Hello</span><span class="sxs-lookup"><span data-stu-id="beefc-114">hello page UI customization feature</span></span>

<span data-ttu-id="beefc-115">Można dostosować hello wyglądu i działania klienta hasła rejestrację, logowanie, resetowania i edytowanie profilu strony (konfigurując [zasady](active-directory-b2c-reference-policies.md)).</span><span class="sxs-lookup"><span data-stu-id="beefc-115">You can customize hello look and feel of customer sign-up, sign-in, password reset, and profile-editing pages (by configuring [policies](active-directory-b2c-reference-policies.md)).</span></span> <span data-ttu-id="beefc-116">Klienci uzyskać bezproblemowe podczas nawigowania między aplikacji i strony obsługiwanych przez usługę Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="beefc-116">Your customers get a seamless experience when navigating between your application and pages served by Azure AD B2C.</span></span>

<span data-ttu-id="beefc-117">W przeciwieństwie do innych usług, gdzie opcji interfejsu użytkownika, używa usługi Azure AD B2C prosty i nowoczesnych rozwiązań tooUI dostosowywania.</span><span class="sxs-lookup"><span data-stu-id="beefc-117">Unlike other services where UI options, Azure AD B2C uses a simple and modern approach tooUI customization.</span></span>

<span data-ttu-id="beefc-118">Oto jak to działa: usługi Azure AD B2C kod w przeglądarce klienta, korzysta z podejścia nowoczesnych o nazwie [udostępniania zasobów między źródłami (CORS)](http://www.w3.org/TR/cors/).</span><span class="sxs-lookup"><span data-stu-id="beefc-118">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span>  <span data-ttu-id="beefc-119">W czasie wykonywania zawartość została załadowana z adresu URL, który określisz w zasadach.</span><span class="sxs-lookup"><span data-stu-id="beefc-119">At run-time, content is loaded from a URL that you specify in a policy.</span></span> <span data-ttu-id="beefc-120">Możesz określić inny adres URL do różnych stron.</span><span class="sxs-lookup"><span data-stu-id="beefc-120">You can specify different URLs for different pages.</span></span> <span data-ttu-id="beefc-121">Po zawartości załadowana z adresu URL jest scalany z fragment kodu HTML z usługi Azure AD B2C, strona hello jest wyświetlanych tooyour klienta.</span><span class="sxs-lookup"><span data-stu-id="beefc-121">After content loaded from your URL is merged with an HTML fragment inserted from Azure AD B2C, hello page is displayed tooyour customer.</span></span> <span data-ttu-id="beefc-122">Toodo wystarczy:</span><span class="sxs-lookup"><span data-stu-id="beefc-122">All you need toodo is:</span></span>

1. <span data-ttu-id="beefc-123">Tworzenie zawartości z pustą poprawnie sformułowanym HTML5 `<div id="api"></div>` element znajduje się gdzieś w hello `<body>`.</span><span class="sxs-lookup"><span data-stu-id="beefc-123">Create well-formed HTML5 content with an empty `<div id="api"></div>` element located somewhere in hello `<body>`.</span></span> <span data-ttu-id="beefc-124">Znaczniki tego elementu gdzie jest wstawiany hello zawartości usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="beefc-124">This element marks where hello Azure AD B2C content is inserted.</span></span>
1. <span data-ttu-id="beefc-125">Udostępnić zawartość w punkcie końcowym HTTPS (z CORS dozwolone).</span><span class="sxs-lookup"><span data-stu-id="beefc-125">Host your content on an HTTPS endpoint (with CORS allowed).</span></span> <span data-ttu-id="beefc-126">Należy pamiętać, zarówno GET i opcje żądania metody musi być włączona podczas konfigurowania CORS.</span><span class="sxs-lookup"><span data-stu-id="beefc-126">Note both GET and OPTIONS request methods must be enabled when configuring CORS.</span></span>
1. <span data-ttu-id="beefc-127">Użyj CSS toostyle hello elementy interfejsu użytkownika wstawia usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="beefc-127">Use CSS toostyle hello UI elements that Azure AD B2C inserts.</span></span>

### <a name="a-basic-example-of-customized-html"></a><span data-ttu-id="beefc-128">Podstawowy przykład dostosowany HTML</span><span class="sxs-lookup"><span data-stu-id="beefc-128">A basic example of customized HTML</span></span>

<span data-ttu-id="beefc-129">Poniższy przykład Hello jest najbardziej podstawowa zawartość HTML hello, których można używać tootest tej możliwości.</span><span class="sxs-lookup"><span data-stu-id="beefc-129">hello following example is hello most basic HTML content that you can use tootest this capability.</span></span> <span data-ttu-id="beefc-130">Użyj hello [Narzędzie Pomocnik](active-directory-b2c-reference-ui-customization-helper-tool.md) tooupload i skonfigurować tę zawartość w magazynie obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="beefc-130">Use hello [helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) tooupload and configure this content on your Azure Blob storage.</span></span> <span data-ttu-id="beefc-131">Następnie można sprawdzić, czy hello podstawowe, stylized przycisków i pola formularza na każdej stronie są wyświetlane i funkcjonalności.</span><span class="sxs-lookup"><span data-stu-id="beefc-131">You can then verify that hello basic, non-stylized buttons & form fields on each page are displayed and functional.</span></span>

```HTML
<!DOCTYPE html>
<html>
    <head>
        <title>!Add your title here!</title>
    </head>
    <body>
        <div id="api"></div>   <!-- Leave this element empty because Azure AD B2C will insert content here. -->
    </body>
</html>
```

## <a name="test-out-hello-ui-customization-feature"></a><span data-ttu-id="beefc-132">Przetestowanie funkcji dostosowanie hello interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="beefc-132">Test out hello UI customization feature</span></span>

<span data-ttu-id="beefc-133">Chcesz tootry limit funkcji dostosowanie hello interfejsu użytkownika za pomocą naszej próbki zawartość HTML i CSS?</span><span class="sxs-lookup"><span data-stu-id="beefc-133">Want tootry out hello UI customization feature by using our sample HTML and CSS content?</span></span>  <span data-ttu-id="beefc-134">Udostępniliśmy [Narzędzie Pomocnik](active-directory-b2c-reference-ui-customization-helper-tool.md) który przekazuje i konfiguruje przykładowej zawartości w magazynie obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="beefc-134">We've provided you [a helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures sample content on your Azure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="beefc-135">Można udostępnić zawartość interfejsu użytkownika dowolnym: na serwerach sieci web, CDN, usług AWS S3, systemy udostępniania plików itp. Tak długo, jak zawartość hello jest udostępniana w publicznie dostępnych punkt końcowy HTTPS z włączonym mechanizmem CORS, jesteś toogo dobra.</span><span class="sxs-lookup"><span data-stu-id="beefc-135">You can host your UI content anywhere: on web servers, CDNs, AWS S3, file sharing systems, etc. As long as hello content is hosted on a publicly available HTTPS endpoint with CORS enabled, you are good toogo.</span></span> <span data-ttu-id="beefc-136">Użyto magazynu obiektów Blob platformy Azure tylko w celach ilustracyjnych.</span><span class="sxs-lookup"><span data-stu-id="beefc-136">We are using Azure Blob storage for illustrative purposes only.</span></span>
>

## <a name="hello-ui-fragments-embedded-by-azure-ad-b2c"></a><span data-ttu-id="beefc-137">Witaj osadzone przez usługę Azure AD B2C fragmenty interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="beefc-137">hello UI fragments embedded by Azure AD B2C</span></span>

<span data-ttu-id="beefc-138">Witaj poniższe sekcje zawierają listę fragmenty hello HTML5, które usługi Azure AD B2C scala hello `<div id="api"></div>` element znajduje się w treści.</span><span class="sxs-lookup"><span data-stu-id="beefc-138">hello following sections list hello HTML5 fragments that Azure AD B2C merges into hello `<div id="api"></div>` element located in your content.</span></span> <span data-ttu-id="beefc-139">**Nie wstawiono tych fragmentów w zawartości HTML 5.**</span><span class="sxs-lookup"><span data-stu-id="beefc-139">**Do not insert these fragments in your HTML 5 content.**</span></span> <span data-ttu-id="beefc-140">Hello usługi Azure AD B2C wstawia je w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="beefc-140">hello Azure AD B2C service inserts them in at run-time.</span></span> <span data-ttu-id="beefc-141">Użyj tych fragmentów jako odwołanie podczas projektowania własnych kaskadowych arkuszy stylów (CSS).</span><span class="sxs-lookup"><span data-stu-id="beefc-141">Use these fragments as a reference when designing your own Cascading Style Sheets (CSS).</span></span>

### <a name="fragment-inserted-into-hello-identity-provider-selection-page"></a><span data-ttu-id="beefc-142">Fragment do hello "Strona wyboru dostawcy tożsamości"</span><span class="sxs-lookup"><span data-stu-id="beefc-142">Fragment inserted into hello "Identity provider selection page"</span></span>

<span data-ttu-id="beefc-143">Ta strona zawiera listę dostawców, którzy hello użytkownika można wybrać podczas tworzenia konta lub Logowanie tożsamości.</span><span class="sxs-lookup"><span data-stu-id="beefc-143">This page contains a list of identity providers that hello user can choose from during sign-up or sign-in.</span></span> <span data-ttu-id="beefc-144">Przyciski te obejmują dostawców tożsamości społecznościowych, takich jak Facebook i Google + lub kont lokalnych (w oparciu nazwa użytkownika lub adres e-mail).</span><span class="sxs-lookup"><span data-stu-id="beefc-144">These buttons include social identity providers such as Facebook and Google+, or local accounts (based on email address or user name).</span></span>

```HTML
<div id="api" data-name="IdpSelections">
    <div class="intro">
         <p>Sign up</p>
    </div>

    <div>
        <ul>
            <li>
                <button class="accountButton" id="FacebookExchange">Facebook</button>
            </li>
            <li>
                <button class="accountButton" id="GoogleExchange">Google+</button>
            </li>
            <li>
                <button class="accountButton" id="SignUpWithLogonEmailExchange">Email</button>
            </li>
        </ul>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-local-account-sign-up-page"></a><span data-ttu-id="beefc-145">Fragment do hello "stronę tworzenia konta lokalnego konta"</span><span class="sxs-lookup"><span data-stu-id="beefc-145">Fragment inserted into hello "Local account sign-up page"</span></span>

<span data-ttu-id="beefc-146">Ta strona zawiera formularza dla lokalnego konta tworzenia konta na podstawie adresu e-mail lub nazwę użytkownika.</span><span class="sxs-lookup"><span data-stu-id="beefc-146">This page contains a form for local account sign-up based on an email address or a user name.</span></span> <span data-ttu-id="beefc-147">Formularz Hello może zawierać różne kontrolki wejściowe, takich jak pola do wprowadzania tekstu, pole wprowadzania hasła przycisk radiowy, jednokrotnym zaznaczeniem pola listy rozwijanej i pól wyboru wielokrotnego wyboru.</span><span class="sxs-lookup"><span data-stu-id="beefc-147">hello form can contain different input controls such as text input box, password entry box, radio button, single-select drop-down boxes, and multi-select check boxes.</span></span>

```HTML
<div id="api" data-name="SelfAsserted">
    <div class="intro">
        <p>Create your account by providing hello following details</p>
    </div>

    <div id="attributeVerification">
        <div class="errorText" id="passwordEntryMismatch" style="display: none;">hello password entry fields do not match. Please enter hello same password in both fields and try again.</div>
        <div class="errorText" id="requiredFieldMissing" style="display: none;">A required field is missing. Please fill out all required fields and try again.</div>
        <div class="errorText" id="fieldIncorrect" style="display: none;">One or more fields are filled out incorrectly. Please check your entries and try again.</div>
        <div class="errorText" id="claimVerificationServerError" style="display: none;"></div>
        <div class="attr" id="attributeList">
            <ul>
                <li>
                    <div class="attrEntry validate">
                        <div>
                            <div class="verificationInfoText" id="email_intro" style="display: inline;">Verification is necessary. Please click Send button.</div>
                            <div class="verificationInfoText" id="email_info" style="display:none">Verification code has been sent tooyour inbox. Please copy it toohello input box below.</div>
                            <div class="verificationSuccessText" id="email_success" style="display:none">E-mail address verified. You can now continue.</div>
                            <div class="verificationErrorText" id="email_fail_retry" style="display:none">Incorrect code, try again.</div>
                            <div class="verificationErrorText" id="email_fail_no_retry" style="display:none">Exceeded number of retries you need toosend new code.</div>
                            <div class="verificationErrorText" id="email_fail_server" style="display:none">Server error, please try again</div>
                            <div class="verificationErrorText" id="email_incorrect_format" style="display:none">Incorect format.</div>
                        </div>

                    <div class="helpText show">This information is required</div>
                        <label>Email</label>
                        <input id="email" class="textInput" type="text" placeholder="Email" required="" autofocus=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Email address that can be used toocontact you.');" class="tiny">What is this?</a>

                    <div class="buttons verify" claim_id="email">
                        <div id="email_ver_wait" class="working" style="display: none;"></div>
                            <label id="email_ver_input_label" for="email_ver_input" style="display: none;">Verification code</label>
                            <input id="email_ver_input" type="text" placeholder="Verification code" style="display:none">
                            <button id="email_ver_but_send" class="sendButton" type="button" style="display: inline;">Send verification code</button>
                            <button id="email_ver_but_verify" class="verifyButton" type="button" style="display:none">Verify code</button>
                            <button id="email_ver_but_resend" class="sendButton" type="button" style="display:none">Send new code</button>
                            <button id="email_ver_but_edit" class="editButton" type="button" style="display:none">Change e-mail</button>
                            <button id="email_ver_but_default" class="defaultButton" type="button" style="display:none">Default</button>
                        </div>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ " ( ) ; .This information is required</div>
                        <label>Enter password</label>
                        <input id="password" class="textInput" type="password" placeholder="Enter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title="8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ &quot; ( ) ; ." required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Enter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"> This information is required</div>
                        <label>Reenter password</label>
                        <input id="reenterPassword" class="textInput" type="password" placeholder="Reenter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title=" " required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Reenter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Name</label>
                        <input id="displayName" class="textInput" type="text" placeholder="Name" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your display name.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Gender</label>
                        <input id="extension_Gender_F" name="extension_Gender" type="radio" value="F" autofocus="">
                        <label for="extension_Gender_F">Female</label>
                        <input id="extension_Gender_M" name="extension_Gender" type="radio" value="M">
                        <label for="extension_Gender_M">Male</label>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Loyalty number</label>
                        <input id="extension_MemNum" class="textInput" type="text" placeholder="Loyalty number"><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Membership number');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>State</label>
                        <select class="dropdown_single" id="state">
                            <option style="display:none" disabled="disabled" value="placeholder" selected="">State</option>
                            <option value="WA">Washington</option>
                            <option value="NY">New York</option>
                            <option value="CA">California</option>
                        </select>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your residential state or province.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Zip code</label>
                        <input id="postalCode" class="textInput" type="text" placeholder="Zip code" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('hello postal code of your address.');" class="tiny">What is this?</a>
                    </div>
                </li>
            </ul>
        </div>
        <div class="buttons"> <button id="continue" disabled="">Create</button> <button id="cancel">Cancel</button></div>
    </div>
    <div class="verifying-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="verifying_blurb"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-social-account-sign-up-page"></a><span data-ttu-id="beefc-148">Fragment wstawione do Witaj, "" społecznego account stronę tworzenia konta"</span><span class="sxs-lookup"><span data-stu-id="beefc-148">Fragment inserted into hello ""Social account sign-up page"</span></span>

<span data-ttu-id="beefc-149">Ta strona może pojawić się podczas rejestracji przy użyciu istniejącego konta od dostawcy tożsamości społecznościowych, takich jak Facebook lub Google +.</span><span class="sxs-lookup"><span data-stu-id="beefc-149">This page may appear when signing up using an existing account from a social identity provider such as Facebook or Google+.</span></span>  <span data-ttu-id="beefc-150">Jest używany podczas dodatkowe informacje muszą zostać pobrane od użytkownika końcowego hello za pomocą formularza tworzenia konta.</span><span class="sxs-lookup"><span data-stu-id="beefc-150">It is used when additional information must be collected from hello end user using a sign-up form.</span></span> <span data-ttu-id="beefc-151">Ta strona jest podobne toohello konta lokalnego stronę tworzenia konta (przedstawione w poprzedniej sekcji hello) z wyjątkiem hello pola wprowadzania hasła hello.</span><span class="sxs-lookup"><span data-stu-id="beefc-151">This page is similar toohello local account sign-up page (shown in hello previous section) with hello exception of hello password entry fields.</span></span>

### <a name="fragment-inserted-into-hello-unified-sign-up-or-sign-in-page"></a><span data-ttu-id="beefc-152">Fragment wstawione do hello "Stronę tworzenia konta lub logowanie Unified"</span><span class="sxs-lookup"><span data-stu-id="beefc-152">Fragment inserted into hello "Unified sign-up or sign-in page"</span></span>

<span data-ttu-id="beefc-153">Ta strona obsługuje zarówno rejestracji i logowania klientów, którzy mogą używać dostawców tożsamości społecznościowych, takich jak Facebook lub Google + lub kont lokalnych.</span><span class="sxs-lookup"><span data-stu-id="beefc-153">This page handles both sign-up & sign-in of customers, who can use social identity providers such as Facebook or Google+, or local accounts.</span></span>

```HTML
<div id="api" data-name="Unified">
        <div class="social" role="form">
               <div class="intro">
                       <h2>Sign in with your social account</h2>
               </div>
               <div class="options">
                       <div><button class="accountButton firstButton" id="MicrosoftAccountExchange" tabindex="1">msa</button></div>
                       <div><button class="accountButton" id="FacebookExchange" tabindex="1">fb</button></div>
               </div>
        </div>
        <div class="divider">
               <h2>OR</h2>
        </div>
        <div class="localAccount" role="form">
               <div class="intro">
                       <h2>Sign in with your existing account</h2>
               </div>
               <div class="error pageLevel" aria-hidden="true" style="display: none;">
                       <p role="alert"></p>
               </div>
               <div class="entry">
                       <div class="entry-item">
                               <label for="logonIdentifier">Email Address</label> 
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="email" id="logonIdentifier" name="LogonIdentifier" pattern="^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$" placeholder="LogonIdentifier" value="" tabindex="1">
                       </div>
                       <div class="entry-item">
                               <div class="password-label"> <label for="password">Password</label><a id="forgotPassword" tabindex="2">Forgot your password?</a></div>
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="password" id="password" name="Password" placeholder="Password" tabindex="1">
                       </div>
                       <div class="working"></div>
                       <div class="buttons"> <button id="next" tabindex="1">Sign in</button> </div>
               </div>
               <div class="divider">
                       <h2>OR</h2>
               </div>
               <div class="create">
                       <p>Don't have an account?<a id="createAccount" tabindex="1">Sign up now</a> </p>
               </div>
        </div>
</div>
```

### <a name="fragment-inserted-into-hello-multi-factor-authentication-page"></a><span data-ttu-id="beefc-154">Fragment wstawione do hello "page usługi Multi-Factor authentication"</span><span class="sxs-lookup"><span data-stu-id="beefc-154">Fragment inserted into hello "Multi-factor authentication page"</span></span>

<span data-ttu-id="beefc-155">Na tej stronie użytkowników można sprawdzić ich numery telefonów (przy użyciu tekstowych lub głosowych) podczas tworzenia konta lub logowania.</span><span class="sxs-lookup"><span data-stu-id="beefc-155">On this page, users can verify their phone numbers (using text or voice) during sign-up or sign-in.</span></span>

```HTML
<div id="api" data-name="Phonefactor">
    <div id="phonefactor_initial">
        <div class="intro">
            <p>Enter a number below that we can send a code via SMS or phone tooauthenticate you.</p>
        </div>
        <div class="errorText" id="errorMessage" style="display:none"></div>
        <div class="phoneEntry" id="phoneEntry">
            <div class="phoneNumber">
                <select id="countryCode" style="display:inline-block">
                    <option value="+93">Afghanistan (+93)</option>
                    <!-- Not all country codes listed -->
                    <option value="+44">United Kingdom (+44)</option>
                    <option value="+1" selected="">United States (+1)</option>
                    <!-- Not all country codes listed -->
                </select>
            </div>
            <div class="phoneNumber">
                <input type="text" id="localNumber" style="display:inline-block" placeholder="Phone number">
            </div>
        </div>
        <div id="codeVerification" style="display:none">
            <div>
                <p>Enter your verification code below, or <button id="retryCode" class="textButton">send a new code</button></p>
                <input type="text" id="verificationCode" placeholder="Verification code">
            </div>
        </div>
        <div class="buttons">
            <button id="verifyCode" class="sendInitialCodeButton">Send Code</button>
            <button id="verifyPhone" style="display:inline-block">Call Me</button>
            <button id="cancel" style="display:inline-block">Cancel</button>
        </div>
    </div>
    <div class="dialing-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="dialing_blurb"></div><div id="dialing_number"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-error-page"></a><span data-ttu-id="beefc-156">Fragment do hello "" strony błędu"</span><span class="sxs-lookup"><span data-stu-id="beefc-156">Fragment inserted into hello ""Error page"</span></span>

```HTML
<div id="api" class="error-page-content" data-name="GlobalException">
    <h2>Sorry, but we're having trouble signing you in.</h2>
    <div class="error-page-help">We track these errors automatically, but if hello problem persists feel free toocontact us. In hello meantime, please try again.</div>
    <div class="error-page-messagedetails">Your administrator hasn't provided any contact details.</div>
    <div class="error-page-messagedetails">
        <div class="error-page-correlationid">Correlation ID:1c4f0397-c6e4-4afe-bf74-42f488f2f15f</div>
        <div>Timestamp:2015-09-14 23:22:35Z</div>
        <div class="error-page-detail">AADB2C90065: A B2C client-side error 'Access is denied.' has occurred requesting hello remote resource.</div>
    </div>
</div>
```

## <a name="localizing-your-html-content"></a><span data-ttu-id="beefc-157">Lokalizacja zawartości HTML</span><span class="sxs-lookup"><span data-stu-id="beefc-157">Localizing your HTML content</span></span>

<span data-ttu-id="beefc-158">Można lokalizować zawartość HTML, włączając ["Języka dostosowania"](active-directory-b2c-reference-language-customization.md).</span><span class="sxs-lookup"><span data-stu-id="beefc-158">You can localize your HTML content by turning on ['Language customization'](active-directory-b2c-reference-language-customization.md).</span></span>  <span data-ttu-id="beefc-159">Włączenie tej funkcji umożliwia usłudze Azure AD B2C tooforward hello Open ID Connect parametru `ui-locales`, tooyour punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="beefc-159">Enabling this feature allows Azure AD B2C tooforward hello Open ID Connect parameter, `ui-locales`, tooyour endpoint.</span></span>  <span data-ttu-id="beefc-160">Serwer zawartości, można użyć tego parametru stron HTML tooprovide dostosowane, które są specyficzne dla języka.</span><span class="sxs-lookup"><span data-stu-id="beefc-160">Your content server can use this parameter tooprovide customized HTML pages that are language-specific.</span></span>

## <a name="things-tooremember-when-building-your-own-content"></a><span data-ttu-id="beefc-161">Tooremember czynności podczas tworzenia własnych zawartości</span><span class="sxs-lookup"><span data-stu-id="beefc-161">Things tooremember when building your own content</span></span>

<span data-ttu-id="beefc-162">Jeśli planujesz funkcji dostosowanie interfejsu użytkownika strony hello toouse, przejrzyj hello następujące najlepsze rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="beefc-162">If you are planning toouse hello page UI customization feature, review hello following best practices:</span></span>

* <span data-ttu-id="beefc-163">Nie kopiowanie zawartości domyślnej hello Azure AD B2C i spróbować toomodify go.</span><span class="sxs-lookup"><span data-stu-id="beefc-163">Don't copy hello Azure AD B2C's default content and attempt toomodify it.</span></span> <span data-ttu-id="beefc-164">Jego jest najlepszym toobuild HTML5 zawartości od początku i toouse zawartości domyślnej jako odwołanie.</span><span class="sxs-lookup"><span data-stu-id="beefc-164">It is best toobuild your HTML5 content from scratch and toouse default content as reference.</span></span>
* <span data-ttu-id="beefc-165">Ze względów bezpieczeństwa firma Microsoft nie pozwala tooinclude żadnych JavaScript w zawartości.</span><span class="sxs-lookup"><span data-stu-id="beefc-165">For security reasons, we don't allow you tooinclude any JavaScript in your content.</span></span> <span data-ttu-id="beefc-166">Większość potrzebnych powinny być dostępne fabrycznej hello.</span><span class="sxs-lookup"><span data-stu-id="beefc-166">Most of what you need should be available out of hello box.</span></span> <span data-ttu-id="beefc-167">Jeśli nie, użyj [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) toorequest nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="beefc-167">If not, use [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) toorequest new functionality.</span></span>
* <span data-ttu-id="beefc-168">Obsługiwane wersje przeglądarki:</span><span class="sxs-lookup"><span data-stu-id="beefc-168">Supported browser versions:</span></span>
  * <span data-ttu-id="beefc-169">Program Internet Explorer 11, 10, krawędzi</span><span class="sxs-lookup"><span data-stu-id="beefc-169">Internet Explorer 11, 10, Edge</span></span>
  * <span data-ttu-id="beefc-170">Ograniczona obsługa programu Internet Explorer 9, 8</span><span class="sxs-lookup"><span data-stu-id="beefc-170">Limited support for Internet Explorer 9, 8</span></span>
  * <span data-ttu-id="beefc-171">Google Chrome 42.0 i powyżej.</span><span class="sxs-lookup"><span data-stu-id="beefc-171">Google Chrome 42.0 and above</span></span>
  * <span data-ttu-id="beefc-172">Mozilla Firefox 38.0 i powyżej.</span><span class="sxs-lookup"><span data-stu-id="beefc-172">Mozilla Firefox 38.0 and above</span></span>
