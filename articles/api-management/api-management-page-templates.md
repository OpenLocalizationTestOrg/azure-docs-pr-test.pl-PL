---
title: "Szablony aaaPage w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocustomize hello zawartości strony portalu dewelopera przy użyciu zestawu szablonów w usłudze Azure API Management."
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
ms.openlocfilehash: 84bd971ad4bcacfdd36c2ebbe05b16063f2a547b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="page-templates-in-azure-api-management"></a>Szablony stron w usłudze Azure API Management
Zarządzanie interfejsami API Azure oferuje hello możliwości toocustomize hello zawartości strony portalu dewelopera przy użyciu zestawu szablonów, które skonfigurować ich zawartości. Przy użyciu [DotLiquid](http://dotliquidmarkup.org/) edytora składni i hello wybranych przez użytkownika, takie jak [DotLiquid dla projektantów](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), i zestaw udostępnionego zlokalizowane [zasoby ciągu](api-management-template-resources.md#strings), [ Zasoby symbolu](api-management-template-resources.md#glyphs), i [strony kontrolki](api-management-page-controls.md), masz dużą elastyczność tooconfigure hello zawartość stron hello zgodnie z własnymi potrzebami, za pomocą tych szablonów.  
  
 Szablony Hello w tej sekcji pozwalają toocustomize zawartość hello hello znak w znaku górę, a strona nie została znaleziona stron w portalu dla deweloperów hello.  
  
-   [Rejestrowanie](#SignIn)  
  
-   [Zarejestruj się](#SignUp)  
  
-   [Strona nie została znaleziona](#PageNotFound)  
  
> [!NOTE]
>  Przykładowe domyślnych szablonów znajdują się w następującej dokumentacji hello, ale są toochange podmiotu powodu toocontinuous ulepszenia. Hello na żywo domyślnych szablonów można wyświetlić w portalu dla deweloperów hello, przechodząc toohello potrzeby poszczególnych szablonów. Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [jak toocustomize hello portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
##  <a name="SignIn"></a>Rejestrowanie  
 Witaj **Zaloguj** szablonu pozwala toocustomize hello logowania na stronie w portalu dla deweloperów hello.  
  
 ![Zaloguj się na stronie](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM logowania szablony portalu deweloperów strony")  
  
### <a name="default-template"></a>Szablon domyślny  
  
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
  
### <a name="controls"></a>Kontrolki  
 Ten szablon może używać następujących hello [strony kontrolki](api-management-page-controls.md).  
  
-   [Rejestrowanie Basic](api-management-page-controls.md#basic-signin)  
  
-   [dostawców](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a>Model danych  
 [Logowanie użytkownika](api-management-template-data-model-reference.md#UseSignIn) jednostki.  
  
### <a name="sample-template-data"></a>Przykładowe dane szablonu  
  
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
  
##  <a name="SignUp"></a>Zarejestruj się  
 Witaj **Zarejestruj** szablonu pozwala toocustomize hello stronę Tworzenie konta w portalu dla deweloperów hello.  
  
 ![Strony rejestrowania](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM Tworzenie konta dewelopera strony portalu szablonów")  
  
### <a name="default-template"></a>Szablon domyślny  
  
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
  
### <a name="controls"></a>Kontrolki  
 Ten szablon może używać następujących hello [strony kontrolki](api-management-page-controls.md).  
  
-   [rejestracji](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a>Model danych  
 [Użytkownicy logują się](api-management-template-data-model-reference.md#UserSignUp) jednostki.  
  
### <a name="sample-template-data"></a>Przykładowe dane szablonu  
  
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
  
##  <a name="PageNotFound"></a>Strona nie została znaleziona  
 Witaj **strony nie można odnaleźć** szablon umożliwia możesz toocustomize hello strony w portalu dla deweloperów hello nie znaleziono strony.  
  
 ![Nie można odnaleźć strony](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM nie znaleziono Developer strony portalu szablonów")  
  
### <a name="default-template"></a>Szablon domyślny  
  
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
  
### <a name="controls"></a>Kontrolki  
 Ten szablon nie może używać żadnego [strony kontrolki](api-management-page-controls.md).  
  
### <a name="data-model"></a>Model danych  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|referenceCode|Ciąg|Kod generowany, gdy ta strona została wyświetlona w wyniku hello wystąpił błąd wewnętrzny.|  
|Kod błędu|Ciąg|Kod generowany, gdy ta strona została wyświetlona w wyniku hello wystąpił błąd wewnętrzny.|  
|emailBody|Ciąg|Wyślij wiadomość e-mail treści generowany, gdy ta strona została wyświetlona w wyniku hello wystąpił błąd wewnętrzny.|  
|requestedUrl|Ciąg|adres URL Hello żądanych hello strony nie został znaleziony.|  
|referrerUrl|Ciąg|toohello adres URL odwołania Hello żądanego adresu URL.|  
  
### <a name="sample-template-data"></a>Przykładowe dane szablonu  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [jak toocustomize hello portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](api-management-developer-portal-templates.md).
