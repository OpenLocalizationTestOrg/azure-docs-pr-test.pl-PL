---
title: "za pomocą szablonów aaaCustomize hello zarządzanie interfejsami API developer portal-Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocustomize hello portalu dla deweloperów usługi Azure API Management za pomocą szablonów."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: a195675b-f7d0-4fc9-90bf-860e6f17ccf7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: b00d5f1534e9466f30ff3920e7aae048feb8b8c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-hello-azure-api-management-developer-portal-using-templates"></a>Jak toocustomize hello portalu dla deweloperów usługi Azure API Management za pomocą szablonów

Istnieją trzy podstawowe sposoby toocustomize hello portalu dla deweloperów usługi Azure API Management:

* [Edytuj zawartość hello strony statyczne i elementy układ strony][modify-content-layout]
* [Aktualizuj style hello używany do elementów strony w portalu dla deweloperów hello][customize-styles]
* [Modyfikowanie szablonów hello używany dla stron wygenerowanych przez hello portal] [ portal-templates] (co omówiono w tym przewodniku)

Szablony są używane toocustomize hello zawartości stron portalu deweloperów generowanych przez system (Dokumentacja interfejsu API, produktów, uwierzytelnianie użytkowników, itp.). Przy użyciu [DotLiquid](http://dotliquidmarkup.org/) składni i podany zestaw zasobów zlokalizowanego ciągu, ikony i formantów strony ma dużą elastyczność tooconfigure hello zawartość stron hello zgodnie z własnymi potrzebami.

## <a name="developer-portal-templates-overview"></a>Przegląd szablonów portalu deweloperów
Edytowanie szablonów jest wykonywane od hello **portalu dla deweloperów** podczas jest zalogowany jako administrator. Brak tooget najpierw otwórz hello portalu Azure i kliknij polecenie **wydawcy portalu** z paska narzędzi usługi hello wystąpienia interfejsu API zarządzania.

![Portal wydawcy][api-management-management-console]

Następnie kliknij polecenie **portalu dla deweloperów** na powitania prawym górnym rogu. 

![Menu portalu dla deweloperów][api-management-developer-portal-menu]

tooaccess hello szablony portalu dla deweloperów, kliknij przycisk hello dostosować ikonę na powitania po lewej stronie toodisplay hello Dostosowywanie menu, a następnie kliknij przycisk **szablony**.

![Szablony portalu dla deweloperów][api-management-customize-menu]

Lista szablonów Hello zostaną wyświetlone różne kategorie obejmujące hello na różnych stronach w portalu dla deweloperów hello szablonów. Każdego szablonu jest inny, ale tooedit kroki hello je i opublikuj zmiany hello są takie same hello. tooedit szablonu, kliknij nazwę hello hello szablonu.

![Szablony portalu dla deweloperów][api-management-templates-menu]

Kliknięcie przycisku szablon ma toohello developer strony portalu, który można dostosować za pomocą tego szablonu. W tym hello przykład **listę produktów** szablonu jest wyświetlany. Witaj **listę produktów** formanty szablonu hello obszar ekranie powitania wskazywanym przez prostokąt hello czerwony. 

![Szablon listy produktów][api-management-developer-portal-templates-overview]

Niektóre szablony, takie jak hello **profilu użytkownika** szablony, dostosować różnych części hello tej samej stronie. 

![Szablony profilów użytkownika][api-management-user-profile-templates]

Edytor powitania dla każdego szablonu portalu dewelopera ma dwie sekcje wyświetlane u dołu hello hello strony. po lewej stronie powitania Wyświetla hello edycji okienku szablonu hello oraz prawej stronie powitania modelu danych hello hello szablonu. 

Szablon Hello edycji okienko zawiera hello kod znaczników, który kontroluje hello wygląd i zachowanie hello odpowiedniej strony w portalu dla deweloperów hello. znaczników Hello w szablonie hello używa hello [DotLiquid](http://dotliquidmarkup.org/) składni. Jeden popularnych edytorem DotLiquid jest [DotLiquid dla projektantów](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers). Szablon toohello wszelkie zmiany wprowadzone podczas edycji są wyświetlane w w czasie rzeczywistym w przeglądarce hello, ale są klienci tooyour nie są widoczne dopóki [zapisać](#to-save-a-template) i [publikowania](#to-publish-a-template) hello szablonu.

![Oznaczenia szablonu][api-management-template]

Witaj **dane szablonu** okienko zawiera przewodnik toohello danych modelu dla hello jednostek, które są dostępne do użycia w określonym szablonie. Ten przewodnik zapewnia wyświetlając hello dane na żywo, które są aktualnie wyświetlane w portalu dla deweloperów hello. Można rozwinąć okienka szablonu hello klikając hello prostokąt w prawym górnym narożniku hello hello **dane szablonu** okienka.

![Model danych szablonu][api-management-template-data]

W poprzednim przykładzie hello są wyświetlane w portalu dla deweloperów hello dwóch produktów, które zostały pobrane z hello dane wyświetlane na powitania **dane szablonu** okienka, jak pokazano w hello poniższy przykład.

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
            "Id": "56ec64c380ed850042060001",
            "Title": "Starter",
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",
            "Terms": "",
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        },
        {
            "Id": "56ec64c380ed850042060002",
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

znaczników Hello w hello **listę produktów** szablonu procesów hello danymi wyjściowymi hello potrzeby tooprovide przez iteracji w kolekcji hello informacji toodisplay produktów i indywidualnych produktów tooeach łącza. Uwaga hello `<search-control>` i `<page-control>` elementy w znaczniku hello. Wyświetlanie hello hello wyszukiwania i stronicowania kontrolki na stronie powitania tych kontroli. `ProductsStrings|PageTitleProducts`Odwołanie do zlokalizowanego ciągu, które zawiera hello jest `h2` tekst nagłówka strony hello. Lista zasobów ciągu, formantów strony i ikony dostępne do użycia w szablonach portalu dla deweloperów, [szablony portalu dewelopera zarządzanie interfejsami API](api-management-developer-portal-templates-reference.md).

```html
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

## <a name="toosave-a-template"></a>toosave szablonu
w edytorze szablonu hello toosave szablonu, kliknij przycisk Zapisz.

![Zapisywanie szablonu][api-management-save-template]

Zapisano zmiany nie są na żywo w portalu dla deweloperów hello, dopóki nie zostaną opublikowane.

## <a name="toopublish-a-template"></a>toopublish szablonu
Zapisane szablony mogą być publikowane pojedynczo, lub wszystkich elementów. toopublish poszczególnych szablonu, kliknij przycisk Publikuj w edytorze szablonu hello.

![Publikowanie szablonu][api-management-publish-template]

Kliknij przycisk **tak** tooconfirm i szablon hello na żywo na powitania portalu dla deweloperów.

![Potwierdź publikowania][api-management-publish-template-confirm]

toopublish wszystkie aktualnie nieopublikowane wersji szablonu, kliknij przycisk **publikowania** hello listy szablonów. Nieopublikowane szablony są oznaczane gwiazdka po hello nazwy szablonu. W tym przykładzie hello **listę produktów** i **produktu** szablony zostały opublikowane.

![Publikowanie szablonów][api-management-publish-templates]

Kliknij przycisk **opublikować dostosowania** tooconfirm.

![Potwierdź publikowania][api-management-publish-customizations]

Nowo opublikowana szablonów zaczynają obowiązywać natychmiast w portalu dla deweloperów hello.

## <a name="toorevert-a-template-toohello-previous-version"></a>toorevert poprzedniej wersji toohello szablonu
toorevert szablonu toohello poprzedniej wersji opublikowanej kliknij przycisk Przywróć w edytorze szablonu hello.

![Przywróć szablonu][api-management-revert-template]

Kliknij przycisk **tak** tooconfirm.

![Upewnij się][api-management-revert-template-confirm]

Witaj poprzednio opublikowanej wersji szablonu jest na żywo w portalu dla deweloperów powitania po hello wycofanie operacji zostało zakończone.

## <a name="toorestore-a-template-toohello-default-version"></a>toorestore wersja domyślna toohello szablonu
Przywracanie szablonów tootheir domyślna wersja jest procesem dwuetapowym. Pierwszy szablony hello musi zostać przywrócona, a następnie przywrócić hello wersji musi zostać opublikowany.

Wersja domyślna toohello jednego szablonu toorestore kliknij przycisk Przywróć w edytorze szablonu hello.

![Przywróć szablonu][api-management-reset-template]

Kliknij przycisk **tak** tooconfirm.

![Upewnij się][api-management-reset-template-confirm]

toorestore wszystkie wersje domyślne tootheir szablony, kliknij przycisk **Przywróć domyślne szablony** na powitania listy szablonów.

![Przywracanie szablonów][api-management-restore-templates]

Witaj szablonach przywróconą należy następnie opublikować pojedynczo lub w całości wykonując kroki hello w [toopublish szablonu](#to-publish-a-template).

## <a name="next-steps"></a>Następne kroki
Aby uzyskać informacje referencyjne dotyczące szablonów portalu dla deweloperów, zasoby ciągów, ikony i formantów strony, zobacz [szablony portalu dewelopera zarządzanie interfejsami API](api-management-developer-portal-templates-reference.md).

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customize-menu]: ./media/api-management-developer-portal-templates/api-management-customize-menu.png
[api-management-templates-menu]: ./media/api-management-developer-portal-templates/api-management-templates-menu.png
[api-management-developer-portal-templates-overview]: ./media/api-management-developer-portal-templates/api-management-developer-portal-templates-overview.png
[api-management-template]: ./media/api-management-developer-portal-templates/api-management-template.png
[api-management-template-data]: ./media/api-management-developer-portal-templates/api-management-template-data.png
[api-management-developer-portal-menu]: ./media/api-management-developer-portal-templates/api-management-developer-portal-menu.png
[api-management-management-console]: ./media/api-management-developer-portal-templates/api-management-management-console.png
[api-management-browse]: ./media/api-management-developer-portal-templates/api-management-browse.png
[api-management-user-profile-templates]: ./media/api-management-developer-portal-templates/api-management-user-profile-templates.png
[api-management-save-template]: ./media/api-management-developer-portal-templates/api-management-save-template.png
[api-management-publish-template]: ./media/api-management-developer-portal-templates/api-management-publish-template.png
[api-management-publish-template-confirm]: ./media/api-management-developer-portal-templates/api-management-publish-template-confirm.png
[api-management-publish-templates]: ./media/api-management-developer-portal-templates/api-management-publish-templates.png
[api-management-publish-customizations]: ./media/api-management-developer-portal-templates/api-management-publish-customizations.png
[api-management-revert-template]: ./media/api-management-developer-portal-templates/api-management-revert-template.png
[api-management-revert-template-confirm]: ./media/api-management-developer-portal-templates/api-management-revert-template-confirm.png
[api-management-reset-template]: ./media/api-management-developer-portal-templates/api-management-reset-template.png
[api-management-reset-template-confirm]: ./media/api-management-developer-portal-templates/api-management-reset-template-confirm.png
[api-management-restore-templates]: ./media/api-management-developer-portal-templates/api-management-restore-templates.png







