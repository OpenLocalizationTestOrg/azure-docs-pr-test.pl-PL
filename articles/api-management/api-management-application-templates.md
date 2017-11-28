---
title: "Szablony aaaApplication w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocustomize hello zawartości strony aplikacji hello w portalu dla deweloperów hello w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: f3122c4d-e10e-4cdf-977b-36e8f4133fc8
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: f4dc078be7163b047ca2e640a9065ba9e5ba709e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="5b705-103">Szablony aplikacji w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="5b705-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="5b705-104">Zarządzanie interfejsami API Azure oferuje hello możliwości toocustomize hello zawartości strony portalu dewelopera przy użyciu zestawu szablonów, które skonfigurować ich zawartości.</span><span class="sxs-lookup"><span data-stu-id="5b705-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="5b705-105">Przy użyciu [DotLiquid](http://dotliquidmarkup.org/) edytora składni i hello wybranych przez użytkownika, takie jak [DotLiquid dla projektantów](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), i zestaw udostępnionego zlokalizowane [zasoby ciągu](api-management-template-resources.md#strings), [ Zasoby symbolu](api-management-template-resources.md#glyphs), i [strony kontrolki](api-management-page-controls.md), masz dużą elastyczność tooconfigure hello zawartość stron hello zgodnie z własnymi potrzebami, za pomocą tych szablonów.</span><span class="sxs-lookup"><span data-stu-id="5b705-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="5b705-106">Szablony Hello w tej sekcji pozwalają toocustomize hello zawartość stron aplikacji hello w portalu dla deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="5b705-106">hello templates in this section allow you toocustomize hello content of hello Application pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="5b705-107">Lista aplikacji</span><span class="sxs-lookup"><span data-stu-id="5b705-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="5b705-108">Aplikacji</span><span class="sxs-lookup"><span data-stu-id="5b705-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="5b705-109">Przykładowe domyślnych szablonów znajdują się w następującej dokumentacji hello, ale są toochange podmiotu powodu toocontinuous ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="5b705-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="5b705-110">Hello na żywo domyślnych szablonów można wyświetlić w portalu dla deweloperów hello, przechodząc toohello potrzeby poszczególnych szablonów.</span><span class="sxs-lookup"><span data-stu-id="5b705-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="5b705-111">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [jak toocustomize hello portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="5b705-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="5b705-112"><a name="ProductList"></a>Lista aplikacji</span><span class="sxs-lookup"><span data-stu-id="5b705-112"><a name="ProductList"></a> Application list</span></span>  
 <span data-ttu-id="5b705-113">Witaj **listy aplikacji** szablonu pozwala toocustomize hello treści strony listy aplikacji hello w portalu dla deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="5b705-113">hello **Application list** template allows you toocustomize hello body of hello application list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="5b705-114">![Szablony portalu deweloperów strony listy aplikacji](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM aplikacji listy Developer strony portalu szablonów")</span><span class="sxs-lookup"><span data-stu-id="5b705-114">![Application List Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5b705-115">Szablon domyślny</span><span class="sxs-lookup"><span data-stu-id="5b705-115">Default template</span></span>  
  
```xml  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "AppStrings|WebApplicationsHeader" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if applications.size > 0 %}  
        <ul class="list-unstyled">  
        {% for app in applications %}  
            <li>  
            {% if app.application.icon.url != "" %}  
                <aside>  
                    <a href="/applications/details/{{app.application.id}}"><img src="{{app.application.icon.url}}" alt="App Icon" /></a>  
                </aside>  
            {% endif %}  
                <h3><a href="/applications/details/{{app.application.id}}">{{app.application.title}}</a></h3>  
                {{app.application.description}}  
            </li>     
        {% endfor %}  
        </ul>  
        <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="5b705-116">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="5b705-116">Controls</span></span>  
 <span data-ttu-id="5b705-117">Witaj `Product list` szablonu może używać następujących hello [strony kontrolki](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="5b705-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="5b705-118">Formant stronicowania</span><span class="sxs-lookup"><span data-stu-id="5b705-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="5b705-119">Model danych</span><span class="sxs-lookup"><span data-stu-id="5b705-119">Data model</span></span>  
  
|<span data-ttu-id="5b705-120">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5b705-120">Property</span></span>|<span data-ttu-id="5b705-121">Typ</span><span class="sxs-lookup"><span data-stu-id="5b705-121">Type</span></span>|<span data-ttu-id="5b705-122">Opis</span><span class="sxs-lookup"><span data-stu-id="5b705-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="5b705-123">Stronicowanie</span><span class="sxs-lookup"><span data-stu-id="5b705-123">Paging</span></span>|<span data-ttu-id="5b705-124">[Stronicowanie](api-management-template-data-model-reference.md#Paging) jednostki.</span><span class="sxs-lookup"><span data-stu-id="5b705-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="5b705-125">informacje o Hello stronicowania dla kolekcji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5b705-125">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="5b705-126">Aplikacje</span><span class="sxs-lookup"><span data-stu-id="5b705-126">Applications</span></span>|<span data-ttu-id="5b705-127">Kolekcja [aplikacji](api-management-template-data-model-reference.md#Application) jednostek.</span><span class="sxs-lookup"><span data-stu-id="5b705-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="5b705-128">Witaj aplikacji widoczne toohello bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5b705-128">hello applications visible toohello current user.</span></span>|  
|<span data-ttu-id="5b705-129">CategoryName</span><span class="sxs-lookup"><span data-stu-id="5b705-129">CategoryName</span></span>|<span data-ttu-id="5b705-130">Ciąg</span><span class="sxs-lookup"><span data-stu-id="5b705-130">string</span></span>|<span data-ttu-id="5b705-131">Kategoria Hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5b705-131">hello category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="5b705-132">Przykładowe dane szablonu</span><span class="sxs-lookup"><span data-stu-id="5b705-132">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Applications": [  
        {  
            "Application": {  
                "Id": "5702b96fb16653124c8f9ba8",  
                "Title": "Contoso Calculator",  
                "Description": "A simple online calculator.",  
                "Url": null,  
                "Version": null,  
                "Requirements": "Free application with no requirements.",  
                "State": 2,  
                "RegistrationDate": "2016-04-04T18:59:00",  
                "CategoryId": 5,  
                "DeveloperId": "5702b5b0b16653124c8f9ba4",  
                "Attachments": [  
                    {  
                        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                        "Type": "Icon",  
                        "ContentType": "image/png"  
                    },  
                    {  
                        "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
                        "Type": "Screenshot",  
                        "ContentType": "image/png"  
                    }  
                ],  
                "Icon": {  
                    "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                    "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                    "Type": "Icon",  
                    "ContentType": "image/png"  
                }  
            },  
            "CategoryName": "Finance"  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="5b705-133"><a name="Application"></a>Aplikacji</span><span class="sxs-lookup"><span data-stu-id="5b705-133"><a name="Application"></a> Application</span></span>  
 <span data-ttu-id="5b705-134">Witaj **aplikacji** szablonu pozwala toocustomize hello treści strony aplikacji hello w portalu dla deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="5b705-134">hello **Application** template allows you toocustomize hello body of hello application page in hello developer portal.</span></span>  
  
 <span data-ttu-id="5b705-135">![Szablony portalu strony, Deweloper aplikacji](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM szablony portalu deweloperów strony aplikacji")</span><span class="sxs-lookup"><span data-stu-id="5b705-135">![Application Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5b705-136">Szablon domyślny</span><span class="sxs-lookup"><span data-stu-id="5b705-136">Default template</span></span>  
  
```xml  
<h2>{{title}}</h2>  
{% if icon.url != "" %}  
<aside class="applications_aside">  
  <div class="image-placeholder">  
    <img src="{{icon.url}}" alt="Application Icon" />  
  </div>  
</aside>  
{% endif %}  
  
<article>  
  {% if url != "" %}  
    <a target="_blank" href="{{url}}">{{url}}</a>  
  {% endif %}  
  
  <p>{{description}}</p>  
  
  {% if requirements != null %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsRequirementsHeader" %}</h3>  
  <p>{{requirements}}</p>  
  {% endif %}  
  
  {% if attachments.size > 0 %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsScreenshotsHeader" %}</h3>  
    {% for screenshot in attachments %}  
      {% if screenshot.type != "Icon" %}  
      <a href="{{screenshot.url}}" data-lightbox="example-set">  
          <img src="/Developer/Applications/Thumbnail?url={{screenshot.url}}" alt='{% localized "AppDetailsStrings|WebApplicationsScreenshotAlt" %}' />  
      </a>  
      {% endif %}  
    {% endfor %}  
  {% endif %}  
</article>  
  
```  
  
### <a name="controls"></a><span data-ttu-id="5b705-137">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="5b705-137">Controls</span></span>  
 <span data-ttu-id="5b705-138">Witaj `Application` szablonu nie zezwala na używanie hello [strony kontrolki](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="5b705-138">hello `Application` template does not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="5b705-139">Model danych</span><span class="sxs-lookup"><span data-stu-id="5b705-139">Data model</span></span>  
 <span data-ttu-id="5b705-140">[Aplikacja](api-management-template-data-model-reference.md#Application) jednostki.</span><span class="sxs-lookup"><span data-stu-id="5b705-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="5b705-141">Przykładowe dane szablonu</span><span class="sxs-lookup"><span data-stu-id="5b705-141">Sample template data</span></span>  
  
```json  
{  
    "Id": "5702b96fb16653124c8f9ba8",  
    "Title": "Contoso Calculator",  
    "Description": "A simple online calculator.",  
    "Url": null,  
    "Version": null,  
    "Requirements": "Free application with no requirements.",  
    "State": 2,  
    "RegistrationDate": "2016-04-04T18:59:00",  
    "CategoryId": 5,  
    "DeveloperId": "5702b5b0b16653124c8f9ba4",  
    "Attachments": [  
        {  
            "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
            "Type": "Icon",  
            "ContentType": "image/png"  
        },  
        {  
            "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
            "Type": "Screenshot",  
            "ContentType": "image/png"  
        }  
    ],  
    "Icon": {  
        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
        "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
        "Type": "Icon",  
        "ContentType": "image/png"  
    }  
}  
```

## <a name="next-steps"></a><span data-ttu-id="5b705-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5b705-142">Next steps</span></span>
<span data-ttu-id="5b705-143">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [jak toocustomize hello portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5b705-143">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
