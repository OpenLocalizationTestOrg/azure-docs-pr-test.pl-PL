---
title: "Szablony profilów użytkownika w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dostosować zawartość strony profilu użytkownika w portalu dla deweloperów w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2e3b73ef-d223-44fe-9280-c3af3fd4a030
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 9a11bd5800068a5725ab2f099043993bff0b28d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a><span data-ttu-id="2de3e-103">Szablony profilów użytkownika w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="2de3e-103">User profile templates in Azure API Management</span></span>
<span data-ttu-id="2de3e-104">Zarządzanie interfejsami API Azure zapewnia możliwość dostosować zawartość strony portalu dewelopera przy użyciu zestawu szablonów, które skonfigurować ich zawartości.</span><span class="sxs-lookup"><span data-stu-id="2de3e-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="2de3e-105">Przy użyciu [DotLiquid](http://dotliquidmarkup.org/) składni i Edytor wybranych przez użytkownika, takie jak [DotLiquid dla projektantów](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), i zestaw udostępnionego zlokalizowane [zasoby ciągu](api-management-template-resources.md#strings), [symboli zasobów](api-management-template-resources.md#glyphs), i [strony kontrolki](api-management-page-controls.md), ma dużą elastyczność konfigurowania zawartości stron, zgodnie z własnymi potrzebami, za pomocą tych szablonów.</span><span class="sxs-lookup"><span data-stu-id="2de3e-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="2de3e-106">Szablony w tej sekcji umożliwiają dostosowanie zawartości strony profilu użytkownika w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="2de3e-106">The templates in this section allow you to customize the content of the User profile pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="2de3e-107">Profil</span><span class="sxs-lookup"><span data-stu-id="2de3e-107">Profile</span></span>](#Profile)  
  
-   [<span data-ttu-id="2de3e-108">Subskrypcje</span><span class="sxs-lookup"><span data-stu-id="2de3e-108">Subscriptions</span></span>](#Subscriptions)  
  
-   [<span data-ttu-id="2de3e-109">Aplikacje</span><span class="sxs-lookup"><span data-stu-id="2de3e-109">Applications</span></span>](#Applications)  
  
-   [<span data-ttu-id="2de3e-110">Zaktualizuj informacje o koncie</span><span class="sxs-lookup"><span data-stu-id="2de3e-110">Update account info</span></span>](#UpdateAccountInfo)  
  
> [!NOTE]
>  <span data-ttu-id="2de3e-111">Przykładowe domyślnych szablonów znajdują się w następującej dokumentacji, ale mogą ulec zmianie z powodu ciągłe ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="2de3e-111">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="2de3e-112">Szablonów domyślnych na żywo można wyświetlić w portalu dla deweloperów, przechodząc do żądanego szablony osobno.</span><span class="sxs-lookup"><span data-stu-id="2de3e-112">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="2de3e-113">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [dostosowywaniu portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="2de3e-113">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="2de3e-114"><a name="Profile"></a>Profil</span><span class="sxs-lookup"><span data-stu-id="2de3e-114"><a name="Profile"></a> Profile</span></span>  
 <span data-ttu-id="2de3e-115">**Profilu** szablonu umożliwia dostosowanie sekcji profilu użytkownika strony profilu użytkownika w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="2de3e-115">The **profile** template allows you to customize the user profile section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="2de3e-116">![Strony profilu użytkownika](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "strona profil użytkownika APIM")</span><span class="sxs-lookup"><span data-stu-id="2de3e-116">![User Profile Page](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM User Profile Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="2de3e-117">Szablon domyślny</span><span class="sxs-lookup"><span data-stu-id="2de3e-117">Default template</span></span>  
  
```xml  
<div class="pull-right">  
  {% if canChangePassword == true %}  
  <a class="btn btn-default" id="ChangePassword" role="button" href="{{changePasswordUrl}}">{% localized "UserProfile|ButtonLabelChangePassword" %}</a>  
  {% endif %}  
  <a id="changeAccountInfo" href="{{changeNameOrEmailUrl}}" class="btn btn-default">  
    <span class="glyphicon glyphicon-user"></span>  
    <span>{% localized "UserProfile|ButtonLabelChangeAccountInfo" %}</span>  
  </a>  
</div>  
<h2>{% localized "SubscriptionStrings|PageTitleDeveloperProfile" %}</h2>  
<div class="container-fluid">  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="Email">{% localized "UserProfile|TextboxLabelEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="Email">{{email}}</div>  
  </div>  
  
  {% if isSystemUser != true %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="FirstName">{% localized "UserProfile|TextboxLabelEmailFirstName" %}</label>  
    </div>  
    <div class="col-sm-9" id="FirstName">{{FirstName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="LastName">{% localized "UserProfile|TextboxLabelEmailLastName" %}</label>  
    </div>  
    <div class="col-sm-9" id="LastName">{{LastName}}</div>  
  </div>  
  {% else %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="CompanyName">{% localized "UserProfile|TextboxLabelOrganizationName" %}</label>  
    </div>  
    <div class="col-sm-9" id="CompanyName">{{CompanyName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="AddresserEmail">{% localized "UserProfile|TextboxLabelNotificationsSenderEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="AddresserEmail">{{AddresserEmail}}</div>  
  </div>  
  {% endif %}  
  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="2de3e-118">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="2de3e-118">Controls</span></span>  
 <span data-ttu-id="2de3e-119">Ten szablon nie może używać żadnego [strony kontrolki](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="2de3e-119">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="2de3e-120">Model danych</span><span class="sxs-lookup"><span data-stu-id="2de3e-120">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="2de3e-121">[Profilu](#Profile), [aplikacji](#Applications), i [subskrypcje](#Subscriptions) szablony udostępnianie tego samego modelu danych i odbierania danych tego samego szablonu.</span><span class="sxs-lookup"><span data-stu-id="2de3e-121">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="2de3e-122">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2de3e-122">Property</span></span>|<span data-ttu-id="2de3e-123">Typ</span><span class="sxs-lookup"><span data-stu-id="2de3e-123">Type</span></span>|<span data-ttu-id="2de3e-124">Opis</span><span class="sxs-lookup"><span data-stu-id="2de3e-124">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="2de3e-125">Imię</span><span class="sxs-lookup"><span data-stu-id="2de3e-125">firstName</span></span>|<span data-ttu-id="2de3e-126">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-126">string</span></span>|<span data-ttu-id="2de3e-127">Imię bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-127">First name of the current user.</span></span>|  
|<span data-ttu-id="2de3e-128">Nazwisko</span><span class="sxs-lookup"><span data-stu-id="2de3e-128">lastName</span></span>|<span data-ttu-id="2de3e-129">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-129">string</span></span>|<span data-ttu-id="2de3e-130">Nazwa ostatniego bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-130">Last name of the current user.</span></span>|  
|<span data-ttu-id="2de3e-131">Nazwa firmy</span><span class="sxs-lookup"><span data-stu-id="2de3e-131">companyName</span></span>|<span data-ttu-id="2de3e-132">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-132">string</span></span>|<span data-ttu-id="2de3e-133">Nazwa firmy bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-133">The company name of the current user.</span></span>|  
|<span data-ttu-id="2de3e-134">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="2de3e-134">addresserEmail</span></span>|<span data-ttu-id="2de3e-135">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-135">string</span></span>|<span data-ttu-id="2de3e-136">Adres e-mail bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-136">Email address of the current user.</span></span>|  
|<span data-ttu-id="2de3e-137">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="2de3e-137">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="2de3e-138">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-138">string</span></span>|<span data-ttu-id="2de3e-139">Względny adres URL, aby wyświetlić analytics dla bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-139">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="2de3e-140">Subskrypcje</span><span class="sxs-lookup"><span data-stu-id="2de3e-140">subscriptions</span></span>|<span data-ttu-id="2de3e-141">Kolekcja [subskrypcji](api-management-template-data-model-reference.md#Subscription) jednostek.</span><span class="sxs-lookup"><span data-stu-id="2de3e-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="2de3e-142">Subskrypcje dla bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-142">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="2de3e-143">aplikacje</span><span class="sxs-lookup"><span data-stu-id="2de3e-143">applications</span></span>|<span data-ttu-id="2de3e-144">Kolekcja [aplikacji](api-management-template-data-model-reference.md#Application) jednostek.</span><span class="sxs-lookup"><span data-stu-id="2de3e-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="2de3e-145">Aplikacje bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-145">The applications of the current user.</span></span>|  
|<span data-ttu-id="2de3e-146">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="2de3e-146">changePasswordUrl</span></span>|<span data-ttu-id="2de3e-147">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-147">string</span></span>|<span data-ttu-id="2de3e-148">Względny adres URL do zmiany hasła bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-148">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="2de3e-149">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="2de3e-149">changeNameOrEmailUrl</span></span>|<span data-ttu-id="2de3e-150">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-150">string</span></span>|<span data-ttu-id="2de3e-151">Względny adres URL, aby zmienić nazwę i adres e-mail dla bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-151">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="2de3e-152">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="2de3e-152">canChangePassword</span></span>|<span data-ttu-id="2de3e-153">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2de3e-153">boolean</span></span>|<span data-ttu-id="2de3e-154">Określa, czy bieżący użytkownik może zmienić swoje hasło.</span><span class="sxs-lookup"><span data-stu-id="2de3e-154">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="2de3e-155">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="2de3e-155">isSystemUser</span></span>|<span data-ttu-id="2de3e-156">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2de3e-156">boolean</span></span>|<span data-ttu-id="2de3e-157">Określa, czy bieżący użytkownik jest członkiem jednej z wbudowanych [grup](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="2de3e-157">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="2de3e-158">Przykładowe dane szablonu</span><span class="sxs-lookup"><span data-stu-id="2de3e-158">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="2de3e-159"><a name="Subscriptions"></a>Subskrypcje</span><span class="sxs-lookup"><span data-stu-id="2de3e-159"><a name="Subscriptions"></a> Subscriptions</span></span>  
 <span data-ttu-id="2de3e-160">**Subskrypcje** szablonu umożliwia dostosowanie subskrypcje części strony profilu użytkownika w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="2de3e-160">The **Subscriptions** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="2de3e-161">![Strona subskrypcji użytkownika](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "stronę subskrypcji użytkownika APIM")</span><span class="sxs-lookup"><span data-stu-id="2de3e-161">![User Subscription Page](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM User Subscription Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="2de3e-162">Szablon domyślny</span><span class="sxs-lookup"><span data-stu-id="2de3e-162">Default template</span></span>  
  
```xml  
<div class="ap-account-subscriptions">  
  <a href="{{developersUsageStatisticsLink}}" id="UsageStatistics" class="btn btn-default pull-right">  
    <span class="glyphicon glyphicon-stats"></span>  
    <span>{% localized "SubscriptionListStrings|WebDevelopersUsageStatisticsLink" %}</span>  
  </a>  
  
  <h2>{% localized "SubscriptionListStrings|WebDevelopersYourSubscriptions" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th>Subscription details</th>  
        <th>Product</th>  
        <th>{% localized "SubscriptionListStrings|WebDevelopersSubscriptionTableStateHeader" %}</th>  
        <th>Action</th>  
      </tr>  
    </thead>  
    <tbody>  
      {% if subscriptions.size == 0 %}  
      <tr>  
        <td class="text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
      {% else %}  
      {% for subscription in subscriptions %}  
      <tr id="{{subscription.id}}" {% if subscription.hasExpired %} class="expired" {% endif %}>  
        <td>  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelName" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.displayName }}  
            </div>  
            <div class="col-lg-2">  
              <a class="btn-link" href="/Subscriptions/{{subscription.id}}/Rename">Rename</a>  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          {% if subscription.isAwaitingApproval %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelRequestedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.createdDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% else %}  
          {% if subscription.isRejected == false %}  
          {% if subscription.startDate %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelStartedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.startDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% endif %}  
  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.primaryKey}}', '{{subscription.id}}', true) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersPrimaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="primary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <!-- ko if: !requestInProgress() -->  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="togglePrimary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel"></a>  
                |  
                <a href="#" class="btn-link" id="regeneratePrimary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel"></a>  
              </div>  
              <!-- /ko -->  
              <!-- ko if: requestInProgress() -->  
              <div class="progress progress-striped active">  
                <div class="progress-bar" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%">  
                  <span class="sr-only"></span>  
                </div>  
              </div>  
              <!-- /ko -->  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          <!-- /ko -->  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.secondaryKey}}', '{{subscription.id}}', false) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersSecondaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="secondary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="toggleSecondary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel">{% localized "SubscriptionListStrings|ButtonLabelShowKey" %}</a>  
                |  
                <a href="#" class="btn-link" id="regenerateSecondary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel">{% localized "SubscriptionListStrings|WebDevelopersRegenerateLink" %}</a>  
              </div>  
            </div>  
            <div class="clearfix"> </div>  
          </div>  
          <!-- /ko -->  
          {% endif %}  
          {% endif %}  
        </td>  
        <td>  
          <a href="{{subscription.productDetailsUrl}}">{{subscription.productTitle}}</a>  
        </td>  
        <td>  
          <strong>  
            {{subscription.state}}  
          </strong>  
        </td>  
        <td>  
          <div class="nowrap">  
            {% if subscription.canBeCancelled %}  
            <subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }"></subscription-cancel>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="2de3e-163">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="2de3e-163">Controls</span></span>  
 <span data-ttu-id="2de3e-164">Ten szablon może korzystać z następujących [strony kontrolki](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="2de3e-164">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="2de3e-165">Anuluj subskrypcję</span><span class="sxs-lookup"><span data-stu-id="2de3e-165">subscription-cancel</span></span>](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a><span data-ttu-id="2de3e-166">Model danych</span><span class="sxs-lookup"><span data-stu-id="2de3e-166">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="2de3e-167">[Profilu](#Profile), [aplikacji](#Applications), i [subskrypcje](#Subscriptions) szablony udostępnianie tego samego modelu danych i odbierania danych tego samego szablonu.</span><span class="sxs-lookup"><span data-stu-id="2de3e-167">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="2de3e-168">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2de3e-168">Property</span></span>|<span data-ttu-id="2de3e-169">Typ</span><span class="sxs-lookup"><span data-stu-id="2de3e-169">Type</span></span>|<span data-ttu-id="2de3e-170">Opis</span><span class="sxs-lookup"><span data-stu-id="2de3e-170">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="2de3e-171">Imię</span><span class="sxs-lookup"><span data-stu-id="2de3e-171">firstName</span></span>|<span data-ttu-id="2de3e-172">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-172">string</span></span>|<span data-ttu-id="2de3e-173">Imię bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-173">First name of the current user.</span></span>|  
|<span data-ttu-id="2de3e-174">Nazwisko</span><span class="sxs-lookup"><span data-stu-id="2de3e-174">lastName</span></span>|<span data-ttu-id="2de3e-175">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-175">string</span></span>|<span data-ttu-id="2de3e-176">Nazwa ostatniego bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-176">Last name of the current user.</span></span>|  
|<span data-ttu-id="2de3e-177">Nazwa firmy</span><span class="sxs-lookup"><span data-stu-id="2de3e-177">companyName</span></span>|<span data-ttu-id="2de3e-178">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-178">string</span></span>|<span data-ttu-id="2de3e-179">Nazwa firmy bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-179">The company name of the current user.</span></span>|  
|<span data-ttu-id="2de3e-180">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="2de3e-180">addresserEmail</span></span>|<span data-ttu-id="2de3e-181">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-181">string</span></span>|<span data-ttu-id="2de3e-182">Adres e-mail bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-182">Email address of the current user.</span></span>|  
|<span data-ttu-id="2de3e-183">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="2de3e-183">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="2de3e-184">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-184">string</span></span>|<span data-ttu-id="2de3e-185">Względny adres URL, aby wyświetlić analytics dla bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-185">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="2de3e-186">Subskrypcje</span><span class="sxs-lookup"><span data-stu-id="2de3e-186">subscriptions</span></span>|<span data-ttu-id="2de3e-187">Kolekcja [subskrypcji](api-management-template-data-model-reference.md#Subscription) jednostek.</span><span class="sxs-lookup"><span data-stu-id="2de3e-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="2de3e-188">Subskrypcje dla bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-188">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="2de3e-189">aplikacje</span><span class="sxs-lookup"><span data-stu-id="2de3e-189">applications</span></span>|<span data-ttu-id="2de3e-190">Kolekcja [aplikacji](api-management-template-data-model-reference.md#Application) jednostek.</span><span class="sxs-lookup"><span data-stu-id="2de3e-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="2de3e-191">Aplikacje bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-191">The applications of the current user.</span></span>|  
|<span data-ttu-id="2de3e-192">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="2de3e-192">changePasswordUrl</span></span>|<span data-ttu-id="2de3e-193">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-193">string</span></span>|<span data-ttu-id="2de3e-194">Względny adres URL do zmiany hasła bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-194">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="2de3e-195">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="2de3e-195">changeNameOrEmailUrl</span></span>|<span data-ttu-id="2de3e-196">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-196">string</span></span>|<span data-ttu-id="2de3e-197">Względny adres URL, aby zmienić nazwę i adres e-mail dla bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-197">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="2de3e-198">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="2de3e-198">canChangePassword</span></span>|<span data-ttu-id="2de3e-199">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2de3e-199">boolean</span></span>|<span data-ttu-id="2de3e-200">Określa, czy bieżący użytkownik może zmienić swoje hasło.</span><span class="sxs-lookup"><span data-stu-id="2de3e-200">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="2de3e-201">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="2de3e-201">isSystemUser</span></span>|<span data-ttu-id="2de3e-202">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2de3e-202">boolean</span></span>|<span data-ttu-id="2de3e-203">Określa, czy bieżący użytkownik jest członkiem jednej z wbudowanych [grup](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="2de3e-203">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="2de3e-204">Przykładowe dane szablonu</span><span class="sxs-lookup"><span data-stu-id="2de3e-204">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="2de3e-205"><a name="Applications"></a>Aplikacje</span><span class="sxs-lookup"><span data-stu-id="2de3e-205"><a name="Applications"></a> Applications</span></span>  
 <span data-ttu-id="2de3e-206">**Aplikacji** szablonu umożliwia dostosowanie subskrypcje części strony profilu użytkownika w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="2de3e-206">The **Applications** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="2de3e-207">![Strony aplikacji na koncie użytkownika](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "konta użytkownika APIM strony aplikacji")</span><span class="sxs-lookup"><span data-stu-id="2de3e-207">![User Account Applications Page](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM User Account Applications Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="2de3e-208">Szablon domyślny</span><span class="sxs-lookup"><span data-stu-id="2de3e-208">Default template</span></span>  
  
```xml  
<div class="ap-account-applications">  
  <a id="RegisterApplication" href="/Developer/Applications/Register" class="btn btn-success pull-right">  
    <span class="glyphicon glyphicon-plus"></span>  
    <span>{% localized "ApplicationListStrings|WebDevelopersRegisterAppLink" %}</span>  
  </a>  
  <h2>{% localized "ApplicationListStrings|WebDevelopersYourApplicationsHeader" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th class="col-md-8">{% localized "ApplicationListStrings|WebDevelopersAppTableNameHeader" %}</th>  
        <th class="col-md-2">{% localized "ApplicationListStrings|WebDevelopersAppTableCategoryHeader" %}</th>  
        <th class="col-md-2" colspan="2">{% localized "ApplicationListStrings|WebDevelopersAppTableStateHeader" %}</th>  
      </tr>  
    </thead>  
    <tbody>  
  
      {% if applications.size == 0 %}  
  
      <tr>  
        <td class="col-md-12 text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
  
      {% else %}  
  
      {% for app in applications %}  
      <tr>  
        <td class="col-md-8">  
          {{app.title}}  
        </td>  
        <td class="col-md-2">  
          {{app.categoryName}}  
        </td>  
        <td class="col-md-2">  
          <strong>  
            {% case app.state %}  
            {% when ApplicationStateModel.Registered %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotSubminted" %}  
  
            {% when ApplicationStateModel.Unpublished %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotPublished" %}  
  
            {% else %}  
            {{ app.state }}  
            {% endcase %}  
          </strong>  
        </td>  
        <td class="col-md-1">  
          <div class="nowrap">  
            {% if app.state != ApplicationStateModel.Submitted and app.state != ApplicationStateModel.Published %}  
            <app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="2de3e-209">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="2de3e-209">Controls</span></span>  
 <span data-ttu-id="2de3e-210">Ten szablon może korzystać z następujących [strony kontrolki](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="2de3e-210">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="2de3e-211">Akcje aplikacji</span><span class="sxs-lookup"><span data-stu-id="2de3e-211">app-actions</span></span>](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a><span data-ttu-id="2de3e-212">Model danych</span><span class="sxs-lookup"><span data-stu-id="2de3e-212">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="2de3e-213">[Profilu](#Profile), [aplikacji](#Applications), i [subskrypcje](#Subscriptions) szablony udostępnianie tego samego modelu danych i odbierania danych tego samego szablonu.</span><span class="sxs-lookup"><span data-stu-id="2de3e-213">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="2de3e-214">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2de3e-214">Property</span></span>|<span data-ttu-id="2de3e-215">Typ</span><span class="sxs-lookup"><span data-stu-id="2de3e-215">Type</span></span>|<span data-ttu-id="2de3e-216">Opis</span><span class="sxs-lookup"><span data-stu-id="2de3e-216">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="2de3e-217">Imię</span><span class="sxs-lookup"><span data-stu-id="2de3e-217">firstName</span></span>|<span data-ttu-id="2de3e-218">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-218">string</span></span>|<span data-ttu-id="2de3e-219">Imię bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-219">First name of the current user.</span></span>|  
|<span data-ttu-id="2de3e-220">Nazwisko</span><span class="sxs-lookup"><span data-stu-id="2de3e-220">lastName</span></span>|<span data-ttu-id="2de3e-221">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-221">string</span></span>|<span data-ttu-id="2de3e-222">Nazwa ostatniego bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-222">Last name of the current user.</span></span>|  
|<span data-ttu-id="2de3e-223">Nazwa firmy</span><span class="sxs-lookup"><span data-stu-id="2de3e-223">companyName</span></span>|<span data-ttu-id="2de3e-224">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-224">string</span></span>|<span data-ttu-id="2de3e-225">Nazwa firmy bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-225">The company name of the current user.</span></span>|  
|<span data-ttu-id="2de3e-226">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="2de3e-226">addresserEmail</span></span>|<span data-ttu-id="2de3e-227">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-227">string</span></span>|<span data-ttu-id="2de3e-228">Adres e-mail bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-228">Email address of the current user.</span></span>|  
|<span data-ttu-id="2de3e-229">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="2de3e-229">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="2de3e-230">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-230">string</span></span>|<span data-ttu-id="2de3e-231">Względny adres URL, aby wyświetlić analytics dla bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-231">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="2de3e-232">Subskrypcje</span><span class="sxs-lookup"><span data-stu-id="2de3e-232">subscriptions</span></span>|<span data-ttu-id="2de3e-233">Kolekcja [subskrypcji](api-management-template-data-model-reference.md#Subscription) jednostek.</span><span class="sxs-lookup"><span data-stu-id="2de3e-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="2de3e-234">Subskrypcje dla bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-234">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="2de3e-235">aplikacje</span><span class="sxs-lookup"><span data-stu-id="2de3e-235">applications</span></span>|<span data-ttu-id="2de3e-236">Kolekcja [aplikacji](api-management-template-data-model-reference.md#Application) jednostek.</span><span class="sxs-lookup"><span data-stu-id="2de3e-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="2de3e-237">Aplikacje bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-237">The applications of the current user.</span></span>|  
|<span data-ttu-id="2de3e-238">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="2de3e-238">changePasswordUrl</span></span>|<span data-ttu-id="2de3e-239">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-239">string</span></span>|<span data-ttu-id="2de3e-240">Względny adres URL do zmiany hasła bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-240">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="2de3e-241">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="2de3e-241">changeNameOrEmailUrl</span></span>|<span data-ttu-id="2de3e-242">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2de3e-242">string</span></span>|<span data-ttu-id="2de3e-243">Względny adres URL, aby zmienić nazwę i adres e-mail dla bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2de3e-243">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="2de3e-244">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="2de3e-244">canChangePassword</span></span>|<span data-ttu-id="2de3e-245">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2de3e-245">boolean</span></span>|<span data-ttu-id="2de3e-246">Określa, czy bieżący użytkownik może zmienić swoje hasło.</span><span class="sxs-lookup"><span data-stu-id="2de3e-246">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="2de3e-247">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="2de3e-247">isSystemUser</span></span>|<span data-ttu-id="2de3e-248">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2de3e-248">boolean</span></span>|<span data-ttu-id="2de3e-249">Określa, czy bieżący użytkownik jest członkiem jednej z wbudowanych [grup](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="2de3e-249">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="2de3e-250">Przykładowe dane szablonu</span><span class="sxs-lookup"><span data-stu-id="2de3e-250">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="2de3e-251"><a name="UpdateAccountInfo"></a>Zaktualizuj informacje o koncie</span><span class="sxs-lookup"><span data-stu-id="2de3e-251"><a name="UpdateAccountInfo"></a> Update account info</span></span>  
 <span data-ttu-id="2de3e-252">**Informacje o koncie Uodate** szablonu umożliwia dostosowanie **zaktualizować informacje o koncie** strony w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="2de3e-252">The **Uodate account info** template allows you to customize the **Update account information** page in the developer portal.</span></span>  
  
 <span data-ttu-id="2de3e-253">![Szablony portalu użytkownika konta informacje Developer strony](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM użytkownika konta informacje Developer strony portalu szablonów")</span><span class="sxs-lookup"><span data-stu-id="2de3e-253">![User Account Info Page Developer Portal Templates](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM User Account Info Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="2de3e-254">Szablon domyślny</span><span class="sxs-lookup"><span data-stu-id="2de3e-254">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-sm-6 col-md-6">  
    <div class="form-group">  
      <label for="Email">{% localized "SigninResources|TextboxLabelEmail" %}</label>  
      <input autofocus="autofocus" class="form-control" id="Email" name="Email" type="text" value="{{email}}">  
    </div>  
    <div class="form-group">  
      <label for="FirstName">{% localized "SigninResources|TextboxLabelEmailFirstName" %}</label>  
      <input class="form-control" id="FirstName" name="FirstName" type="text" value="{{firstName}}">  
    </div>  
    <div class="form-group">  
      <label for="LastName">{% localized "SigninResources|TextboxLabelEmailLastName" %}</label>  
      <input class="form-control" id="LastName" name="LastName" type="text" value="{{lastName}}">  
    </div>  
    <div class="form-group">  
      <label for="Password">{% localized "SigninResources|WebAuthenticationSigninPasswordLabel" %}</label>  
      <input class="form-control" id="Password" name="Password" type="password">  
    </div>  
  </div>  
</div>  
  
<button type="submit" class="btn btn-primary" id="UpdateProfile">  
  {% localized "UpdateProfileStrings|ButtonLabelUpdateProfile" %}  
</button>  
<a class="btn btn-default" href="/developer" role="button">  
  {% localized "CommonStrings|ButtonLabelCancel" %}  
</a>  
```  
  
### <a name="controls"></a><span data-ttu-id="2de3e-255">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="2de3e-255">Controls</span></span>  
 <span data-ttu-id="2de3e-256">Ten szablon nie może używać żadnego [strony kontrolki](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="2de3e-256">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="2de3e-257">Model danych</span><span class="sxs-lookup"><span data-stu-id="2de3e-257">Data model</span></span>  
 <span data-ttu-id="2de3e-258">[Informacje o koncie użytkownika](api-management-template-data-model-reference.md#UserAccountInfo) jednostki.</span><span class="sxs-lookup"><span data-stu-id="2de3e-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="2de3e-259">Przykładowe dane szablonu</span><span class="sxs-lookup"><span data-stu-id="2de3e-259">Sample template data</span></span>  
  
```json  
{  
    "FirstName": "Administrator",  
    "LastName": "",  
    "Email": "admin@live.com",  
    "Password": null,  
    "NameIdentifier": null,  
    "ProviderName": null,  
    "IsBasicAccount": false  
}  
```

## <a name="next-steps"></a><span data-ttu-id="2de3e-260">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2de3e-260">Next steps</span></span>
<span data-ttu-id="2de3e-261">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [dostosowywaniu portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2de3e-261">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>