---
title: "Strona Szablony w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dostosować zawartość strony portalu dewelopera przy użyciu zestawu szablonów w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: e57df269-1019-4b74-b74d-53155b809d59
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 7f9ef37a694bce786b6acaa428df83f0cb23c2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="page-templates-in-azure-api-management"></a><span data-ttu-id="6e8e7-103">Szablony stron w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="6e8e7-103">Page templates in Azure API Management</span></span>
<span data-ttu-id="6e8e7-104">Zarządzanie interfejsami API Azure zapewnia możliwość dostosować zawartość strony portalu dewelopera przy użyciu zestawu szablonów, które skonfigurować ich zawartości.</span><span class="sxs-lookup"><span data-stu-id="6e8e7-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="6e8e7-105">Przy użyciu [DotLiquid](http://dotliquidmarkup.org/) składni i Edytor wybranych przez użytkownika, takie jak [DotLiquid dla projektantów](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), i zestaw udostępnionego zlokalizowane [zasoby ciągu](api-management-template-resources.md#strings), [symboli zasobów](api-management-template-resources.md#glyphs), i [strony kontrolki](api-management-page-controls.md), ma dużą elastyczność konfigurowania zawartości stron, zgodnie z własnymi potrzebami, za pomocą tych szablonów.</span><span class="sxs-lookup"><span data-stu-id="6e8e7-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="6e8e7-106">Szablony w tej sekcji umożliwiają dostosowanie zawartości logowania, zaloguj się, a strona nie została znaleziona stron w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="6e8e7-106">The templates in this section allow you to customize the content of the sign in, sign up, and page not found pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="6e8e7-107">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="6e8e7-107">Sign in</span></span>](#SignIn)  
  
-   [<span data-ttu-id="6e8e7-108">Zarejestruj się</span><span class="sxs-lookup"><span data-stu-id="6e8e7-108">Sign up</span></span>](#SignUp)  
  
-   [<span data-ttu-id="6e8e7-109">Strona nie została znaleziona</span><span class="sxs-lookup"><span data-stu-id="6e8e7-109">Page not found</span></span>](#PageNotFound)  
  
> [!NOTE]
>  <span data-ttu-id="6e8e7-110">Przykładowe domyślnych szablonów znajdują się w następującej dokumentacji, ale mogą ulec zmianie z powodu ciągłe ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="6e8e7-110">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="6e8e7-111">Szablonów domyślnych na żywo można wyświetlić w portalu dla deweloperów, przechodząc do żądanego szablony osobno.</span><span class="sxs-lookup"><span data-stu-id="6e8e7-111">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="6e8e7-112">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [dostosowywaniu portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="6e8e7-112">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="6e8e7-113"><a name="SignIn"></a>Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="6e8e7-113"><a name="SignIn"></a> Sign in</span></span>  
 <span data-ttu-id="6e8e7-114">**Zaloguj** szablonu umożliwia dostosowanie stronie logowania w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="6e8e7-114">The **sign in** template allows you to customize the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="6e8e7-115">![Zaloguj się na stronie](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM logowania szablony portalu deweloperów strony")</span><span class="sxs-lookup"><span data-stu-id="6e8e7-115">![Sign In Page](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM Sign In Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="6e8e7-116">Szablon domyślny</span><span class="sxs-lookup"><span data-stu-id="6e8e7-116">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SigninStrings|WebAuthenticationSigninTitle" %}</h2>  
{% if registrationEnabled == true %}  
<p class="text-center">{% localized "SigninStrings|WebAuthenticationNotAMember" %}</p>  
{% endif %}  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    {% if registrationEnabled == true %}  
        <p>{% localized "SigninStrings|WebAuthenticationSigininWithPassword" %}</p>  
    <basic-SignIn></basic-SignIn>  
    {% endif %}  
  </div>  
  
    {% if registrationEnabled != true and providers.size == 0 %}  
        {% localized "ProviderInfoStrings|TextboxExternalIdentitiesDisabled" %}  
  {% else %}  
        {% if providers.size > 0 %}  
      <div class="col-md-6">  
            <div class="providers-list">  
                <p class="text-left">  
                {% if registrationEnabled == true %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitation" %}  
                {% else %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitationPrimary" %}  
                {% endif %}  
                </p>  
        <providers></providers>  
            </div>  
    </div>  
        {% endif %}  
    {% endif %}  
  
  {% if userRegistrationTermsEnabled == true %}  
    <div class="col-md-6">  
        <div id="terms" class="modal" role="dialog" tabindex="-1">  
            <div class="modal-dialog">  
                <div class="modal-content">  
                    <div class="modal-header">  
                        <h4 class="modal-title">{% localized "SigninResources|DialogHeadingTermsOfUse" %}</h4>  
                    </div>  
                    <div class="modal-body break-all">{{userRegistrationTerms}}</div>  
                    <div class="modal-footer">  
                        <button type="button" class="btn btn-default" data-dismiss="modal">{% localized "CommonStrings|ButtonLabelClose" %}</button>  
                    </div>  
                </div>  
            </div>  
        </div>  
        <p>{% localized "SigninResources|TextblockUserRegistrationTermsProvided" %}</p>  
    </div>  
    {% endif %}  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="6e8e7-117">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="6e8e7-117">Controls</span></span>  
 <span data-ttu-id="6e8e7-118">Ten szablon może korzystać z następujących [strony kontrolki](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="6e8e7-118">This template may  use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="6e8e7-119">Rejestrowanie Basic</span><span class="sxs-lookup"><span data-stu-id="6e8e7-119">basic-signin</span></span>](api-management-page-controls.md#basic-signin)  
  
-   [<span data-ttu-id="6e8e7-120">dostawców</span><span class="sxs-lookup"><span data-stu-id="6e8e7-120">providers</span></span>](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a><span data-ttu-id="6e8e7-121">Model danych</span><span class="sxs-lookup"><span data-stu-id="6e8e7-121">Data model</span></span>  
 <span data-ttu-id="6e8e7-122">[Logowanie użytkownika](api-management-template-data-model-reference.md#UseSignIn) jednostki.</span><span class="sxs-lookup"><span data-stu-id="6e8e7-122">[User sign in](api-management-template-data-model-reference.md#UseSignIn) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="6e8e7-123">Przykładowe dane szablonu</span><span class="sxs-lookup"><span data-stu-id="6e8e7-123">Sample template data</span></span>  
  
```json  
{  
    "Email": null,  
    "Password": null,  
    "ReturnUrl": null,  
    "RememberMe": false,  
    "RegistrationEnabled": true,  
    "DelegationEnabled": false,  
    "DelegationUrl": null,  
    "SsoSignUpUrl": null,  
    "AuxServiceUrl": "https://manage.windowsazure.com/#Workspaces/ApiManagementExtension/service/contoso5/dashboard",  
    "Providers": [  
        {  
            "Properties": {  
                "AuthenticationType": "Aad",  
                "Caption": "Azure Active Directory"  
            },  
            "AuthenticationType": "Aad",  
            "Caption": "Azure Active Directory"  
        }  
    ],  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsEnabled": false  
}  
```  
  
##  <span data-ttu-id="6e8e7-124"><a name="SignUp"></a>Zarejestruj się</span><span class="sxs-lookup"><span data-stu-id="6e8e7-124"><a name="SignUp"></a> Sign up</span></span>  
 <span data-ttu-id="6e8e7-125">**Zarejestruj** szablonu umożliwia dostosowanie rejestracji strony w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="6e8e7-125">The **sign up** template allows you to customize the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="6e8e7-126">![Strony rejestrowania](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM Tworzenie konta dewelopera strony portalu szablonów")</span><span class="sxs-lookup"><span data-stu-id="6e8e7-126">![Sign Up Page](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM Sign Up Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="6e8e7-127">Szablon domyślny</span><span class="sxs-lookup"><span data-stu-id="6e8e7-127">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SignupStrings|PageTitleSignup" %}</h2>  
<p class="text-center">  
  {% localized "SignupStrings|WebAuthenticationAlreadyAMember" %} <a href="/signin">{% localized "SignupStrings|WebAuthenticationSigninNow" %}</a>  
</p>  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    <p>{% localized "SignupStrings|WebAuthenticationCreateNewAccount" %}</p>  
    <sign-up></sign-up>  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="6e8e7-128">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="6e8e7-128">Controls</span></span>  
 <span data-ttu-id="6e8e7-129">Ten szablon może korzystać z następujących [strony kontrolki](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="6e8e7-129">This template may  use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="6e8e7-130">rejestracji</span><span class="sxs-lookup"><span data-stu-id="6e8e7-130">sign-up</span></span>](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a><span data-ttu-id="6e8e7-131">Model danych</span><span class="sxs-lookup"><span data-stu-id="6e8e7-131">Data model</span></span>  
 <span data-ttu-id="6e8e7-132">[Użytkownicy logują się](api-management-template-data-model-reference.md#UserSignUp) jednostki.</span><span class="sxs-lookup"><span data-stu-id="6e8e7-132">[User sign up](api-management-template-data-model-reference.md#UserSignUp) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="6e8e7-133">Przykładowe dane szablonu</span><span class="sxs-lookup"><span data-stu-id="6e8e7-133">Sample template data</span></span>  
  
```json  
{  
    "PasswordConfirm": null,  
    "Password": null,  
    "PasswordVerdictLevel": 0,  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsOptions": 0,  
    "ConsentAccepted": false,  
    "Email": null,  
    "FirstName": null,  
    "LastName": null,  
    "UserData": null,  
    "NameIdentifier": null,  
    "ProviderName": null  
}  
```  
  
##  <span data-ttu-id="6e8e7-134"><a name="PageNotFound"></a>Strona nie została znaleziona</span><span class="sxs-lookup"><span data-stu-id="6e8e7-134"><a name="PageNotFound"></a> Page not found</span></span>  
 <span data-ttu-id="6e8e7-135">**Strony nie można odnaleźć** szablon umożliwia dostosowywanie strony nie można odnaleźć strony w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="6e8e7-135">The **page not found** template allows you to customize the page not found page in the developer portal.</span></span>  
  
 <span data-ttu-id="6e8e7-136">![Nie można odnaleźć strony](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM nie znaleziono Developer strony portalu szablonów")</span><span class="sxs-lookup"><span data-stu-id="6e8e7-136">![Not Found Page](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM Not Found Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="6e8e7-137">Szablon domyślny</span><span class="sxs-lookup"><span data-stu-id="6e8e7-137">Default template</span></span>  
  
```xml  
<h2>{% localized "NotFoundStrings|PageTitleNotFound" %}</h2>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialCause" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseOldLink" %}</li>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseMisspelledUrl" %}</li>  
</ul>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialSolution" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialSolutionRetype" %}</li>  
  <li>  
    {% capture textPotentialSolutionStartOver %}{% localized "NotFoundStrings|TextblockPotentialSolutionStartOver" %}{% endcapture %}  
    {% capture homeLink %}<a href="/">{% localized "NotFoundStrings|LinkLabelHomePage" %}</a>{% endcapture %}  
    {% assign replaceString = '{0}' %}  
  
    {{ textPotentialSolutionStartOver | replace : replaceString, homeLink }}  
  </li>  
</ul>  
  
<p>  
  {% capture textReportProblem %}{% localized "NotFoundStrings|TextReportProblem" %}{% endcapture %}  
  {% capture emailLink %}<a href="mailto:apimgmt@microsoft.com" target="_self" title="API Management Support">{% localized "NotFoundStrings|LinkLabelSendUsEmail" %}</a>{% endcapture %}  
  {% assign replaceString = '{0}' %}  
  
  {{ textReportProblem | replace : replaceString, emailLink }}  
</p>  
```  
  
### <a name="controls"></a><span data-ttu-id="6e8e7-138">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="6e8e7-138">Controls</span></span>  
 <span data-ttu-id="6e8e7-139">Ten szablon nie może używać żadnego [strony kontrolki](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="6e8e7-139">This template may  not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="6e8e7-140">Model danych</span><span class="sxs-lookup"><span data-stu-id="6e8e7-140">Data model</span></span>  
  
|<span data-ttu-id="6e8e7-141">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6e8e7-141">Property</span></span>|<span data-ttu-id="6e8e7-142">Typ</span><span class="sxs-lookup"><span data-stu-id="6e8e7-142">Type</span></span>|<span data-ttu-id="6e8e7-143">Opis</span><span class="sxs-lookup"><span data-stu-id="6e8e7-143">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="6e8e7-144">referenceCode</span><span class="sxs-lookup"><span data-stu-id="6e8e7-144">referenceCode</span></span>|<span data-ttu-id="6e8e7-145">Ciąg</span><span class="sxs-lookup"><span data-stu-id="6e8e7-145">string</span></span>|<span data-ttu-id="6e8e7-146">Kod generowany, gdy ta strona została wyświetlona w wyniku błędu wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="6e8e7-146">Code generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="6e8e7-147">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="6e8e7-147">errorCode</span></span>|<span data-ttu-id="6e8e7-148">Ciąg</span><span class="sxs-lookup"><span data-stu-id="6e8e7-148">string</span></span>|<span data-ttu-id="6e8e7-149">Kod generowany, gdy ta strona została wyświetlona w wyniku błędu wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="6e8e7-149">Code generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="6e8e7-150">emailBody</span><span class="sxs-lookup"><span data-stu-id="6e8e7-150">emailBody</span></span>|<span data-ttu-id="6e8e7-151">Ciąg</span><span class="sxs-lookup"><span data-stu-id="6e8e7-151">string</span></span>|<span data-ttu-id="6e8e7-152">Wyślij wiadomość e-mail treści generowany, gdy ta strona została wyświetlona w wyniku błędu wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="6e8e7-152">Email body generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="6e8e7-153">requestedUrl</span><span class="sxs-lookup"><span data-stu-id="6e8e7-153">requestedUrl</span></span>|<span data-ttu-id="6e8e7-154">Ciąg</span><span class="sxs-lookup"><span data-stu-id="6e8e7-154">string</span></span>|<span data-ttu-id="6e8e7-155">Adres URL żądanych nie odnaleziono strony.</span><span class="sxs-lookup"><span data-stu-id="6e8e7-155">The URL requested when the page was not found.</span></span>|  
|<span data-ttu-id="6e8e7-156">referrerUrl</span><span class="sxs-lookup"><span data-stu-id="6e8e7-156">referrerUrl</span></span>|<span data-ttu-id="6e8e7-157">Ciąg</span><span class="sxs-lookup"><span data-stu-id="6e8e7-157">string</span></span>|<span data-ttu-id="6e8e7-158">Adres URL odwołania do żądanego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="6e8e7-158">The referrer URL to the requested URL.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="6e8e7-159">Przykładowe dane szablonu</span><span class="sxs-lookup"><span data-stu-id="6e8e7-159">Sample template data</span></span>  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a><span data-ttu-id="6e8e7-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6e8e7-160">Next steps</span></span>
<span data-ttu-id="6e8e7-161">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [dostosowywaniu portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6e8e7-161">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>