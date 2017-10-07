---
title: "aaaHow toocreate i publikować w usłudze Azure API Management produktu"
description: "Dowiedz się, jak toocreate i publikować w usłudze Azure API Management produktów."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a>Jak toocreate i publikować w usłudze Azure API Management produktu
W systemie Azure API Management produkt zawiera jeden lub więcej interfejsów API, jak również użycie przydziału i hello warunki użytkowania. Po opublikowaniu produktu deweloperzy mogą subskrypcji toohello produktu i rozpocząć interfejsów API toouse hello produktu. temat Hello zawiera toocreating przewodnik produktu, dodawanie interfejsu API i publikowania dla deweloperów.

## <a name="create-product"></a>Tworzenie produktu
Operacje są dodawane i tooan interfejsu API w portalu wydawcy hello. tooaccess hello wydawcy portalu, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API.

![Portal wydawcy][api-management-management-console]

> Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.
> 
> 

Polecenie **produktów** w menu hello na powitania po lewej stronie toodisplay hello **produktów** , a następnie kliknij przycisk **Dodaj produkt**.

![Produkty][api-management-products]

![Nowego produktu][api-management-add-new-product]

Wprowadź opisową nazwę produktu hello w hello **nazwa** opis produktu hello hello **opis** pola.

Produkty w usłudze API Management może być **Otwórz** lub **chronione**. Produkty chronione muszą być subskrybowanego toobefore mogą być używane, otwartej produktów może być używany bez subskrypcji. Sprawdź **wymagają subskrypcji** toocreate chronionych produkt, który wymaga subskrypcji. To jest ustawienie domyślne hello.

Sprawdź **wymagają zatwierdzenia subskrypcji** Jeśli chcesz tooreview administratora i zaakceptuj lub Odrzuć subskrypcji prób toothis produktu. Jeśli pole hello jest zaznaczona, prób subskrypcji będą automatycznie zatwierdzone. Aby uzyskać więcej informacji o subskrypcji, zobacz [widoku subskrybentów tooa produktu][View subscribers tooa product].

toosubscribe konta dewelopera tooallow wielokrotnie toohello produktu, sprawdź hello **zezwalać na wiele subskrypcji** pole wyboru. Jeśli to pole nie jest zaznaczone, każdego konta dewelopera można zasubskrybować tylko produkt toohello jeden raz.

![Nieograniczone wiele subskrypcji][api-management-unlimited-multiple-subscriptions]

Liczba hello toolimit wiele równoczesnych subskrypcji, sprawdź hello **Ogranicz liczbę jednoczesnych subskrypcje** pole wyboru, a następnie wprowadź hello limit subskrypcji. W hello poniższy przykład jednoczesnych subskrypcje są ograniczone toofour na konto dewelopera.

![Cztery wiele subskrypcji][api-management-four-multiple-subscriptions]

Po skonfigurowaniu wszystkich nowych opcji produktu, kliknij przycisk **zapisać** toocreate hello nowego produktu.

![Produkty][api-management-products-page]

> Domyślnie są nieopublikowane nowych produktów i są widoczne tylko toohello **Administratorzy** grupy.
> 
> 

Kliknij tooconfigure produktu, nazwa produktu hello w hello **produktów** kartę.

## <a name="add-apis"></a>Produktu tooa dodać interfejsów API
Witaj **produktów** strona zawiera cztery łącza dla konfiguracji: **Podsumowanie**, **ustawienia**, **widoczność**, i ** Subskrybenci**. Witaj **Podsumowanie** jest karta, którym można dodać interfejsów API i opublikować lub Cofnij publikowanie produktu.

![Podsumowanie][api-management-new-product-summary]

Przed opublikowaniem produktu należy tooadd jeden lub więcej interfejsów API. toodo tego, kliknij **tooproduct dodać interfejsu API**.

![Dodaj interfejsów API][api-management-add-apis-to-product]

Wybierz hello potrzeby interfejsów API i kliknij przycisk **zapisać**.

## <a name="add-description"></a>Dodaj informacje opisowe tooa produktu
Witaj **ustawienia** karta umożliwia tooprovide szczegółowe informacje o produkcie hello, takie jak jego przeznaczenie, hello zapewnia dostęp do interfejsów API i inne przydatne informacje. zawartość Hello jest przeznaczona dla deweloperów hello, będzie wywoływany hello interfejsu API, które mogą być zapisywane w postaci zwykłego tekstu lub kod znaczników HTML.

![Ustawienia produktów][api-management-product-settings]

Sprawdź **wymagają subskrypcji** toocreate chronionych produkt, który wymaga toobe subskrypcji, używane, lub wyczyść pole wyboru hello toocreate wyboru Otwieranie produktu, który można wywołać bez subskrypcji.

Wybierz **wymagają zatwierdzenia subskrypcji** Jeśli chcesz toomanually zatwierdzić wszystkie żądania subskrypcji produktu. Domyślnie wszystkie subskrypcje produktu są przyznawane automatycznie.

toosubscribe konta dewelopera tooallow wielokrotnie toohello produktu, sprawdź hello **zezwalać na wiele subskrypcji** pole wyboru i opcjonalnie Określ limit. Jeśli to pole nie jest zaznaczone, każdego konta dewelopera można zasubskrybować tylko produkt toohello jeden raz.

Opcjonalnie Wypełnij hello **warunki użytkowania** pola opisujące hello warunki użytkowania hello produktu, które zaakceptować subskrybentów w kolejności toouse hello produktu.

## <a name="publish-product"></a>Publikowania produktu
Aby można było wywołać hello interfejsów API w produkcie, musi zostać opublikowany hello produktu. Na powitania **Podsumowanie** hello produktu, kliknij pozycję **publikowania**, a następnie kliknij przycisk **tak, przed opublikowaniem** tooconfirm. toomake prywatnej wydane wcześniej produktu, kliknij przycisk **Cofnij publikowanie**.

![Publikowanie produktu][api-management-publish-product]

## <a name="make-visible"></a>Upewnij toodevelopers widoczne produktu
Witaj **widoczność** karta umożliwia toochoose role są możliwe toosee hello produktu w portalu dla deweloperów hello i subskrybowania toohello produktu.

![Widoczność produktu][api-management-product-visiblity]

widoczność tooenable lub wyłącz produktu dla deweloperów hello w grupie, sprawdź lub usuń zaznaczenie pola wyboru hello obok hello grupy, a następnie kliknij przycisk **zapisać**.

> Aby uzyskać więcej informacji, zobacz [jak developer toomanage grup toocreate i używania kont w usłudze Azure API Management][How toocreate and use groups toomanage developer accounts in Azure API Management].
> 
> 

## <a name="view-subscribers"></a>Widoku subskrybentów tooa produktu
Witaj **subskrybentów** karta zawiera listę hello deweloperów, którzy subskrybowanych toohello produktu. Hello ustawienia dla wszystkich deweloperów i szczegółowe informacje można wyświetlić, klikając nazwę hello developer. W tym przykładzie deweloperzy nie masz jeszcze subskrypcję toohello produktu.

![Deweloperzy][api-management-developer-list]

## <a name="next-steps"> </a>Następne kroki
Raz hello żądana dodano interfejsy API i produktu hello opublikowana, deweloperzy mogą subskrybować toohello produktu i rozpocząć hello toocall interfejsów API. Samouczek przedstawiający tych elementów, a także zaawansowane produktu configuration [jak utworzyć i skonfigurować ustawienia zaawansowane produktu w usłudze Azure API Management][How create and configure advanced product settings in Azure API Management].

Aby uzyskać więcej informacji na temat pracy z produktami Zobacz powitania po wideo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
