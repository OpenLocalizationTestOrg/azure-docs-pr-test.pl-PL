---
title: "Szablony produktów w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dostosować zawartość stron produktu w portalu dla deweloperów usługi Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 49f9254c-4c5f-4ed4-9c8d-798f44e805ee
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 9ddbb9860b437cb3e7334bdf5891f2fba1cffb76
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="3e24f-103">Szablony produktów w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="3e24f-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="3e24f-104">Zarządzanie interfejsami API Azure zapewnia możliwość dostosować zawartość strony portalu dewelopera przy użyciu zestawu szablonów, które skonfigurować ich zawartości.</span><span class="sxs-lookup"><span data-stu-id="3e24f-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="3e24f-105">Przy użyciu [DotLiquid](http://dotliquidmarkup.org/) składni i Edytor wybranych przez użytkownika, takie jak [DotLiquid dla projektantów](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), i zestaw udostępnionego zlokalizowane [zasoby ciągu](api-management-template-resources.md#strings), [symboli zasobów](api-management-template-resources.md#glyphs), i [strony kontrolki](api-management-page-controls.md), ma dużą elastyczność konfigurowania zawartości stron, zgodnie z własnymi potrzebami, za pomocą tych szablonów.</span><span class="sxs-lookup"><span data-stu-id="3e24f-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="3e24f-106">Szablony w tej sekcji umożliwiają dostosowanie zawartości stron produktu w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="3e24f-106">The templates in this section allow you to customize the content of the product pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="3e24f-107">Lista produktów</span><span class="sxs-lookup"><span data-stu-id="3e24f-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="3e24f-108">Produktu</span><span class="sxs-lookup"><span data-stu-id="3e24f-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="3e24f-109">Przykładowe domyślnych szablonów znajdują się w następującej dokumentacji, ale mogą ulec zmianie z powodu ciągłe ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="3e24f-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="3e24f-110">Szablonów domyślnych na żywo można wyświetlić w portalu dla deweloperów, przechodząc do żądanego szablony osobno.</span><span class="sxs-lookup"><span data-stu-id="3e24f-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="3e24f-111">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [dostosowywaniu portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="3e24f-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="3e24f-112"><a name="ProductList"></a>Lista produktów</span><span class="sxs-lookup"><span data-stu-id="3e24f-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="3e24f-113">**Listę produktów** szablonu umożliwia dostosowanie treści strony listy produktów w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="3e24f-113">The **Product list** template allows you to customize the body of the product list page in the developer portal.</span></span>  
  
 <span data-ttu-id="3e24f-114">![Listy produktów](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="3e24f-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="3e24f-115">Szablon domyślny</span><span class="sxs-lookup"><span data-stu-id="3e24f-115">Default template</span></span>  
  
```xml  
<search-control></search-control>  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if products.size > 0 %}  
    <ul class="list-unstyled">  
    {% for product in products %}  
        <li>  
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>  
            {{product.description}}  
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
  
### <a name="controls"></a><span data-ttu-id="3e24f-116">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="3e24f-116">Controls</span></span>  
 <span data-ttu-id="3e24f-117">`Product list` Szablonu może korzystać z następujących [strony kontrolki](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="3e24f-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="3e24f-118">Formant stronicowania</span><span class="sxs-lookup"><span data-stu-id="3e24f-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="3e24f-119">formant wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="3e24f-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="3e24f-120">Model danych</span><span class="sxs-lookup"><span data-stu-id="3e24f-120">Data model</span></span>  
  
|<span data-ttu-id="3e24f-121">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3e24f-121">Property</span></span>|<span data-ttu-id="3e24f-122">Typ</span><span class="sxs-lookup"><span data-stu-id="3e24f-122">Type</span></span>|<span data-ttu-id="3e24f-123">Opis</span><span class="sxs-lookup"><span data-stu-id="3e24f-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="3e24f-124">Stronicowanie</span><span class="sxs-lookup"><span data-stu-id="3e24f-124">Paging</span></span>|<span data-ttu-id="3e24f-125">[Stronicowanie](api-management-template-data-model-reference.md#Paging) jednostki.</span><span class="sxs-lookup"><span data-stu-id="3e24f-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="3e24f-126">Informacje o stronicowania dla kolekcji produktów.</span><span class="sxs-lookup"><span data-stu-id="3e24f-126">The paging information for the products collection.</span></span>|  
|<span data-ttu-id="3e24f-127">Filtrowanie</span><span class="sxs-lookup"><span data-stu-id="3e24f-127">Filtering</span></span>|<span data-ttu-id="3e24f-128">[Filtrowanie](api-management-template-data-model-reference.md#Filtering) jednostki.</span><span class="sxs-lookup"><span data-stu-id="3e24f-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="3e24f-129">Informacje filtrowania dla strony listy produktów.</span><span class="sxs-lookup"><span data-stu-id="3e24f-129">The filtering information for the products list page.</span></span>|  
|<span data-ttu-id="3e24f-130">Produkty</span><span class="sxs-lookup"><span data-stu-id="3e24f-130">Products</span></span>|<span data-ttu-id="3e24f-131">Kolekcja [produktu](api-management-template-data-model-reference.md#Product) jednostek.</span><span class="sxs-lookup"><span data-stu-id="3e24f-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="3e24f-132">Produkty są widoczne dla bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3e24f-132">The products visible to the current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="3e24f-133">Przykładowe dane szablonu</span><span class="sxs-lookup"><span data-stu-id="3e24f-133">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 2,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Filtering": {  
        "Pattern": null,  
        "Placeholder": "Search products"  
    },  
    "Products": [  
        {  
            "Id": "56f9445ffaf7560049060001",  
            "Title": "Starter",  
            "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="3e24f-134"><a name="Product"></a>Produktu</span><span class="sxs-lookup"><span data-stu-id="3e24f-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="3e24f-135">**Produktu** szablonu umożliwia dostosowanie treści strony produktu w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="3e24f-135">The **Product** template allows you to customize the body of the product page in the developer portal.</span></span>  
  
 <span data-ttu-id="3e24f-136">![Strona produktu portalu dewelopera](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="3e24f-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="3e24f-137">Szablon domyślny</span><span class="sxs-lookup"><span data-stu-id="3e24f-137">Default template</span></span>  
  
```xml  
<h2>{{Product.Title}}</h2>  
<p>{{Product.Description}}</p>  
  
{% assign replaceString0 = '{0}' %}  
  
{% if Limits and Limits.size > 0 %}  
<h3>{% localized "ProductDetailsStrings|WebProductsUsageLimitsHeader"%}</h3>  
<ul>  
  {% for limit in Limits %}  
  <li>{{limit.DisplayName}}</li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if apis.size > 0 %}  
<p>  
  <b>  
    {% if apis.size == 1 %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockSingleApisCount" %}{% endcapture %}  
    {% else %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockMultipleApisCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture apisCount %}{{apis.size}}{% endcapture %}  
    {{ apisCountText | replace : replaceString0, apisCount }}  
  </b>  
</p>  
  
<ul>  
  {% for api in Apis %}  
  <li>  
    <a href="/docs/services/{{api.Id}}">{{api.Name}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if subscriptions.size > 0 %}  
<p>  
  <b>  
    {% if subscriptions.size == 1 %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockSingleSubscriptionsCount" %}{% endcapture %}  
    {% else %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockMultipleSubscriptionsCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture subscriptionsCount %}{{subscriptions.size}}{% endcapture %}  
    {{ subscriptionsCountText | replace : replaceString0, subscriptionsCount }}  
  </b>  
</p>  
  
<ul>  
  {% for subscription in subscriptions %}  
  <li>  
    <a href="/developer#{{subscription.Id}}">{{subscription.DisplayName}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
{% if CannotAddBecauseSubscriptionNumberLimitReached %}  
<b>{% localized "ProductDetailsStrings|TextblockSubscriptionLimitReached" %}</b>  
{% elsif CannotAddBecauseMultipleSubscriptionsNotAllowed == false %}  
<subscribe-button></subscribe-button>  
{% endif %}  
```  
  
### <a name="controls"></a><span data-ttu-id="3e24f-138">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="3e24f-138">Controls</span></span>  
 <span data-ttu-id="3e24f-139">`Product list` Szablonu może korzystać z następujących [strony kontrolki](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="3e24f-139">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="3e24f-140">przycisk subskrypcji</span><span class="sxs-lookup"><span data-stu-id="3e24f-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="3e24f-141">Model danych</span><span class="sxs-lookup"><span data-stu-id="3e24f-141">Data model</span></span>  
  
|<span data-ttu-id="3e24f-142">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3e24f-142">Property</span></span>|<span data-ttu-id="3e24f-143">Typ</span><span class="sxs-lookup"><span data-stu-id="3e24f-143">Type</span></span>|<span data-ttu-id="3e24f-144">Opis</span><span class="sxs-lookup"><span data-stu-id="3e24f-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="3e24f-145">Product (Produkt)</span><span class="sxs-lookup"><span data-stu-id="3e24f-145">Product</span></span>|[<span data-ttu-id="3e24f-146">Produktu</span><span class="sxs-lookup"><span data-stu-id="3e24f-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="3e24f-147">Określony produkt.</span><span class="sxs-lookup"><span data-stu-id="3e24f-147">The specified product.</span></span>|  
|<span data-ttu-id="3e24f-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="3e24f-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="3e24f-149">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="3e24f-149">boolean</span></span>|<span data-ttu-id="3e24f-150">Określa, czy bieżący użytkownik jest subskrypcję do tego produktu.</span><span class="sxs-lookup"><span data-stu-id="3e24f-150">Whether the current user is subscribed to this product.</span></span>|  
|<span data-ttu-id="3e24f-151">Parametr SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="3e24f-151">SubscriptionState</span></span>|<span data-ttu-id="3e24f-152">Numer</span><span class="sxs-lookup"><span data-stu-id="3e24f-152">number</span></span>|<span data-ttu-id="3e24f-153">Stan subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3e24f-153">The state of the subscription.</span></span> <span data-ttu-id="3e24f-154">Dostępne są następujące stany:</span><span class="sxs-lookup"><span data-stu-id="3e24f-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="3e24f-155">-   `0 - suspended`— subskrypcji jest zablokowany i subskrybenta nie można wywołać wszystkie interfejsy API produktu.</span><span class="sxs-lookup"><span data-stu-id="3e24f-155">-   `0 - suspended` – the subscription is blocked, and the subscriber cannot call any APIs of the product.</span></span><br /><span data-ttu-id="3e24f-156">-   `1 - active`— Subskrypcja jest aktywna.</span><span class="sxs-lookup"><span data-stu-id="3e24f-156">-   `1 - active` – the subscription is active.</span></span><br /><span data-ttu-id="3e24f-157">-   `2 - expired`— Subskrypcja osiągnęła daty jego wygaśnięcia i została zdezaktywowana.</span><span class="sxs-lookup"><span data-stu-id="3e24f-157">-   `2 - expired` – the subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="3e24f-158">-   `3 - submitted`— Żądanie subskrypcji przez deweloperów, ale ma nie została jeszcze zatwierdzeniu lub odrzuceniu.</span><span class="sxs-lookup"><span data-stu-id="3e24f-158">-   `3 - submitted` – the subscription request has been made by the developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="3e24f-159">-   `4 - rejected`— Żądanie subskrypcji zostało odrzucone przez administratora.</span><span class="sxs-lookup"><span data-stu-id="3e24f-159">-   `4 - rejected` – the subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="3e24f-160">-   `5 - cancelled`— Subskrypcja została anulowana przez dewelopera lub administratora.</span><span class="sxs-lookup"><span data-stu-id="3e24f-160">-   `5 - cancelled` – the subscription has been cancelled by the developer or administrator.</span></span>|  
|<span data-ttu-id="3e24f-161">Limity</span><span class="sxs-lookup"><span data-stu-id="3e24f-161">Limits</span></span>|<span data-ttu-id="3e24f-162">Tablica</span><span class="sxs-lookup"><span data-stu-id="3e24f-162">array</span></span>|<span data-ttu-id="3e24f-163">Ta właściwość jest przestarzała i nie powinna być używana.</span><span class="sxs-lookup"><span data-stu-id="3e24f-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="3e24f-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="3e24f-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="3e24f-165">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="3e24f-165">boolean</span></span>|<span data-ttu-id="3e24f-166">Czy [delegowania](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) jest włączony dla tej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3e24f-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="3e24f-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="3e24f-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="3e24f-168">Ciąg</span><span class="sxs-lookup"><span data-stu-id="3e24f-168">string</span></span>|<span data-ttu-id="3e24f-169">Jeśli delegowanie jest włączone, adres URL subskrypcji delegowanego.</span><span class="sxs-lookup"><span data-stu-id="3e24f-169">If delegation is enabled, the delegated subscription URL.</span></span>|  
|<span data-ttu-id="3e24f-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="3e24f-170">IsAgreed</span></span>|<span data-ttu-id="3e24f-171">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="3e24f-171">boolean</span></span>|<span data-ttu-id="3e24f-172">Jeśli produkt ma warunki, czy bieżący użytkownik zgodził się na warunki.</span><span class="sxs-lookup"><span data-stu-id="3e24f-172">If the product has terms, whether the current user has agreed to the terms.</span></span>|  
|<span data-ttu-id="3e24f-173">Subskrypcje</span><span class="sxs-lookup"><span data-stu-id="3e24f-173">Subscriptions</span></span>|<span data-ttu-id="3e24f-174">Kolekcja [Podsumowanie subskrypcji](api-management-template-data-model-reference.md#SubscriptionSummary) jednostek.</span><span class="sxs-lookup"><span data-stu-id="3e24f-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="3e24f-175">Subskrypcje produktu.</span><span class="sxs-lookup"><span data-stu-id="3e24f-175">The subscriptions to the product.</span></span>|  
|<span data-ttu-id="3e24f-176">Interfejsy API</span><span class="sxs-lookup"><span data-stu-id="3e24f-176">Apis</span></span>|<span data-ttu-id="3e24f-177">Kolekcja [interfejsu API](api-management-template-data-model-reference.md#API) jednostek.</span><span class="sxs-lookup"><span data-stu-id="3e24f-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="3e24f-178">Interfejsy API w tym produkcie.</span><span class="sxs-lookup"><span data-stu-id="3e24f-178">The APIs in this product.</span></span>|  
|<span data-ttu-id="3e24f-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="3e24f-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="3e24f-180">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="3e24f-180">boolean</span></span>|<span data-ttu-id="3e24f-181">Określa, czy bieżący użytkownik nie kwalifikuje się do subskrybowania tego produktu w odniesieniu do limit subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3e24f-181">Whether the current user is eligible to subscribe to this product with regard to the subscription limit.</span></span>|  
|<span data-ttu-id="3e24f-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="3e24f-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="3e24f-183">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="3e24f-183">boolean</span></span>|<span data-ttu-id="3e24f-184">Określa, czy bieżący użytkownik nie kwalifikuje się do subskrybowania tego produktu w odniesieniu do wielu subskrypcji jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="3e24f-184">Whether the current user is eligible to subscribe to this product with regard to multiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="3e24f-185">Przykładowe dane szablonu</span><span class="sxs-lookup"><span data-stu-id="3e24f-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
        "Terms": "",  
        "ProductState": 1,  
        "AllowMultipleSubscriptions": false,  
        "MultipleSubscriptionsCount": 1  
    },  
    "IsDeveloperSubscribed": true,  
    "SubscriptionState": 1,  
    "Limits": [],  
    "DelegatedSubscriptionEnabled": false,  
    "DelegatedSubscriptionUrl": null,  
    "IsAgreed": false,  
    "Subscriptions": [  
        {  
            "Id": "56f9445ffaf7560049070001",  
            "DisplayName": "Starter  (default)"  
        }  
    ],  
    "Apis": [  
        {  
            "id": "56f9445ffaf7560049040001",  
            "name": "Echo API",  
            "description": null,  
            "serviceUrl": "http://echoapi.cloudapp.net/api",  
            "path": "echo",  
            "protocols": [  
                2  
            ],  
            "authenticationSettings": null,  
            "subscriptionKeyParameterNames": null  
        }  
    ],  
    "CannotAddBecauseSubscriptionNumberLimitReached": false,  
    "CannotAddBecauseMultipleSubscriptionsNotAllowed": true  
}  
```

## <a name="next-steps"></a><span data-ttu-id="3e24f-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3e24f-186">Next steps</span></span>
<span data-ttu-id="3e24f-187">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [dostosowywaniu portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3e24f-187">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>