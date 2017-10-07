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
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="753b7-103">Jak toocreate i publikować w usłudze Azure API Management produktu</span><span class="sxs-lookup"><span data-stu-id="753b7-103">How toocreate and publish a product in Azure API Management</span></span>
<span data-ttu-id="753b7-104">W systemie Azure API Management produkt zawiera jeden lub więcej interfejsów API, jak również użycie przydziału i hello warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="753b7-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and hello terms of use.</span></span> <span data-ttu-id="753b7-105">Po opublikowaniu produktu deweloperzy mogą subskrypcji toohello produktu i rozpocząć interfejsów API toouse hello produktu.</span><span class="sxs-lookup"><span data-stu-id="753b7-105">Once a product is published, developers can subscribe toohello product and begin toouse hello product's APIs.</span></span> <span data-ttu-id="753b7-106">temat Hello zawiera toocreating przewodnik produktu, dodawanie interfejsu API i publikowania dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="753b7-106">hello topic provides a guide toocreating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="753b7-107"><a name="create-product"></a>Tworzenie produktu</span><span class="sxs-lookup"><span data-stu-id="753b7-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="753b7-108">Operacje są dodawane i tooan interfejsu API w portalu wydawcy hello.</span><span class="sxs-lookup"><span data-stu-id="753b7-108">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="753b7-109">tooaccess hello wydawcy portalu, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="753b7-109">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portal wydawcy][api-management-management-console]

> <span data-ttu-id="753b7-111">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.</span><span class="sxs-lookup"><span data-stu-id="753b7-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="753b7-112">Polecenie **produktów** w menu hello na powitania po lewej stronie toodisplay hello **produktów** , a następnie kliknij przycisk **Dodaj produkt**.</span><span class="sxs-lookup"><span data-stu-id="753b7-112">Click on **Products** in hello menu on hello left toodisplay hello **Products** page, and click **Add Product**.</span></span>

![Produkty][api-management-products]

![Nowego produktu][api-management-add-new-product]

<span data-ttu-id="753b7-115">Wprowadź opisową nazwę produktu hello w hello **nazwa** opis produktu hello hello **opis** pola.</span><span class="sxs-lookup"><span data-stu-id="753b7-115">Enter a descriptive name for hello product in hello **Name** field and a description of hello product in hello **Description** field.</span></span>

<span data-ttu-id="753b7-116">Produkty w usłudze API Management może być **Otwórz** lub **chronione**.</span><span class="sxs-lookup"><span data-stu-id="753b7-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="753b7-117">Produkty chronione muszą być subskrybowanego toobefore mogą być używane, otwartej produktów może być używany bez subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="753b7-117">Protected products must be subscribed toobefore they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="753b7-118">Sprawdź **wymagają subskrypcji** toocreate chronionych produkt, który wymaga subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="753b7-118">Check **Require subscription** toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="753b7-119">To jest ustawienie domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="753b7-119">This is hello default setting.</span></span>

<span data-ttu-id="753b7-120">Sprawdź **wymagają zatwierdzenia subskrypcji** Jeśli chcesz tooreview administratora i zaakceptuj lub Odrzuć subskrypcji prób toothis produktu.</span><span class="sxs-lookup"><span data-stu-id="753b7-120">Check **Require subscription approval** if you want an administrator tooreview and accept or reject subscription attempts toothis product.</span></span> <span data-ttu-id="753b7-121">Jeśli pole hello jest zaznaczona, prób subskrypcji będą automatycznie zatwierdzone.</span><span class="sxs-lookup"><span data-stu-id="753b7-121">If hello box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="753b7-122">Aby uzyskać więcej informacji o subskrypcji, zobacz [widoku subskrybentów tooa produktu][View subscribers tooa product].</span><span class="sxs-lookup"><span data-stu-id="753b7-122">For more information on subscriptions, see [View subscribers tooa product][View subscribers tooa product].</span></span>

<span data-ttu-id="753b7-123">toosubscribe konta dewelopera tooallow wielokrotnie toohello produktu, sprawdź hello **zezwalać na wiele subskrypcji** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="753b7-123">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="753b7-124">Jeśli to pole nie jest zaznaczone, każdego konta dewelopera można zasubskrybować tylko produkt toohello jeden raz.</span><span class="sxs-lookup"><span data-stu-id="753b7-124">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

![Nieograniczone wiele subskrypcji][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="753b7-126">Liczba hello toolimit wiele równoczesnych subskrypcji, sprawdź hello **Ogranicz liczbę jednoczesnych subskrypcje** pole wyboru, a następnie wprowadź hello limit subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="753b7-126">toolimit hello count of multiple simultaneous subscriptions, check hello **Limit number of simultaneous subscriptions to** check box and enter hello subscription limit.</span></span> <span data-ttu-id="753b7-127">W hello poniższy przykład jednoczesnych subskrypcje są ograniczone toofour na konto dewelopera.</span><span class="sxs-lookup"><span data-stu-id="753b7-127">In hello following example, simultaneous subscriptions are limited toofour per developer account.</span></span>

![Cztery wiele subskrypcji][api-management-four-multiple-subscriptions]

<span data-ttu-id="753b7-129">Po skonfigurowaniu wszystkich nowych opcji produktu, kliknij przycisk **zapisać** toocreate hello nowego produktu.</span><span class="sxs-lookup"><span data-stu-id="753b7-129">Once all new product options are configured, click **Save** toocreate hello new product.</span></span>

![Produkty][api-management-products-page]

> <span data-ttu-id="753b7-131">Domyślnie są nieopublikowane nowych produktów i są widoczne tylko toohello **Administratorzy** grupy.</span><span class="sxs-lookup"><span data-stu-id="753b7-131">By default new products are unpublished, and are visible only toohello  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="753b7-132">Kliknij tooconfigure produktu, nazwa produktu hello w hello **produktów** kartę.</span><span class="sxs-lookup"><span data-stu-id="753b7-132">tooconfigure a product, click on hello product name in hello **Products** tab.</span></span>

## <span data-ttu-id="753b7-133"><a name="add-apis"></a>Produktu tooa dodać interfejsów API</span><span class="sxs-lookup"><span data-stu-id="753b7-133"><a name="add-apis"> </a>Add APIs tooa product</span></span>
<span data-ttu-id="753b7-134">Witaj **produktów** strona zawiera cztery łącza dla konfiguracji: **Podsumowanie**, **ustawienia**, **widoczność**, i ** Subskrybenci**.</span><span class="sxs-lookup"><span data-stu-id="753b7-134">hello **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="753b7-135">Witaj **Podsumowanie** jest karta, którym można dodać interfejsów API i opublikować lub Cofnij publikowanie produktu.</span><span class="sxs-lookup"><span data-stu-id="753b7-135">hello **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![Podsumowanie][api-management-new-product-summary]

<span data-ttu-id="753b7-137">Przed opublikowaniem produktu należy tooadd jeden lub więcej interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="753b7-137">Before publishing your product you need tooadd one or more APIs.</span></span> <span data-ttu-id="753b7-138">toodo tego, kliknij **tooproduct dodać interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="753b7-138">toodo this, click **Add API tooproduct**.</span></span>

![Dodaj interfejsów API][api-management-add-apis-to-product]

<span data-ttu-id="753b7-140">Wybierz hello potrzeby interfejsów API i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="753b7-140">Select hello desired APIs and click **Save**.</span></span>

## <span data-ttu-id="753b7-141"><a name="add-description"></a>Dodaj informacje opisowe tooa produktu</span><span class="sxs-lookup"><span data-stu-id="753b7-141"><a name="add-description"> </a>Add descriptive information tooa product</span></span>
<span data-ttu-id="753b7-142">Witaj **ustawienia** karta umożliwia tooprovide szczegółowe informacje o produkcie hello, takie jak jego przeznaczenie, hello zapewnia dostęp do interfejsów API i inne przydatne informacje.</span><span class="sxs-lookup"><span data-stu-id="753b7-142">hello **Settings** tab allows you tooprovide detailed information about hello product such as its purpose, hello APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="753b7-143">zawartość Hello jest przeznaczona dla deweloperów hello, będzie wywoływany hello interfejsu API, które mogą być zapisywane w postaci zwykłego tekstu lub kod znaczników HTML.</span><span class="sxs-lookup"><span data-stu-id="753b7-143">hello content is targeted at hello developers that will be calling hello API and can be written in plain text or HTML markup.</span></span>

![Ustawienia produktów][api-management-product-settings]

<span data-ttu-id="753b7-145">Sprawdź **wymagają subskrypcji** toocreate chronionych produkt, który wymaga toobe subskrypcji, używane, lub wyczyść pole wyboru hello toocreate wyboru Otwieranie produktu, który można wywołać bez subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="753b7-145">Check **Require subscription** toocreate a protected product that requires a subscription toobe used, or clear hello checkbox toocreate an open product that can be called without a subscription.</span></span>

<span data-ttu-id="753b7-146">Wybierz **wymagają zatwierdzenia subskrypcji** Jeśli chcesz toomanually zatwierdzić wszystkie żądania subskrypcji produktu.</span><span class="sxs-lookup"><span data-stu-id="753b7-146">Select **Require subscription approval** if you want toomanually approve all product subscription requests.</span></span> <span data-ttu-id="753b7-147">Domyślnie wszystkie subskrypcje produktu są przyznawane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="753b7-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="753b7-148">toosubscribe konta dewelopera tooallow wielokrotnie toohello produktu, sprawdź hello **zezwalać na wiele subskrypcji** pole wyboru i opcjonalnie Określ limit.</span><span class="sxs-lookup"><span data-stu-id="753b7-148">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="753b7-149">Jeśli to pole nie jest zaznaczone, każdego konta dewelopera można zasubskrybować tylko produkt toohello jeden raz.</span><span class="sxs-lookup"><span data-stu-id="753b7-149">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

<span data-ttu-id="753b7-150">Opcjonalnie Wypełnij hello **warunki użytkowania** pola opisujące hello warunki użytkowania hello produktu, które zaakceptować subskrybentów w kolejności toouse hello produktu.</span><span class="sxs-lookup"><span data-stu-id="753b7-150">Optionally fill in hello **Terms of use** field describing hello terms of use for hello product which subscribers must accept in order toouse hello product.</span></span>

## <span data-ttu-id="753b7-151"><a name="publish-product"></a>Publikowania produktu</span><span class="sxs-lookup"><span data-stu-id="753b7-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="753b7-152">Aby można było wywołać hello interfejsów API w produkcie, musi zostać opublikowany hello produktu.</span><span class="sxs-lookup"><span data-stu-id="753b7-152">Before hello APIs in a product can be called, hello product must be published.</span></span> <span data-ttu-id="753b7-153">Na powitania **Podsumowanie** hello produktu, kliknij pozycję **publikowania**, a następnie kliknij przycisk **tak, przed opublikowaniem** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="753b7-153">On hello **Summary** tab for hello product, click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span> <span data-ttu-id="753b7-154">toomake prywatnej wydane wcześniej produktu, kliknij przycisk **Cofnij publikowanie**.</span><span class="sxs-lookup"><span data-stu-id="753b7-154">toomake a previously published product private, click **Unpublish**.</span></span>

![Publikowanie produktu][api-management-publish-product]

## <span data-ttu-id="753b7-156"><a name="make-visible"></a>Upewnij toodevelopers widoczne produktu</span><span class="sxs-lookup"><span data-stu-id="753b7-156"><a name="make-visible"> </a>Make a product visible toodevelopers</span></span>
<span data-ttu-id="753b7-157">Witaj **widoczność** karta umożliwia toochoose role są możliwe toosee hello produktu w portalu dla deweloperów hello i subskrybowania toohello produktu.</span><span class="sxs-lookup"><span data-stu-id="753b7-157">hello **Visibility** tab allows you toochoose which roles are able toosee hello product on hello developer portal and subscribe toohello product.</span></span>

![Widoczność produktu][api-management-product-visiblity]

<span data-ttu-id="753b7-159">widoczność tooenable lub wyłącz produktu dla deweloperów hello w grupie, sprawdź lub usuń zaznaczenie pola wyboru hello obok hello grupy, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="753b7-159">tooenable or disable visibility of a product for hello developers in a group, check or uncheck hello check box beside hello group and then click **Save**.</span></span>

> <span data-ttu-id="753b7-160">Aby uzyskać więcej informacji, zobacz [jak developer toomanage grup toocreate i używania kont w usłudze Azure API Management][How toocreate and use groups toomanage developer accounts in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="753b7-160">For more information, see [How toocreate and use groups toomanage developer accounts in Azure API Management][How toocreate and use groups toomanage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="753b7-161"><a name="view-subscribers"></a>Widoku subskrybentów tooa produktu</span><span class="sxs-lookup"><span data-stu-id="753b7-161"><a name="view-subscribers"> </a>View subscribers tooa product</span></span>
<span data-ttu-id="753b7-162">Witaj **subskrybentów** karta zawiera listę hello deweloperów, którzy subskrybowanych toohello produktu.</span><span class="sxs-lookup"><span data-stu-id="753b7-162">hello **Subscribers** tab lists hello developers who have subscribed toohello product.</span></span> <span data-ttu-id="753b7-163">Hello ustawienia dla wszystkich deweloperów i szczegółowe informacje można wyświetlić, klikając nazwę hello developer.</span><span class="sxs-lookup"><span data-stu-id="753b7-163">hello details and settings for each developer can be viewed by clicking on hello developer's name.</span></span> <span data-ttu-id="753b7-164">W tym przykładzie deweloperzy nie masz jeszcze subskrypcję toohello produktu.</span><span class="sxs-lookup"><span data-stu-id="753b7-164">In this example no developers have yet subscribed toohello product.</span></span>

![Deweloperzy][api-management-developer-list]

## <span data-ttu-id="753b7-166"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="753b7-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="753b7-167">Raz hello żądana dodano interfejsy API i produktu hello opublikowana, deweloperzy mogą subskrybować toohello produktu i rozpocząć hello toocall interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="753b7-167">Once hello desired APIs are added and hello product published, developers can subscribe toohello product and begin toocall hello APIs.</span></span> <span data-ttu-id="753b7-168">Samouczek przedstawiający tych elementów, a także zaawansowane produktu configuration [jak utworzyć i skonfigurować ustawienia zaawansowane produktu w usłudze Azure API Management][How create and configure advanced product settings in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="753b7-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="753b7-169">Aby uzyskać więcej informacji na temat pracy z produktami Zobacz powitania po wideo.</span><span class="sxs-lookup"><span data-stu-id="753b7-169">For more information about working with products, see hello following video.</span></span>

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
