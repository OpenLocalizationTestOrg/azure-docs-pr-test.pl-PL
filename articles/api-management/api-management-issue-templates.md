---
title: "Należy wystawić szablony w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dostosować zawartość strony problem w portalu dla deweloperów w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 47da4bb2-426e-4e53-8fa7-214ee2e3ab37
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: e13344df198bca4f73c75fa58221436b94e2f258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="deb20-103">Szablony problem w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="deb20-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="deb20-104">Zarządzanie interfejsami API Azure zapewnia możliwość dostosować zawartość strony portalu dewelopera przy użyciu zestawu szablonów, które skonfigurować ich zawartości.</span><span class="sxs-lookup"><span data-stu-id="deb20-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="deb20-105">Przy użyciu [DotLiquid](http://dotliquidmarkup.org/) składni i Edytor wybranych przez użytkownika, takie jak [DotLiquid dla projektantów](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), i zestaw udostępnionego zlokalizowane [zasoby ciągu](api-management-template-resources.md#strings), [symboli zasobów](api-management-template-resources.md#glyphs), i [strony kontrolki](api-management-page-controls.md), ma dużą elastyczność konfigurowania zawartości stron, zgodnie z własnymi potrzebami, za pomocą tych szablonów.</span><span class="sxs-lookup"><span data-stu-id="deb20-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="deb20-106">Szablony w tej sekcji umożliwiają dostosowanie zawartości stron problem w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="deb20-106">The templates in this section allow you to customize the content of the Issue pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="deb20-107">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="deb20-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="deb20-108">Przykładowe domyślnych szablonów znajdują się w następującej dokumentacji, ale mogą ulec zmianie z powodu ciągłe ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="deb20-108">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="deb20-109">Szablonów domyślnych na żywo można wyświetlić w portalu dla deweloperów, przechodząc do żądanego szablony osobno.</span><span class="sxs-lookup"><span data-stu-id="deb20-109">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="deb20-110">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [dostosowywaniu portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="deb20-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="deb20-111"><a name="IssueList"></a>Lista problemów</span><span class="sxs-lookup"><span data-stu-id="deb20-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="deb20-112">**Lista problemów** szablonu umożliwia dostosowanie treści strony listy problem w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="deb20-112">The **Issue list** template allows you to customize the body of the issue list page in the developer portal.</span></span>  
  
 <span data-ttu-id="deb20-113">![Wystawiać portalu dla deweloperów listy](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM problem listy Developer Portal.")</span><span class="sxs-lookup"><span data-stu-id="deb20-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="deb20-114">Szablon domyślny</span><span class="sxs-lookup"><span data-stu-id="deb20-114">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-md-9">  
    <h2>{% localized "IssuesStrings|WebIssuesIndexTitle" %}</h2>  
  </div>  
</div>  
<div class="row">  
  <div class="col-md-12">  
    {% if issues.size > 0 %}  
    <ul class="list-unstyled">  
      {% capture reportedBy %}{% localized "IssuesStrings|WebIssuesStatusReportedBy" %}{% endcapture %}  
      {% assign replaceString0 = '{0}' %}  
      {% assign replaceString1 = '{1}' %}  
      {% for issue in issues %}  
      <li>  
        <h3>  
          <a href="/issues/{{issue.id}}">{{issue.title}}</a>  
        </h3>  
        <p>{{issue.description}}</p>  
        <em>  
          {% capture state %}{{issue.issueState}}{% endcapture %}  
          {% capture devName %}{{issue.subscriptionDeveloperName}}{% endcapture %}  
          {% capture str1 %}{{ reportedBy | replace : replaceString0, state }}{% endcapture %}  
          {{ str1 | replace : replaceString1, devName }}  
          <span class="UtcDateElement">{{ issue.reportedOn | date: "r" }}</span>  
        </em>  
      </li>  
      {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    {% if canReportIssue %}  
    <a class="btn btn-primary" id="createIssue" href="/Issues/Create">{% localized "IssuesStrings|WebIssuesReportIssueButton" %}</a>  
    {% elsif isAuthenticated %}  
    <hr />  
    <p>{% localized "IssuesStrings|WebIssuesNoActiveSubscriptions" %}</p>  
    {% else %}  
    <hr />  
    <p>  
      {% capture signIntext %}{% localized "IssuesStrings|WebIssuesNotSignin" %}{% endcapture %}  
      {% capture link %}<a href="/signin">{% localized "IssuesStrings|WebIssuesSignIn" %}</a>{% endcapture %}  
      {{ signIntext | replace : replaceString0, link }}  
    </p>  
    {% endif %}  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="deb20-115">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="deb20-115">Controls</span></span>  
 <span data-ttu-id="deb20-116">`Issue list` Szablonu może korzystać z następujących [strony kontrolki](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="deb20-116">The `Issue list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="deb20-117">Formant stronicowania</span><span class="sxs-lookup"><span data-stu-id="deb20-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="deb20-118">Model danych</span><span class="sxs-lookup"><span data-stu-id="deb20-118">Data model</span></span>  
  
|<span data-ttu-id="deb20-119">Właściwość</span><span class="sxs-lookup"><span data-stu-id="deb20-119">Property</span></span>|<span data-ttu-id="deb20-120">Typ</span><span class="sxs-lookup"><span data-stu-id="deb20-120">Type</span></span>|<span data-ttu-id="deb20-121">Opis</span><span class="sxs-lookup"><span data-stu-id="deb20-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="deb20-122">Problemy</span><span class="sxs-lookup"><span data-stu-id="deb20-122">Issues</span></span>|<span data-ttu-id="deb20-123">Kolekcja [problem](api-management-template-data-model-reference.md#Issue) jednostek.</span><span class="sxs-lookup"><span data-stu-id="deb20-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="deb20-124">Problemy widoczne dla bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="deb20-124">The issues visible to the current user.</span></span>|  
|<span data-ttu-id="deb20-125">Stronicowanie</span><span class="sxs-lookup"><span data-stu-id="deb20-125">Paging</span></span>|<span data-ttu-id="deb20-126">[Stronicowanie](api-management-template-data-model-reference.md#Paging) jednostki.</span><span class="sxs-lookup"><span data-stu-id="deb20-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="deb20-127">Informacje o stronicowania dla kolekcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="deb20-127">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="deb20-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="deb20-128">IsAuthenticated</span></span>|<span data-ttu-id="deb20-129">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="deb20-129">boolean</span></span>|<span data-ttu-id="deb20-130">Określa, czy bieżący użytkownik jest zalogowany do portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="deb20-130">Whether the current user is signed-in to the developer portal.</span></span>|  
|<span data-ttu-id="deb20-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="deb20-131">CanReportIssues</span></span>|<span data-ttu-id="deb20-132">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="deb20-132">boolean</span></span>|<span data-ttu-id="deb20-133">Określa, czy bieżący użytkownik ma uprawnienia do pliku problemu.</span><span class="sxs-lookup"><span data-stu-id="deb20-133">Whether the current user has permissions to file an issue.</span></span>|  
|<span data-ttu-id="deb20-134">Wyszukiwanie</span><span class="sxs-lookup"><span data-stu-id="deb20-134">Search</span></span>|<span data-ttu-id="deb20-135">Ciąg</span><span class="sxs-lookup"><span data-stu-id="deb20-135">string</span></span>|<span data-ttu-id="deb20-136">Ta właściwość jest przestarzała i nie powinna być używana.</span><span class="sxs-lookup"><span data-stu-id="deb20-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="deb20-137">Przykładowe dane szablonu</span><span class="sxs-lookup"><span data-stu-id="deb20-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how to connect my application to the API",  
            "Description": "I'm having trouble connecting my application to the backend API.",  
            "SubscriptionDeveloperName": "Clayton",  
            "IssueState": "Proposed",  
            "ReportedOn": "2016-04-04T18:46:35.64",  
            "Comments": null,  
            "Attachments": null,  
            "Services": null  
        }  
    ],  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "IsAuthenticated": true,  
    "CanReportIssue": true,  
    "Search": null  
}  
```

## <a name="next-steps"></a><span data-ttu-id="deb20-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="deb20-138">Next steps</span></span>
<span data-ttu-id="deb20-139">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [dostosowywaniu portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="deb20-139">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>