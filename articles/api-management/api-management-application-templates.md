---
title: "Szablony aplikacji w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dostosować zawartość strony aplikacji w portalu dla deweloperów w usłudze Azure API Management."
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
ms.openlocfilehash: 6d2d44465800219f16866a621d4822614ac9e1dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="6337b-103">Szablony aplikacji w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="6337b-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="6337b-104">Zarządzanie interfejsami API Azure zapewnia możliwość dostosować zawartość strony portalu dewelopera przy użyciu zestawu szablonów, które skonfigurować ich zawartości.</span><span class="sxs-lookup"><span data-stu-id="6337b-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="6337b-105">Przy użyciu [DotLiquid](http://dotliquidmarkup.org/) składni i Edytor wybranych przez użytkownika, takie jak [DotLiquid dla projektantów](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), i zestaw udostępnionego zlokalizowane [zasoby ciągu](api-management-template-resources.md#strings), [symboli zasobów](api-management-template-resources.md#glyphs), i [strony kontrolki](api-management-page-controls.md), ma dużą elastyczność konfigurowania zawartości stron, zgodnie z własnymi potrzebami, za pomocą tych szablonów.</span><span class="sxs-lookup"><span data-stu-id="6337b-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="6337b-106">Szablony w tej sekcji umożliwiają dostosowanie zawartości strony aplikacji w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="6337b-106">The templates in this section allow you to customize the content of the Application pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="6337b-107">Lista aplikacji</span><span class="sxs-lookup"><span data-stu-id="6337b-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="6337b-108">Aplikacji</span><span class="sxs-lookup"><span data-stu-id="6337b-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="6337b-109">Przykładowe domyślnych szablonów znajdują się w następującej dokumentacji, ale mogą ulec zmianie z powodu ciągłe ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="6337b-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="6337b-110">Szablonów domyślnych na żywo można wyświetlić w portalu dla deweloperów, przechodząc do żądanego szablony osobno.</span><span class="sxs-lookup"><span data-stu-id="6337b-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="6337b-111">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [dostosowywaniu portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="6337b-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="6337b-112"><a name="ProductList"></a>Lista aplikacji</span><span class="sxs-lookup"><span data-stu-id="6337b-112"><a name="ProductList"></a> Application list</span></span>  
 <span data-ttu-id="6337b-113">**Listy aplikacji** szablonu umożliwia dostosowanie treści strony listy aplikacji w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="6337b-113">The **Application list** template allows you to customize the body of the application list page in the developer portal.</span></span>  
  
 <span data-ttu-id="6337b-114">![Szablony portalu deweloperów strony listy aplikacji](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM aplikacji listy Developer strony portalu szablonów")</span><span class="sxs-lookup"><span data-stu-id="6337b-114">![Application List Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="6337b-115">Szablon domyślny</span><span class="sxs-lookup"><span data-stu-id="6337b-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="6337b-116">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="6337b-116">Controls</span></span>  
 <span data-ttu-id="6337b-117">`Product list` Szablonu może korzystać z następujących [strony kontrolki](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="6337b-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="6337b-118">Formant stronicowania</span><span class="sxs-lookup"><span data-stu-id="6337b-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="6337b-119">Model danych</span><span class="sxs-lookup"><span data-stu-id="6337b-119">Data model</span></span>  
  
|<span data-ttu-id="6337b-120">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6337b-120">Property</span></span>|<span data-ttu-id="6337b-121">Typ</span><span class="sxs-lookup"><span data-stu-id="6337b-121">Type</span></span>|<span data-ttu-id="6337b-122">Opis</span><span class="sxs-lookup"><span data-stu-id="6337b-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="6337b-123">Stronicowanie</span><span class="sxs-lookup"><span data-stu-id="6337b-123">Paging</span></span>|<span data-ttu-id="6337b-124">[Stronicowanie](api-management-template-data-model-reference.md#Paging) jednostki.</span><span class="sxs-lookup"><span data-stu-id="6337b-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="6337b-125">Informacje o stronicowania dla kolekcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6337b-125">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="6337b-126">Aplikacje</span><span class="sxs-lookup"><span data-stu-id="6337b-126">Applications</span></span>|<span data-ttu-id="6337b-127">Kolekcja [aplikacji](api-management-template-data-model-reference.md#Application) jednostek.</span><span class="sxs-lookup"><span data-stu-id="6337b-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="6337b-128">Aplikacje są widoczne dla bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6337b-128">The applications visible to the current user.</span></span>|  
|<span data-ttu-id="6337b-129">CategoryName</span><span class="sxs-lookup"><span data-stu-id="6337b-129">CategoryName</span></span>|<span data-ttu-id="6337b-130">Ciąg</span><span class="sxs-lookup"><span data-stu-id="6337b-130">string</span></span>|<span data-ttu-id="6337b-131">Kategoria aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6337b-131">The category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="6337b-132">Przykładowe dane szablonu</span><span class="sxs-lookup"><span data-stu-id="6337b-132">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="6337b-133"><a name="Application"></a>Aplikacji</span><span class="sxs-lookup"><span data-stu-id="6337b-133"><a name="Application"></a> Application</span></span>  
 <span data-ttu-id="6337b-134">**Aplikacji** szablonu umożliwia dostosowanie treści strony aplikacji w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="6337b-134">The **Application** template allows you to customize the body of the application page in the developer portal.</span></span>  
  
 <span data-ttu-id="6337b-135">![Szablony portalu strony, Deweloper aplikacji](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM szablony portalu deweloperów strony aplikacji")</span><span class="sxs-lookup"><span data-stu-id="6337b-135">![Application Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="6337b-136">Szablon domyślny</span><span class="sxs-lookup"><span data-stu-id="6337b-136">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="6337b-137">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="6337b-137">Controls</span></span>  
 <span data-ttu-id="6337b-138">`Application` Szablonu nie zezwala na używanie [strony kontrolki](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="6337b-138">The `Application` template does not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="6337b-139">Model danych</span><span class="sxs-lookup"><span data-stu-id="6337b-139">Data model</span></span>  
 <span data-ttu-id="6337b-140">[Aplikacja](api-management-template-data-model-reference.md#Application) jednostki.</span><span class="sxs-lookup"><span data-stu-id="6337b-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="6337b-141">Przykładowe dane szablonu</span><span class="sxs-lookup"><span data-stu-id="6337b-141">Sample template data</span></span>  
  
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

## <a name="next-steps"></a><span data-ttu-id="6337b-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6337b-142">Next steps</span></span>
<span data-ttu-id="6337b-143">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [dostosowywaniu portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6337b-143">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>