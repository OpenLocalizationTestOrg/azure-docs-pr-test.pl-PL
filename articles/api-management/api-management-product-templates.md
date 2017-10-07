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
# <a name="product-templates-in-azure-api-management"></a>Szablony produktów w usłudze Azure API Management
Zarządzanie interfejsami API Azure oferuje hello możliwości toocustomize hello zawartości strony portalu dewelopera przy użyciu zestawu szablonów, które skonfigurować ich zawartości. Przy użyciu [DotLiquid](http://dotliquidmarkup.org/) edytora składni i hello wybranych przez użytkownika, takie jak [DotLiquid dla projektantów](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), i zestaw udostępnionego zlokalizowane [zasoby ciągu](api-management-template-resources.md#strings), [ Zasoby symbolu](api-management-template-resources.md#glyphs), i [strony kontrolki](api-management-page-controls.md), masz dużą elastyczność tooconfigure hello zawartość stron hello zgodnie z własnymi potrzebami, za pomocą tych szablonów.  
  
 Szablony Hello w tej sekcji pozwalają toocustomize hello zawartość stron produktu hello w portalu dla deweloperów hello.  
  
-   [Lista produktów](#ProductList)  
  
-   [Produktu](#Product)  
  
> [!NOTE]
>  Przykładowe domyślnych szablonów znajdują się w następującej dokumentacji hello, ale są toochange podmiotu powodu toocontinuous ulepszenia. Hello na żywo domyślnych szablonów można wyświetlić w portalu dla deweloperów hello, przechodząc toohello potrzeby poszczególnych szablonów. Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [jak toocustomize hello portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
##  <a name="ProductList"></a>Lista produktów  
 Witaj **listę produktów** szablonu pozwala toocustomize hello treści strony listy produktów hello w portalu dla deweloperów hello.  
  
 ![Listy produktów](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")  
  
### <a name="default-template"></a>Szablon domyślny  
  
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
  
### <a name="controls"></a>Kontrolki  
 Witaj `Product list` szablonu może używać następujących hello [strony kontrolki](api-management-page-controls.md).  
  
-   [Formant stronicowania](api-management-page-controls.md#paging-control)  
  
-   [formant wyszukiwania](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a>Model danych  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|Stronicowanie|[Stronicowanie](api-management-template-data-model-reference.md#Paging) jednostki.|informacje o stronicowania Hello hello produktów kolekcji.|  
|Filtrowanie|[Filtrowanie](api-management-template-data-model-reference.md#Filtering) jednostki.|Witaj filtrowania dla listy produktów hello strony.|  
|Produkty|Kolekcja [produktu](api-management-template-data-model-reference.md#Product) jednostek.|Witaj produktów widoczne toohello bieżącego użytkownika.|  
  
### <a name="sample-template-data"></a>Przykładowe dane szablonu  
  
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
  
##  <a name="Product"></a>Produktu  
 Witaj **produktu** szablonu pozwala toocustomize treści hello hello produktu strony w portalu dla deweloperów hello.  
  
 ![Strona produktu portalu dewelopera](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")  
  
### <a name="default-template"></a>Szablon domyślny  
  
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
  
### <a name="controls"></a>Kontrolki  
 Witaj `Product list` szablonu może używać następujących hello [strony kontrolki](api-management-page-controls.md).  
  
-   [przycisk subskrypcji](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a>Model danych  
  
|Właściwość|Typ|Opis|  
|--------------|----------|-----------------|  
|Product (Produkt)|[Produktu](api-management-template-data-model-reference.md#Product)|Witaj określony produkt.|  
|IsDeveloperSubscribed|Wartość logiczna|Określa, czy hello bieżący użytkownik jest subskrybowanego toothis produktu.|  
|Parametr SubscriptionState|Numer|Stan Hello hello subskrypcji. Dostępne są następujące stany:<br /><br /> -   `0 - suspended`— Witaj subskrypcji jest zablokowany i hello subskrybenta nie można wywołać wszystkie interfejsy API hello produktu.<br />-   `1 - active`— Witaj subskrypcja jest aktywna.<br />-   `2 - expired`— Witaj subskrypcja osiągnęła daty jego wygaśnięcia i została zdezaktywowana.<br />-   `3 - submitted`— Żądanie subskrypcji hello przez dewelopera hello, ale nie została jeszcze ma zostały zatwierdzone lub odrzucone.<br />-   `4 - rejected`— Witaj subskrypcji żądanie zostało odrzucone przez administratora.<br />-   `5 - cancelled`— Witaj subskrypcja została anulowana przez dewelopera hello lub administratora.|  
|Limity|Tablica|Ta właściwość jest przestarzała i nie powinna być używana.|  
|DelegatedSubscriptionEnabled|Wartość logiczna|Czy [delegowania](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) jest włączony dla tej subskrypcji.|  
|DelegatedSubscriptionUrl|Ciąg|Jeśli delegowanie jest włączone, hello delegowane adres URL subskrypcji.|  
|IsAgreed|Wartość logiczna|Jeśli produkt hello ma warunki, czy hello bieżący użytkownik zgodził się toohello warunki.|  
|Subskrypcje|Kolekcja [Podsumowanie subskrypcji](api-management-template-data-model-reference.md#SubscriptionSummary) jednostek.|Witaj subskrypcje toohello produktu.|  
|Interfejsy API|Kolekcja [interfejsu API](api-management-template-data-model-reference.md#API) jednostek.|interfejsy API Hello w tym produkcie.|  
|CannotAddBecauseSubscriptionNumberLimitReached|Wartość logiczna|Czy hello bieżącego użytkownika jest uprawniona toosubscribe toothis produktu z uwzględnieniem toohello subskrypcji limit.|  
|CannotAddBecauseMultipleSubscriptionsNotAllowed|Wartość logiczna|Określa, czy hello bieżący użytkownik jest kwalifikujących się toosubscribe toothis produktu z uwzględnieniem toomultiple subskrypcje są dozwolone.|  
  
### <a name="sample-template-data"></a>Przykładowe dane szablonu  
  
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

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [jak toocustomize hello portalu dla deweloperów interfejsu API zarządzania za pomocą szablonów](api-management-developer-portal-templates.md).
