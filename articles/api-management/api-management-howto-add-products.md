---
title: "Jak tworzyć i publikować w usłudze Azure API Management produktu"
description: "Dowiedz się, jak tworzyć i publikować w usłudze Azure API Management produktów."
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
ms.openlocfilehash: 73bf4451ba1b71807e22440beecc73a7e8045c5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="793da-103">Jak tworzyć i publikować w usłudze Azure API Management produktu</span><span class="sxs-lookup"><span data-stu-id="793da-103">How to create and publish a product in Azure API Management</span></span>
<span data-ttu-id="793da-104">W systemie Azure API Management produkt zawiera jeden lub więcej interfejsów API, a także przydział użycia i warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="793da-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and the terms of use.</span></span> <span data-ttu-id="793da-105">Po opublikowaniu produktu deweloperzy mogą subskrybować produktu i rozpocząć przy użyciu interfejsów API produktu.</span><span class="sxs-lookup"><span data-stu-id="793da-105">Once a product is published, developers can subscribe to the product and begin to use the product's APIs.</span></span> <span data-ttu-id="793da-106">Temat zawiera przewodnik dotyczący tworzenia produktu, dodawanie interfejsu API i publikowania dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="793da-106">The topic provides a guide to creating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="793da-107"><a name="create-product"></a>Tworzenie produktu</span><span class="sxs-lookup"><span data-stu-id="793da-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="793da-108">Działania są dodawane i skonfigurowane do interfejsu API w portalu wydawcy.</span><span class="sxs-lookup"><span data-stu-id="793da-108">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="793da-109">Aby uzyskać dostęp do portalu wydawcy, kliknij przycisk **portal wydawcy** w portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="793da-109">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portal wydawcy][api-management-management-console]

> <span data-ttu-id="793da-111">Jeśli jeszcze nie masz utworzonego wystąpienia usługi API Management, zobacz [Tworzenie wystąpienia usługi API Management][Create an API Management service instance] w samouczku [Wprowadzenie do usługi Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="793da-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="793da-112">Polecenie **produktów** w menu po lewej stronie, aby wyświetlić **produktów** , a następnie kliknij przycisk **Dodaj produkt**.</span><span class="sxs-lookup"><span data-stu-id="793da-112">Click on **Products** in the menu on the left to display the **Products** page, and click **Add Product**.</span></span>

![Produkty][api-management-products]

![Nowego produktu][api-management-add-new-product]

<span data-ttu-id="793da-115">Wprowadź opisową nazwę produktu w **nazwa** opis produktu w **opis** pola.</span><span class="sxs-lookup"><span data-stu-id="793da-115">Enter a descriptive name for the product in the **Name** field and a description of the product in the **Description** field.</span></span>

<span data-ttu-id="793da-116">Produkty w usłudze API Management może być **Otwórz** lub **chronione**.</span><span class="sxs-lookup"><span data-stu-id="793da-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="793da-117">Produkty chronione trzeba subskrybować przed użyciem, a produkty otwarte mogą być używane bez subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="793da-117">Protected products must be subscribed to before they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="793da-118">Sprawdź **wymagają subskrypcji** do tworzenia chronionej produkt, który wymaga subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="793da-118">Check **Require subscription** to create a protected product that requires a subscription.</span></span> <span data-ttu-id="793da-119">Jest to ustawienie domyślne.</span><span class="sxs-lookup"><span data-stu-id="793da-119">This is the default setting.</span></span>

<span data-ttu-id="793da-120">Sprawdź **wymagają zatwierdzenia subskrypcji** Jeśli chcesz, aby administrator, aby przejrzeć i zaakceptować lub odrzucić prób subskrypcję do tego produktu.</span><span class="sxs-lookup"><span data-stu-id="793da-120">Check **Require subscription approval** if you want an administrator to review and accept or reject subscription attempts to this product.</span></span> <span data-ttu-id="793da-121">Jeśli pole jest zaznaczona, prób subskrypcja będzie automatycznie zatwierdzone.</span><span class="sxs-lookup"><span data-stu-id="793da-121">If the box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="793da-122">Aby uzyskać więcej informacji o subskrypcji, zobacz [wyświetlić subskrybentów produktu][View subscribers to a product].</span><span class="sxs-lookup"><span data-stu-id="793da-122">For more information on subscriptions, see [View subscribers to a product][View subscribers to a product].</span></span>

<span data-ttu-id="793da-123">Aby zezwalać kontom developer do subskrybowania wielokrotnie produktu, sprawdź **zezwalać na wiele subskrypcji** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="793da-123">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="793da-124">Jeśli to pole nie jest zaznaczone, każde konto dewelopera można zasubskrybować tylko jeden raz dla produktu.</span><span class="sxs-lookup"><span data-stu-id="793da-124">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

![Nieograniczone wiele subskrypcji][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="793da-126">Aby ograniczyć liczbę wiele równoczesnych subskrypcji, sprawdź **Ogranicz liczbę jednoczesnych subskrypcje** pole wyboru, a następnie wprowadź limit subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="793da-126">To limit the count of multiple simultaneous subscriptions, check the **Limit number of simultaneous subscriptions to** check box and enter the subscription limit.</span></span> <span data-ttu-id="793da-127">W poniższym przykładzie jednoczesnych subskrypcje są maksymalnie cztery na konto dewelopera.</span><span class="sxs-lookup"><span data-stu-id="793da-127">In the following example, simultaneous subscriptions are limited to four per developer account.</span></span>

![Cztery wiele subskrypcji][api-management-four-multiple-subscriptions]

<span data-ttu-id="793da-129">Po skonfigurowaniu wszystkich nowych opcji produktu, kliknij przycisk **zapisać** do tworzenia nowych produktów.</span><span class="sxs-lookup"><span data-stu-id="793da-129">Once all new product options are configured, click **Save** to create the new product.</span></span>

![Produkty][api-management-products-page]

> <span data-ttu-id="793da-131">Domyślnie są nieopublikowane nowych produktów i są widoczne tylko dla **Administratorzy** grupy.</span><span class="sxs-lookup"><span data-stu-id="793da-131">By default new products are unpublished, and are visible only to the  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="793da-132">Aby skonfigurować produkt, kliknij nazwę produktu w **produktów** kartę.</span><span class="sxs-lookup"><span data-stu-id="793da-132">To configure a product, click on the product name in the **Products** tab.</span></span>

## <span data-ttu-id="793da-133"><a name="add-apis"></a>Dodaj interfejsów API do produktu</span><span class="sxs-lookup"><span data-stu-id="793da-133"><a name="add-apis"> </a>Add APIs to a product</span></span>
<span data-ttu-id="793da-134">**Produktów** strona zawiera cztery łącza dla konfiguracji: **Podsumowanie**, **ustawienia**, **widoczność**, i  **Subskrybenci**.</span><span class="sxs-lookup"><span data-stu-id="793da-134">The **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="793da-135">**Podsumowanie** jest karta, którym można dodać interfejsów API i opublikować lub Cofnij publikowanie produktu.</span><span class="sxs-lookup"><span data-stu-id="793da-135">The **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![Podsumowanie][api-management-new-product-summary]

<span data-ttu-id="793da-137">Przed opublikowaniem produkt, musisz dodać jeden lub więcej interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="793da-137">Before publishing your product you need to add one or more APIs.</span></span> <span data-ttu-id="793da-138">Aby to zrobić, kliknij przycisk **dodać interfejsu API do produktu**.</span><span class="sxs-lookup"><span data-stu-id="793da-138">To do this, click **Add API to product**.</span></span>

![Dodaj interfejsów API][api-management-add-apis-to-product]

<span data-ttu-id="793da-140">Wybierz żądaną interfejsów API i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="793da-140">Select the desired APIs and click **Save**.</span></span>

## <span data-ttu-id="793da-141"><a name="add-description"></a>Dodać opisowe informacje do produktu</span><span class="sxs-lookup"><span data-stu-id="793da-141"><a name="add-description"> </a>Add descriptive information to a product</span></span>
<span data-ttu-id="793da-142">**Ustawienia** karta umożliwia zawierają szczegółowe informacje o produkcie, takie jak jego przeznaczenie, zapewnia dostęp do interfejsów API i inne przydatne informacje.</span><span class="sxs-lookup"><span data-stu-id="793da-142">The **Settings** tab allows you to provide detailed information about the product such as its purpose, the APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="793da-143">Zawartość jest przeznaczona dla deweloperów, spowoduje wywołanie interfejsu API, które mogą być zapisywane w postaci zwykłego tekstu lub kod znaczników HTML.</span><span class="sxs-lookup"><span data-stu-id="793da-143">The content is targeted at the developers that will be calling the API and can be written in plain text or HTML markup.</span></span>

![Ustawienia produktów][api-management-product-settings]

<span data-ttu-id="793da-145">Sprawdź **wymagają subskrypcji** do tworzenia chronionej produkt, który wymaga subskrypcji można używać, lub wyczyść pole wyboru, aby utworzyć otwieranie produktu, który można wywołać bez subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="793da-145">Check **Require subscription** to create a protected product that requires a subscription to be used, or clear the checkbox to create an open product that can be called without a subscription.</span></span>

<span data-ttu-id="793da-146">Wybierz **wymagają zatwierdzenia subskrypcji** Jeśli chcesz ręcznie zatwierdzić wszystkie żądania subskrypcji produktu.</span><span class="sxs-lookup"><span data-stu-id="793da-146">Select **Require subscription approval** if you want to manually approve all product subscription requests.</span></span> <span data-ttu-id="793da-147">Domyślnie wszystkie subskrypcje produktu są przyznawane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="793da-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="793da-148">Aby zezwalać kontom developer do subskrybowania wielokrotnie produktu, sprawdź **zezwalać na wiele subskrypcji** pole wyboru i opcjonalnie Określ limit.</span><span class="sxs-lookup"><span data-stu-id="793da-148">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="793da-149">Jeśli to pole nie jest zaznaczone, każde konto dewelopera można zasubskrybować tylko jeden raz dla produktu.</span><span class="sxs-lookup"><span data-stu-id="793da-149">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

<span data-ttu-id="793da-150">Opcjonalnie wypełnij **warunki użytkowania** pola opisujące warunki użytkowania produktów, którzy użytkownicy muszą zaakceptować, aby korzystać z produktu.</span><span class="sxs-lookup"><span data-stu-id="793da-150">Optionally fill in the **Terms of use** field describing the terms of use for the product which subscribers must accept in order to use the product.</span></span>

## <span data-ttu-id="793da-151"><a name="publish-product"></a>Publikowania produktu</span><span class="sxs-lookup"><span data-stu-id="793da-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="793da-152">Aby można było wywołać interfejsów API w produkcie, musi zostać opublikowany produktu.</span><span class="sxs-lookup"><span data-stu-id="793da-152">Before the APIs in a product can be called, the product must be published.</span></span> <span data-ttu-id="793da-153">Na **Podsumowanie** produktu, kliknij pozycję **publikowania**, a następnie kliknij przycisk **tak, przed opublikowaniem** o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="793da-153">On the **Summary** tab for the product, click **Publish**, and then click **Yes, publish it** to confirm.</span></span> <span data-ttu-id="793da-154">Aby wcześniej opublikowanej produktu prywatne, kliknij przycisk **Cofnij publikowanie**.</span><span class="sxs-lookup"><span data-stu-id="793da-154">To make a previously published product private, click **Unpublish**.</span></span>

![Publikowanie produktu][api-management-publish-product]

## <span data-ttu-id="793da-156"><a name="make-visible"></a>Udostępnienie produktu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="793da-156"><a name="make-visible"> </a>Make a product visible to developers</span></span>
<span data-ttu-id="793da-157">**Widoczność** karcie można wybrać role mogą wyświetlić w portalu dla deweloperów i subskrybowanie produktu.</span><span class="sxs-lookup"><span data-stu-id="793da-157">The **Visibility** tab allows you to choose which roles are able to see the product on the developer portal and subscribe to the product.</span></span>

![Widoczność produktu][api-management-product-visiblity]

<span data-ttu-id="793da-159">Aby włączyć lub wyłączyć widoczność produktu dla deweloperów w grupie, sprawdź lub usuń zaznaczenie pola wyboru obok grupy, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="793da-159">To enable or disable visibility of a product for the developers in a group, check or uncheck the check box beside the group and then click **Save**.</span></span>

> <span data-ttu-id="793da-160">Aby uzyskać więcej informacji, zobacz [tworzenie i używanie grup do zarządzania konta dewelopera usługi Azure API Management][How to create and use groups to manage developer accounts in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="793da-160">For more information, see [How to create and use groups to manage developer accounts in Azure API Management][How to create and use groups to manage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="793da-161"><a name="view-subscribers"></a>Wyświetlić subskrybentów produktu</span><span class="sxs-lookup"><span data-stu-id="793da-161"><a name="view-subscribers"> </a>View subscribers to a product</span></span>
<span data-ttu-id="793da-162">**Subskrybentów** karta zawiera listę deweloperów, którzy subskrybuje produktu.</span><span class="sxs-lookup"><span data-stu-id="793da-162">The **Subscribers** tab lists the developers who have subscribed to the product.</span></span> <span data-ttu-id="793da-163">Ustawienia dla wszystkich deweloperów i szczegółowe informacje można wyświetlić, klikając nazwę dewelopera.</span><span class="sxs-lookup"><span data-stu-id="793da-163">The details and settings for each developer can be viewed by clicking on the developer's name.</span></span> <span data-ttu-id="793da-164">W tym przykładzie deweloperzy nie masz jeszcze subskrypcję do produktu.</span><span class="sxs-lookup"><span data-stu-id="793da-164">In this example no developers have yet subscribed to the product.</span></span>

![Deweloperzy][api-management-developer-list]

## <span data-ttu-id="793da-166"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="793da-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="793da-167">Po są dodawane odpowiednie interfejsów API i publikowane produktu, deweloperzy mogą subskrybować produktu i rozpocząć do wywoływania interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="793da-167">Once the desired APIs are added and the product published, developers can subscribe to the product and begin to call the APIs.</span></span> <span data-ttu-id="793da-168">Samouczek przedstawiający tych elementów, a także zaawansowane produktu configuration [jak utworzyć i skonfigurować ustawienia zaawansowane produktu w usłudze Azure API Management][How create and configure advanced product settings in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="793da-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="793da-169">Aby uzyskać więcej informacji na temat pracy z produktami zobacz poniższe wideo.</span><span class="sxs-lookup"><span data-stu-id="793da-169">For more information about working with products, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs to a product]: #add-apis
[Add descriptive information to a product]: #add-description
[Publish a product]: #publish-product
[Make a product visible to developers]: #make-visible
[View subscribers to a product]: #view-subscribers
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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How to create and use groups to manage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
