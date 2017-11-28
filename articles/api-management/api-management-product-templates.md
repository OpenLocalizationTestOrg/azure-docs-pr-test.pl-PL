---
title: "Szablony aaaProduct w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zawartość hello toocustomize produktu hello stron w portalu dla deweloperów usługi Azure API Management hello."
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
ms.openlocfilehash: 60600299287aad87f9b621782ab5ceb866601d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="5ed94-103">Szablony produktów w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="5ed94-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="5ed94-104">Zarządzanie interfejsami API Azure oferuje hello możliwości toocustomize hello zawartości strony portalu dewelopera przy użyciu zestawu szablonów, które skonfigurować ich zawartości.</span><span class="sxs-lookup"><span data-stu-id="5ed94-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="5ed94-105">Przy użyciu [DotLiquid](http://dotliquidmarkup.org/) edytora składni i hello wybranych przez użytkownika, takie jak [DotLiquid dla projektantów](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), i zestaw udostępnionego zlokalizowane [zasoby ciągu](api-management-template-resources.md#strings), [ Zasoby symbolu](api-management-template-resources.md#glyphs), i [strony kontrolki](api-management-page-controls.md), masz dużą elastyczność tooconfigure hello zawartość stron hello zgodnie z własnymi potrzebami, za pomocą tych szablonów.</span><span class="sxs-lookup"><span data-stu-id="5ed94-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="5ed94-106">Szablony Hello w tej sekcji pozwalają toocustomize hello zawartość stron produktu hello w portalu dla deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="5ed94-106">hello templates in this section allow you toocustomize hello content of hello product pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="5ed94-107">Lista produktów</span><span class="sxs-lookup"><span data-stu-id="5ed94-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="5ed94-108">Produktu</span><span class="sxs-lookup"><span data-stu-id="5ed94-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="5ed94-109">Przykładowe domyślnych szablonów znajdują się w następującej dokumentacji hello, ale są toochange podmiotu powodu toocontinuous ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="5ed94-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="5ed94-110">Hello na żywo domyślnych szablonów można wyświetlić w portalu dla deweloperów hello, przechodząc toohello potrzeby poszczególnych szablonów.</span><span class="sxs-lookup"><span data-stu-id="5ed94-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="5ed94-111">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [jak toocustomize hello portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="5ed94-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="5ed94-112"><a name="ProductList"></a>Lista produktów</span><span class="sxs-lookup"><span data-stu-id="5ed94-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="5ed94-113">Witaj **listę produktów** szablonu pozwala toocustomize hello treści strony listy produktów hello w portalu dla deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="5ed94-113">hello **Product list** template allows you toocustomize hello body of hello product list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="5ed94-114">![Listy produktów](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="5ed94-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5ed94-115">Szablon domyślny</span><span class="sxs-lookup"><span data-stu-id="5ed94-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="5ed94-116">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="5ed94-116">Controls</span></span>  
 <span data-ttu-id="5ed94-117">Witaj `Product list` szablonu może używać następujących hello [strony kontrolki](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="5ed94-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="5ed94-118">Formant stronicowania</span><span class="sxs-lookup"><span data-stu-id="5ed94-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="5ed94-119">formant wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="5ed94-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="5ed94-120">Model danych</span><span class="sxs-lookup"><span data-stu-id="5ed94-120">Data model</span></span>  
  
|<span data-ttu-id="5ed94-121">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5ed94-121">Property</span></span>|<span data-ttu-id="5ed94-122">Typ</span><span class="sxs-lookup"><span data-stu-id="5ed94-122">Type</span></span>|<span data-ttu-id="5ed94-123">Opis</span><span class="sxs-lookup"><span data-stu-id="5ed94-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="5ed94-124">Stronicowanie</span><span class="sxs-lookup"><span data-stu-id="5ed94-124">Paging</span></span>|<span data-ttu-id="5ed94-125">[Stronicowanie](api-management-template-data-model-reference.md#Paging) jednostki.</span><span class="sxs-lookup"><span data-stu-id="5ed94-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="5ed94-126">informacje o stronicowania Hello hello produktów kolekcji.</span><span class="sxs-lookup"><span data-stu-id="5ed94-126">hello paging information for hello products collection.</span></span>|  
|<span data-ttu-id="5ed94-127">Filtrowanie</span><span class="sxs-lookup"><span data-stu-id="5ed94-127">Filtering</span></span>|<span data-ttu-id="5ed94-128">[Filtrowanie](api-management-template-data-model-reference.md#Filtering) jednostki.</span><span class="sxs-lookup"><span data-stu-id="5ed94-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="5ed94-129">Witaj filtrowania dla listy produktów hello strony.</span><span class="sxs-lookup"><span data-stu-id="5ed94-129">hello filtering information for hello products list page.</span></span>|  
|<span data-ttu-id="5ed94-130">Produkty</span><span class="sxs-lookup"><span data-stu-id="5ed94-130">Products</span></span>|<span data-ttu-id="5ed94-131">Kolekcja [produktu](api-management-template-data-model-reference.md#Product) jednostek.</span><span class="sxs-lookup"><span data-stu-id="5ed94-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="5ed94-132">Witaj produktów widoczne toohello bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5ed94-132">hello products visible toohello current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="5ed94-133">Przykładowe dane szablonu</span><span class="sxs-lookup"><span data-stu-id="5ed94-133">Sample template data</span></span>  
  
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
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="5ed94-134"><a name="Product"></a>Produktu</span><span class="sxs-lookup"><span data-stu-id="5ed94-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="5ed94-135">Witaj **produktu** szablonu pozwala toocustomize treści hello hello produktu strony w portalu dla deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="5ed94-135">hello **Product** template allows you toocustomize hello body of hello product page in hello developer portal.</span></span>  
  
 <span data-ttu-id="5ed94-136">![Strona produktu portalu dewelopera](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="5ed94-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5ed94-137">Szablon domyślny</span><span class="sxs-lookup"><span data-stu-id="5ed94-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="5ed94-138">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="5ed94-138">Controls</span></span>  
 <span data-ttu-id="5ed94-139">Witaj `Product list` szablonu może używać następujących hello [strony kontrolki](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="5ed94-139">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="5ed94-140">przycisk subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5ed94-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="5ed94-141">Model danych</span><span class="sxs-lookup"><span data-stu-id="5ed94-141">Data model</span></span>  
  
|<span data-ttu-id="5ed94-142">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5ed94-142">Property</span></span>|<span data-ttu-id="5ed94-143">Typ</span><span class="sxs-lookup"><span data-stu-id="5ed94-143">Type</span></span>|<span data-ttu-id="5ed94-144">Opis</span><span class="sxs-lookup"><span data-stu-id="5ed94-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="5ed94-145">Product (Produkt)</span><span class="sxs-lookup"><span data-stu-id="5ed94-145">Product</span></span>|[<span data-ttu-id="5ed94-146">Produktu</span><span class="sxs-lookup"><span data-stu-id="5ed94-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="5ed94-147">Witaj określony produkt.</span><span class="sxs-lookup"><span data-stu-id="5ed94-147">hello specified product.</span></span>|  
|<span data-ttu-id="5ed94-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="5ed94-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="5ed94-149">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="5ed94-149">boolean</span></span>|<span data-ttu-id="5ed94-150">Określa, czy hello bieżący użytkownik jest subskrybowanego toothis produktu.</span><span class="sxs-lookup"><span data-stu-id="5ed94-150">Whether hello current user is subscribed toothis product.</span></span>|  
|<span data-ttu-id="5ed94-151">Parametr SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="5ed94-151">SubscriptionState</span></span>|<span data-ttu-id="5ed94-152">Numer</span><span class="sxs-lookup"><span data-stu-id="5ed94-152">number</span></span>|<span data-ttu-id="5ed94-153">Stan Hello hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5ed94-153">hello state of hello subscription.</span></span> <span data-ttu-id="5ed94-154">Dostępne są następujące stany:</span><span class="sxs-lookup"><span data-stu-id="5ed94-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="5ed94-155">-   `0 - suspended`— Witaj subskrypcji jest zablokowany i hello subskrybenta nie można wywołać wszystkie interfejsy API hello produktu.</span><span class="sxs-lookup"><span data-stu-id="5ed94-155">-   `0 - suspended` – hello subscription is blocked, and hello subscriber cannot call any APIs of hello product.</span></span><br /><span data-ttu-id="5ed94-156">-   `1 - active`— Witaj subskrypcja jest aktywna.</span><span class="sxs-lookup"><span data-stu-id="5ed94-156">-   `1 - active` – hello subscription is active.</span></span><br /><span data-ttu-id="5ed94-157">-   `2 - expired`— Witaj subskrypcja osiągnęła daty jego wygaśnięcia i została zdezaktywowana.</span><span class="sxs-lookup"><span data-stu-id="5ed94-157">-   `2 - expired` – hello subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="5ed94-158">-   `3 - submitted`— Żądanie subskrypcji hello przez dewelopera hello, ale nie została jeszcze ma zostały zatwierdzone lub odrzucone.</span><span class="sxs-lookup"><span data-stu-id="5ed94-158">-   `3 - submitted` – hello subscription request has been made by hello developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="5ed94-159">-   `4 - rejected`— Witaj subskrypcji żądanie zostało odrzucone przez administratora.</span><span class="sxs-lookup"><span data-stu-id="5ed94-159">-   `4 - rejected` – hello subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="5ed94-160">-   `5 - cancelled`— Witaj subskrypcja została anulowana przez dewelopera hello lub administratora.</span><span class="sxs-lookup"><span data-stu-id="5ed94-160">-   `5 - cancelled` – hello subscription has been cancelled by hello developer or administrator.</span></span>|  
|<span data-ttu-id="5ed94-161">Limity</span><span class="sxs-lookup"><span data-stu-id="5ed94-161">Limits</span></span>|<span data-ttu-id="5ed94-162">Tablica</span><span class="sxs-lookup"><span data-stu-id="5ed94-162">array</span></span>|<span data-ttu-id="5ed94-163">Ta właściwość jest przestarzała i nie powinna być używana.</span><span class="sxs-lookup"><span data-stu-id="5ed94-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="5ed94-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="5ed94-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="5ed94-165">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="5ed94-165">boolean</span></span>|<span data-ttu-id="5ed94-166">Czy [delegowania](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) jest włączony dla tej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5ed94-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="5ed94-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="5ed94-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="5ed94-168">Ciąg</span><span class="sxs-lookup"><span data-stu-id="5ed94-168">string</span></span>|<span data-ttu-id="5ed94-169">Jeśli delegowanie jest włączone, hello delegowane adres URL subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5ed94-169">If delegation is enabled, hello delegated subscription URL.</span></span>|  
|<span data-ttu-id="5ed94-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="5ed94-170">IsAgreed</span></span>|<span data-ttu-id="5ed94-171">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="5ed94-171">boolean</span></span>|<span data-ttu-id="5ed94-172">Jeśli produkt hello ma warunki, czy hello bieżący użytkownik zgodził się toohello warunki.</span><span class="sxs-lookup"><span data-stu-id="5ed94-172">If hello product has terms, whether hello current user has agreed toohello terms.</span></span>|  
|<span data-ttu-id="5ed94-173">Subskrypcje</span><span class="sxs-lookup"><span data-stu-id="5ed94-173">Subscriptions</span></span>|<span data-ttu-id="5ed94-174">Kolekcja [Podsumowanie subskrypcji](api-management-template-data-model-reference.md#SubscriptionSummary) jednostek.</span><span class="sxs-lookup"><span data-stu-id="5ed94-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="5ed94-175">Witaj subskrypcje toohello produktu.</span><span class="sxs-lookup"><span data-stu-id="5ed94-175">hello subscriptions toohello product.</span></span>|  
|<span data-ttu-id="5ed94-176">Interfejsy API</span><span class="sxs-lookup"><span data-stu-id="5ed94-176">Apis</span></span>|<span data-ttu-id="5ed94-177">Kolekcja [interfejsu API](api-management-template-data-model-reference.md#API) jednostek.</span><span class="sxs-lookup"><span data-stu-id="5ed94-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="5ed94-178">interfejsy API Hello w tym produkcie.</span><span class="sxs-lookup"><span data-stu-id="5ed94-178">hello APIs in this product.</span></span>|  
|<span data-ttu-id="5ed94-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="5ed94-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="5ed94-180">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="5ed94-180">boolean</span></span>|<span data-ttu-id="5ed94-181">Czy hello bieżącego użytkownika jest uprawniona toosubscribe toothis produktu z uwzględnieniem toohello subskrypcji limit.</span><span class="sxs-lookup"><span data-stu-id="5ed94-181">Whether hello current user is eligible toosubscribe toothis product with regard toohello subscription limit.</span></span>|  
|<span data-ttu-id="5ed94-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="5ed94-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="5ed94-183">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="5ed94-183">boolean</span></span>|<span data-ttu-id="5ed94-184">Określa, czy hello bieżący użytkownik jest kwalifikujących się toosubscribe toothis produktu z uwzględnieniem toomultiple subskrypcje są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="5ed94-184">Whether hello current user is eligible toosubscribe toothis product with regard toomultiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="5ed94-185">Przykładowe dane szablonu</span><span class="sxs-lookup"><span data-stu-id="5ed94-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
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

## <a name="next-steps"></a><span data-ttu-id="5ed94-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5ed94-186">Next steps</span></span>
<span data-ttu-id="5ed94-187">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [jak toocustomize hello portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5ed94-187">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
