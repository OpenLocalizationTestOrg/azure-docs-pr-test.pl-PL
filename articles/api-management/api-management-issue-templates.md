---
title: "Szablony aaaIssue w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocustomize hello zawartość hello problem stron w portalu dla deweloperów hello w usłudze Azure API Management."
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
ms.openlocfilehash: e12902e52c164f73902a97f15ea550790dfecf1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="78897-103">Szablony problem w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="78897-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="78897-104">Zarządzanie interfejsami API Azure oferuje hello możliwości toocustomize hello zawartości strony portalu dewelopera przy użyciu zestawu szablonów, które skonfigurować ich zawartości.</span><span class="sxs-lookup"><span data-stu-id="78897-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="78897-105">Przy użyciu [DotLiquid](http://dotliquidmarkup.org/) edytora składni i hello wybranych przez użytkownika, takie jak [DotLiquid dla projektantów](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), i zestaw udostępnionego zlokalizowane [zasoby ciągu](api-management-template-resources.md#strings), [ Zasoby symbolu](api-management-template-resources.md#glyphs), i [strony kontrolki](api-management-page-controls.md), masz dużą elastyczność tooconfigure hello zawartość stron hello zgodnie z własnymi potrzebami, za pomocą tych szablonów.</span><span class="sxs-lookup"><span data-stu-id="78897-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="78897-106">Szablony Hello w tej sekcji pozwalają toocustomize zawartość hello hello problem stron w portalu dla deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="78897-106">hello templates in this section allow you toocustomize hello content of hello Issue pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="78897-107">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="78897-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="78897-108">Przykładowe domyślnych szablonów znajdują się w następującej dokumentacji hello, ale są toochange podmiotu powodu toocontinuous ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="78897-108">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="78897-109">Hello na żywo domyślnych szablonów można wyświetlić w portalu dla deweloperów hello, przechodząc toohello potrzeby poszczególnych szablonów.</span><span class="sxs-lookup"><span data-stu-id="78897-109">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="78897-110">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [jak toocustomize hello portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="78897-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="78897-111"><a name="IssueList"></a>Lista problemów</span><span class="sxs-lookup"><span data-stu-id="78897-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="78897-112">Witaj **Lista problemów** szablonu pozwala toocustomize treści hello hello problem listy strony w portalu dla deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="78897-112">hello **Issue list** template allows you toocustomize hello body of hello issue list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="78897-113">![Wystawiać portalu dla deweloperów listy](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM problem listy Developer Portal.")</span><span class="sxs-lookup"><span data-stu-id="78897-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="78897-114">Szablon domyślny</span><span class="sxs-lookup"><span data-stu-id="78897-114">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="78897-115">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="78897-115">Controls</span></span>  
 <span data-ttu-id="78897-116">Witaj `Issue list` szablonu może używać następujących hello [strony kontrolki](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="78897-116">hello `Issue list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="78897-117">Formant stronicowania</span><span class="sxs-lookup"><span data-stu-id="78897-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="78897-118">Model danych</span><span class="sxs-lookup"><span data-stu-id="78897-118">Data model</span></span>  
  
|<span data-ttu-id="78897-119">Właściwość</span><span class="sxs-lookup"><span data-stu-id="78897-119">Property</span></span>|<span data-ttu-id="78897-120">Typ</span><span class="sxs-lookup"><span data-stu-id="78897-120">Type</span></span>|<span data-ttu-id="78897-121">Opis</span><span class="sxs-lookup"><span data-stu-id="78897-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="78897-122">Problemy</span><span class="sxs-lookup"><span data-stu-id="78897-122">Issues</span></span>|<span data-ttu-id="78897-123">Kolekcja [problem](api-management-template-data-model-reference.md#Issue) jednostek.</span><span class="sxs-lookup"><span data-stu-id="78897-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="78897-124">Witaj problemów widoczne toohello bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="78897-124">hello issues visible toohello current user.</span></span>|  
|<span data-ttu-id="78897-125">Stronicowanie</span><span class="sxs-lookup"><span data-stu-id="78897-125">Paging</span></span>|<span data-ttu-id="78897-126">[Stronicowanie](api-management-template-data-model-reference.md#Paging) jednostki.</span><span class="sxs-lookup"><span data-stu-id="78897-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="78897-127">informacje o Hello stronicowania dla kolekcji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="78897-127">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="78897-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="78897-128">IsAuthenticated</span></span>|<span data-ttu-id="78897-129">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="78897-129">boolean</span></span>|<span data-ttu-id="78897-130">Określa, czy hello bieżący użytkownik jest zalogowany toohello portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="78897-130">Whether hello current user is signed-in toohello developer portal.</span></span>|  
|<span data-ttu-id="78897-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="78897-131">CanReportIssues</span></span>|<span data-ttu-id="78897-132">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="78897-132">boolean</span></span>|<span data-ttu-id="78897-133">Określa, czy hello bieżący użytkownik nie ma uprawnień toofile problemu.</span><span class="sxs-lookup"><span data-stu-id="78897-133">Whether hello current user has permissions toofile an issue.</span></span>|  
|<span data-ttu-id="78897-134">Wyszukiwanie</span><span class="sxs-lookup"><span data-stu-id="78897-134">Search</span></span>|<span data-ttu-id="78897-135">Ciąg</span><span class="sxs-lookup"><span data-stu-id="78897-135">string</span></span>|<span data-ttu-id="78897-136">Ta właściwość jest przestarzała i nie powinna być używana.</span><span class="sxs-lookup"><span data-stu-id="78897-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="78897-137">Przykładowe dane szablonu</span><span class="sxs-lookup"><span data-stu-id="78897-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how tooconnect my application toohello API",  
            "Description": "I'm having trouble connecting my application toohello backend API.",  
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

## <a name="next-steps"></a><span data-ttu-id="78897-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="78897-138">Next steps</span></span>
<span data-ttu-id="78897-139">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [jak toocustomize hello portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="78897-139">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
