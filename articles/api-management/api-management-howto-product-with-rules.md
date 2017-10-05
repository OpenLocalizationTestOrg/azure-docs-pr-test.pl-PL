---
title: "Ochrona interfejsu API za pomocą usługi Azure API Management | Microsoft Docs"
description: "Dowiedz się, jak chronić interfejs API za pomocą zasad przydziałów i dławienia (ograniczania liczby wywołań)."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 5553bcb8f9fd38630f694151dc644a684266387c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a><span data-ttu-id="bbd41-103">Ochrona interfejsu API za pomocą ograniczania liczby wywołań przy użyciu usługi Azure API Management</span><span class="sxs-lookup"><span data-stu-id="bbd41-103">Protect your API with rate limits using Azure API Management</span></span>
<span data-ttu-id="bbd41-104">W tym przewodniku przedstawiono, jak łatwo można dodawać ochronę do interfejsu API zaplecza dzięki konfigurowaniu zasad ograniczania liczby wywołań i przydziałów za pomocą usługi Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="bbd41-104">This guide shows you how easy it is to add protection for your backend API by configuring rate limit and quota policies with Azure API Management.</span></span>

<span data-ttu-id="bbd41-105">W tym samouczku utworzysz produkt interfejsu API o nazwie „Bezpłatna wersja próbna”, który umożliwia deweloperom wykonywanie do 10 wywołań na minutę i maksymalnie 200 wywołań na tydzień tego interfejsu API przy użyciu zasad [Ograniczanie liczby wywołań na subskrypcję](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) i [Ustawianie przydziału użycia na subskrypcję](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota).</span><span class="sxs-lookup"><span data-stu-id="bbd41-105">In this tutorial, you will create a "Free Trial" API product that allows developers to make up to 10 calls per minute and up to a maximum of 200 calls per week to your API using the [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="bbd41-106">Następnie opublikujesz interfejs API i przetestujesz zasadę ograniczania liczby wywołań.</span><span class="sxs-lookup"><span data-stu-id="bbd41-106">You will then publish the API and test the rate limit policy.</span></span>

<span data-ttu-id="bbd41-107">Bardziej zaawansowane scenariusze ograniczania żądań używające zasad [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) i [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) są opisane w artykule [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md) (Zaawansowane ograniczanie żądań za pomocą usługi Azure API Management).</span><span class="sxs-lookup"><span data-stu-id="bbd41-107">For more advanced throttling scenarios using the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies, see [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md).</span></span>

## <span data-ttu-id="bbd41-108"><a name="create-product"> </a>Aby utworzyć produkt</span><span class="sxs-lookup"><span data-stu-id="bbd41-108"><a name="create-product"> </a>To create a product</span></span>
<span data-ttu-id="bbd41-109">W tym kroku utworzysz produkt Bezpłatna wersja próbna, który nie wymaga zatwierdzania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bbd41-109">In this step, you will create a Free Trial product that does not require subscription approval.</span></span>

> [!NOTE]
> <span data-ttu-id="bbd41-110">Jeśli już masz skonfigurowany produkt i chcesz używać go w ramach tego samouczka, możesz przejść od razu do tematu [Konfigurowanie zasad ograniczania liczby wywołań oraz przydziałów][Configure call rate limit and quota policies] i wykonać kroki samouczka od tamtego miejsca przy użyciu swojego produktu zamiast produktu Bezpłatna wersja próbna.</span><span class="sxs-lookup"><span data-stu-id="bbd41-110">If you already have a product configured and want to use it for this tutorial, you can jump ahead to [Configure call rate limit and quota policies][Configure call rate limit and quota policies] and follow the tutorial from there using your product in place of the Free Trial product.</span></span>
> 
> 

<span data-ttu-id="bbd41-111">Na początku kliknij opcję **Portal wydawcy** w klasycznej witrynie Azure Portal dla usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="bbd41-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portal wydawcy][api-management-management-console]

> <span data-ttu-id="bbd41-113">Jeśli jeszcze nie utworzono wystąpienia usługi API Management, zobacz [Tworzenie wystąpienia usługi API Management][Create an API Management service instance] w samouczku [Zarządzanie pierwszym interfejsem API w usłudze Azure API Management][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="bbd41-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Manage your first API in Azure API Management][Manage your first API in Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="bbd41-114">Kliknij opcję **Produkty** w menu **API Management** po lewej stronie, aby wyświetlić stronę **Produkty**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-114">Click **Products** in the **API Management** menu on the left to display the **Products** page.</span></span>

![Dodawanie produktu][api-management-add-product]

<span data-ttu-id="bbd41-116">Kliknij przycisk **Dodaj produkt**, aby wyświetlić okno dialogowe **Dodawanie nowego produktu**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-116">Click **Add product** to display the **Add new product** dialog box.</span></span>

![Dodawanie nowego produktu][api-management-new-product-window]

<span data-ttu-id="bbd41-118">W polu **Tytuł** wpisz **Bezpłatna wersja próbna**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-118">In the **Title** box, type **Free Trial**.</span></span>

<span data-ttu-id="bbd41-119">W polu **Opis** wpisz następujący tekst: **Subskrybenci będą mogli uruchamiać 10 wywołań na minutę, ale nie więcej niż 200 wywołań na tydzień, po czym nastąpi odmowa dostępu.**</span><span class="sxs-lookup"><span data-stu-id="bbd41-119">In the **Description** box, type the following text: **Subscribers will be able to run 10 calls/minute up to a maximum of 200 calls/week after which access is denied.**</span></span>

<span data-ttu-id="bbd41-120">Produkty w usłudze API Management mogą być chronione lub otwarte.</span><span class="sxs-lookup"><span data-stu-id="bbd41-120">Products in API Management can be protected or open.</span></span> <span data-ttu-id="bbd41-121">Produkty chronione muszą być subskrybowane przed użyciem.</span><span class="sxs-lookup"><span data-stu-id="bbd41-121">Protected products must be subscribed to before they can be used.</span></span> <span data-ttu-id="bbd41-122">Produkty otwarte mogą być używane bez subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bbd41-122">Open products can be used without a subscription.</span></span> <span data-ttu-id="bbd41-123">Upewnij się, że opcja **Wymagaj subskrypcji** jest zaznaczona, aby utworzyć produkt chroniony, który wymaga subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bbd41-123">Ensure that **Require subscription** is selected to create a protected product that requires a subscription.</span></span> <span data-ttu-id="bbd41-124">Jest to ustawienie domyślne.</span><span class="sxs-lookup"><span data-stu-id="bbd41-124">This is the default setting.</span></span>

<span data-ttu-id="bbd41-125">Jeśli chcesz, aby administrator przeglądał i akceptował lub odrzucał próby subskrypcji tego produktu, wybierz opcję **Wymagaj zatwierdzenia subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-125">If you want an administrator to review and accept or reject subscription attempts to this product, select **Require subscription approval**.</span></span> <span data-ttu-id="bbd41-126">Jeśli to pole wyboru nie jest zaznaczone, próby subskrypcji będą zatwierdzane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="bbd41-126">If the check box is not selected, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="bbd41-127">W tym przykładzie subskrypcje są zatwierdzane automatycznie, więc nie zaznaczaj tego pola.</span><span class="sxs-lookup"><span data-stu-id="bbd41-127">In this example, subscriptions are automatically approved, so do not select the box.</span></span>

<span data-ttu-id="bbd41-128">Aby umożliwić kontom deweloperów wielokrotne subskrybowanie nowego produktu, zaznacz pole wyboru **Zezwalaj na wiele jednoczesnych subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-128">To allow developer accounts to subscribe multiple times to the new product, select the **Allow multiple simultaneous subscriptions** check box.</span></span> <span data-ttu-id="bbd41-129">Ten samouczek nie wykorzystuje wielu jednoczesnych subskrypcji, więc pozostaw to pole niezaznaczone.</span><span class="sxs-lookup"><span data-stu-id="bbd41-129">This tutorial does not utilize multiple simultaneous subscriptions, so leave it unchecked.</span></span>

<span data-ttu-id="bbd41-130">Po wprowadzeniu wszystkich wartości kliknij przycisk **Zapisz**, aby utworzyć produkt.</span><span class="sxs-lookup"><span data-stu-id="bbd41-130">After all values are entered, click **Save** to create the product.</span></span>

![Dodany produkt][api-management-product-added]

<span data-ttu-id="bbd41-132">Domyślnie nowe produkty są widoczne dla użytkowników w grupie **Administratorzy**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-132">By default, new products are visible to users in the **Administrators** group.</span></span> <span data-ttu-id="bbd41-133">Zamierzamy dodać grupę **Deweloperzy**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-133">We are going to add the **Developers** group.</span></span> <span data-ttu-id="bbd41-134">Kliknij produkt **Bezpłatna wersja próbna**, a następnie kliknij kartę **Widoczność**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-134">Click **Free Trial**, and then click the **Visibility** tab.</span></span>

> <span data-ttu-id="bbd41-135">W usłudze API Management grupy służą do zarządzania widocznością produktów dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="bbd41-135">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="bbd41-136">Widoczność produktów jest przydzielana według grup, a deweloperzy mogą wyświetlać i subskrybować produkty, które są widoczne dla grup, do których należą.</span><span class="sxs-lookup"><span data-stu-id="bbd41-136">Products grant visibility to groups, and developers can view and subscribe to the products that are visible to the groups in which they belong.</span></span> <span data-ttu-id="bbd41-137">Aby uzyskać więcej informacji, zobacz [How to create and use groups in Azure API Management][How to create and use groups in Azure API Management] (Jak utworzyć grupy w usłudze Azure API Management i używać ich).</span><span class="sxs-lookup"><span data-stu-id="bbd41-137">For more information, see [How to create and use groups in Azure API Management][How to create and use groups in Azure API Management].</span></span>
> 
> 

![Dodawanie grupy deweloperów][api-management-add-developers-group]

<span data-ttu-id="bbd41-139">Zaznacz pole wyboru **Deweloperzy**, a następnie kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-139">Select the **Developers** check box, and then click **Save**.</span></span>

## <span data-ttu-id="bbd41-140"><a name="add-api"> </a>Aby dodać interfejs API do produktu</span><span class="sxs-lookup"><span data-stu-id="bbd41-140"><a name="add-api"> </a>To add an API to the product</span></span>
<span data-ttu-id="bbd41-141">W tym kroku samouczka dodamy interfejs Echo API do nowego produktu Bezpłatna wersja próbna.</span><span class="sxs-lookup"><span data-stu-id="bbd41-141">In this step of the tutorial, we will add the Echo API to the new Free Trial product.</span></span>

> <span data-ttu-id="bbd41-142">Każde wystąpienie usługi API Management ma wstępnie skonfigurowany interfejs Echo API, którego można używać do eksperymentów oraz poznawania usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="bbd41-142">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="bbd41-143">Aby uzyskać więcej informacji, zobacz [Zarządzanie pierwszym interfejsem API w usłudze Azure API Management][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="bbd41-143">For more information, see [Manage your first API in Azure API Management][Manage your first API in Azure API Management].</span></span>
> 
> 

<span data-ttu-id="bbd41-144">Kliknij przycisk **Produkty** z menu **API Management** po lewej stronie, a następnie kliknij produkt **Bezpłatna wersja próbna**, aby go skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="bbd41-144">Click **Products** from the **API Management** menu on the left, and then click **Free Trial** to configure the product.</span></span>

![Konfigurowanie produktu][api-management-configure-product]

<span data-ttu-id="bbd41-146">Kliknij przycisk **Dodaj interfejs API do produktu**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-146">Click **Add API to product**.</span></span>

![Dodawanie interfejsu API do produktu.][api-management-add-api]

<span data-ttu-id="bbd41-148">Wybierz interfejs **Echo API**, a następnie kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-148">Select **Echo API**, and then click **Save**.</span></span>

![Dodawanie interfejsu Echo API][api-management-add-echo-api]

## <span data-ttu-id="bbd41-150"><a name="policies"> </a>Aby skonfigurować zasady ograniczania liczby wywołań oraz przydziałów</span><span class="sxs-lookup"><span data-stu-id="bbd41-150"><a name="policies"> </a>To configure call rate limit and quota policies</span></span>
<span data-ttu-id="bbd41-151">Ograniczenia liczby wywołań i przydziały są konfigurowane w edytorze zasad.</span><span class="sxs-lookup"><span data-stu-id="bbd41-151">Rate limits and quotas are configured in the policy editor.</span></span> <span data-ttu-id="bbd41-152">Dwiema zasadami, które dodamy w tym samouczku, są zasady [Ograniczanie liczby wywołań na subskrypcję](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) i [Ustawianie przydziału użycia na subskrypcję](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota).</span><span class="sxs-lookup"><span data-stu-id="bbd41-152">The two policies we will be adding in this tutorial are the [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="bbd41-153">Te zasady muszą być stosowane w zakresie produktu.</span><span class="sxs-lookup"><span data-stu-id="bbd41-153">These policies must be applied at the product scope.</span></span>

<span data-ttu-id="bbd41-154">Kliknij opcję **Zasady** w menu **API Management** po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="bbd41-154">Click **Policies** under the **API Management** menu on the left.</span></span> <span data-ttu-id="bbd41-155">Na liście **Produkty** kliknij produkt **Bezpłatna wersja próbna**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-155">In the **Product** list, click **Free Trial**.</span></span>

![Zasady produktu][api-management-product-policy]

<span data-ttu-id="bbd41-157">Kliknij przycisk **Dodaj zasadę**, aby zaimportować szablon zasad i rozpocząć tworzenie zasad ograniczania liczby wywołań i przydziałów.</span><span class="sxs-lookup"><span data-stu-id="bbd41-157">Click **Add Policy** to import the policy template and begin creating the rate limit and quota policies.</span></span>

![Dodawanie zasad][api-management-add-policy]

<span data-ttu-id="bbd41-159">Zasady ograniczania liczby wywołań i przydziałów są zasadami ruchu przychodzącego, więc umieść kursor w elemencie inbound.</span><span class="sxs-lookup"><span data-stu-id="bbd41-159">Rate limit and quota policies are inbound policies, so position the cursor in the inbound element.</span></span>

![Edytor zasad][api-management-policy-editor-inbound]

<span data-ttu-id="bbd41-161">Przewiń listę zasad i znajdź wpis zasad **Ograniczanie liczby wywołań na subskrypcję**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-161">Scroll through the list of policies and locate the **Limit call rate per subscription** policy entry.</span></span>

![Instrukcje zasad][api-management-limit-policies]

<span data-ttu-id="bbd41-163">Po umieszczeniu kursora w elemencie zasady **inbound**, kliknij strzałkę obok opcji **Ograniczanie liczby wywołań na subskrypcję**, aby wstawić ten szablon zasady.</span><span class="sxs-lookup"><span data-stu-id="bbd41-163">After the cursor is positioned in the **inbound** policy element, click the arrow beside **Limit call rate per subscription** to insert its policy template.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

<span data-ttu-id="bbd41-164">Jak widać we fragmencie kodu, zasady umożliwiają ustawienie limitów dla interfejsów API i operacji produktu.</span><span class="sxs-lookup"><span data-stu-id="bbd41-164">As you can see from the snippet, the policy allows setting limits for the product's APIs and operations.</span></span> <span data-ttu-id="bbd41-165">W tym samouczku nie będziemy korzystać z tej możliwości, więc usuń elementy **api** i **operation** elementu **rate-limit**, aby pozostał tylko zewnętrzny element **rate-limit**, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="bbd41-165">In this tutorial we will not use that capability, so delete the **api** and **operation** elements from the **rate-limit** element, such that only the outer **rate-limit** element remains, as shown in the following example.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

<span data-ttu-id="bbd41-166">W produkcie Bezpłatna wersja próbna maksymalna liczba wywołań to 10 na minutę, więc wpisz **10** jako wartość atrybutu **calls** oraz i **60** jako wartość atrybutu **renewal-period**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-166">In the Free Trial product, the maximum allowable call rate is 10 calls per minute, so type **10** as the value for the **calls** attribute, and **60** for the **renewal-period** attribute.</span></span>

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

<span data-ttu-id="bbd41-167">Aby skonfigurować zasady **Ustawianie przydziału użycia na subskrypcję**, umieść kursor bezpośrednio pod nowo dodanym elementem **rate-limit** w elemencie **inbound**, a następnie zlokalizuj i kliknij strzałkę po lewej stronie zasad **Ustawianie przydziału użycia na subskrypcję**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-167">To configure the **Set usage quota per subscription** policy, position your cursor immediately below the newly added **rate-limit** element within the **inbound** element, and then locate and click the arrow to the left of **Set usage quota per subscription**.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

<span data-ttu-id="bbd41-168">Podobnie jak zasady **Ustawianie przydziału użycia na subskrypcję**, zasady **Ustawianie przydziału użycia na subskrypcję** umożliwia ustawienie limitów dla interfejsów API i operacji w produkcie.</span><span class="sxs-lookup"><span data-stu-id="bbd41-168">Similarly to the **Set usage quota per subscription** policy, **Set usage quota per subscription** policy allows setting caps for on the product's APIs and operations.</span></span> <span data-ttu-id="bbd41-169">W tym samouczku nie będziemy korzystać z tej możliwości, więc usuń elementy **api** i **operation** z elementu **quota**, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="bbd41-169">In this tutorial we will not use that capability, so delete the **api** and **operation** elements from the **quota** element, as shown in the following example.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

<span data-ttu-id="bbd41-170">Przydziały mogą opierać się na liczbie wywołań na interwał, przepustowości lub obu tych warunkach.</span><span class="sxs-lookup"><span data-stu-id="bbd41-170">Quotas can be based on the number of calls per interval, bandwidth, or both.</span></span> <span data-ttu-id="bbd41-171">W tym samouczku nie będziemy ograniczać żądań na podstawie przepustowości, więc usuń atrybut **bandwidth**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-171">In this tutorial, we are not throttling based on bandwidth, so delete the **bandwidth** attribute.</span></span>

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

<span data-ttu-id="bbd41-172">W produkcie Bezpłatna wersja próbna przydział wynosi 200 wywołań na tydzień.</span><span class="sxs-lookup"><span data-stu-id="bbd41-172">In the Free Trial product, the quota is 200 calls per week.</span></span> <span data-ttu-id="bbd41-173">Podaj **200** jako wartość atrybutu **calls**, a następnie podaj **604800** jako wartość atrybutu **renewal-period**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-173">Specify **200** as the value for the **calls** attribute, and then specify **604800** as the value for the **renewal-period** attribute.</span></span>

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> <span data-ttu-id="bbd41-174">Interwały zasad są określane w sekundach.</span><span class="sxs-lookup"><span data-stu-id="bbd41-174">Policy intervals are specified in seconds.</span></span> <span data-ttu-id="bbd41-175">Aby obliczyć interwał dla tygodnia, należy pomnożyć liczbę dni (7) przez liczbę godzin w ciągu dnia (24) przez liczbę minut w godzinie (60) przez liczbę sekund w ciągu minuty (60): 7 * 24 * 60 * 60 = 604800.</span><span class="sxs-lookup"><span data-stu-id="bbd41-175">To calculate the interval for a week, you can multiply the number of days (7) by the number of hours in a day (24) by the number of minutes in an hour (60) by the number of seconds in a minute (60): 7 * 24 * 60 * 60 = 604800.</span></span>
> 
> 

<span data-ttu-id="bbd41-176">Po zakończeniu konfigurowania zasady powinny być zgodne z poniższym przykładem.</span><span class="sxs-lookup"><span data-stu-id="bbd41-176">When you have finished configuring the policy, it should match the following example.</span></span>

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

<span data-ttu-id="bbd41-177">Po skonfigurowaniu żądanych zasad kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-177">After the desired policies are configured, click **Save**.</span></span>

![Zapisywanie zasad][api-management-policy-save]

## <span data-ttu-id="bbd41-179"><a name="publish-product"> </a> Aby opublikować produkt</span><span class="sxs-lookup"><span data-stu-id="bbd41-179"><a name="publish-product"> </a> To publish the product</span></span>
<span data-ttu-id="bbd41-180">Teraz, gdy interfejsy API zostały dodane, a zasady skonfigurowane, trzeba opublikować produkt, aby mógł być używany przez deweloperów.</span><span class="sxs-lookup"><span data-stu-id="bbd41-180">Now that the the APIs are added and the policies are configured, the product must be published so that it can be used by developers.</span></span> <span data-ttu-id="bbd41-181">Kliknij przycisk **Produkty** z menu **API Management** po lewej stronie, a następnie kliknij produkt **Bezpłatna wersja próbna**, aby go skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="bbd41-181">Click **Products** from the **API Management** menu on the left, and then click **Free Trial** to configure the product.</span></span>

![Konfigurowanie produktu][api-management-configure-product]

<span data-ttu-id="bbd41-183">Kliknij przycisk **Publikuj**, a następnie kliknij przycisk **Tak, opublikuj**, aby potwierdzić.</span><span class="sxs-lookup"><span data-stu-id="bbd41-183">Click **Publish**, and then click **Yes, publish it** to confirm.</span></span>

![Publikowanie produktu][api-management-publish-product]

## <span data-ttu-id="bbd41-185"><a name="subscribe-account"> </a>Aby zasubskrybować produkt dla konta dewelopera</span><span class="sxs-lookup"><span data-stu-id="bbd41-185"><a name="subscribe-account"> </a>To subscribe a developer account to the product</span></span>
<span data-ttu-id="bbd41-186">Teraz, gdy produkt jest publikowany, jest on dostępny do subskrybowania i używania przez deweloperów.</span><span class="sxs-lookup"><span data-stu-id="bbd41-186">Now that the product is published, it is available to be subscribed to and used by developers.</span></span>

> <span data-ttu-id="bbd41-187">Administratorzy wystąpienia usługi API Management automatycznie mają subskrypcję każdego produktu.</span><span class="sxs-lookup"><span data-stu-id="bbd41-187">Administrators of an API Management instance are automatically subscribed to every product.</span></span> <span data-ttu-id="bbd41-188">W tym kroku samouczka zasubskrybujemy produkt Bezpłatna wersja próbna dla jednego z kont deweloperów, którzy nie są administratorami.</span><span class="sxs-lookup"><span data-stu-id="bbd41-188">In this tutorial step, we will subscribe one of the non-administrator developer accounts to the Free Trial product.</span></span> <span data-ttu-id="bbd41-189">Jeśli konto dewelopera należy do roli Administratorzy, możesz wykonać ten krok, chociaż masz już subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="bbd41-189">If your developer account is part of the Administrators role, then you can follow along with this step, even though you are already subscribed.</span></span>
> 
> 

<span data-ttu-id="bbd41-190">Kliknij przycisk **Użytkownicy** w menu **API Management** po lewej stronie, a następnie kliknij nazwę Twojego konta dewelopera.</span><span class="sxs-lookup"><span data-stu-id="bbd41-190">Click **Users** on the **API Management** menu on the left, and then click the name of your developer account.</span></span> <span data-ttu-id="bbd41-191">W tym przykładzie użyto konta dewelopera **Clayton Gragg**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-191">In this example, we are using the **Clayton Gragg** developer account.</span></span>

![Konfigurowanie konta dewelopera][api-management-configure-developer]

<span data-ttu-id="bbd41-193">Kliknij przycisk **Dodaj subskrypcję**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-193">Click **Add Subscription**.</span></span>

![Dodawanie subskrypcji][api-management-add-subscription-menu]

<span data-ttu-id="bbd41-195">Wybierz produkt **Bezpłatna wersja próbna**, a następnie kliknij przycisk **Subskrybuj**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-195">Select **Free Trial**, and then click **Subscribe**.</span></span>

![Dodawanie subskrypcji][api-management-add-subscription]

> [!NOTE]
> <span data-ttu-id="bbd41-197">W tym samouczku nie włączono wielu jednoczesnych subskrypcji dla produktu Bezpłatna wersja próbna.</span><span class="sxs-lookup"><span data-stu-id="bbd41-197">In this tutorial, multiple simultaneous subscriptions are not enabled for the Free Trial product.</span></span> <span data-ttu-id="bbd41-198">Gdyby były włączone, pojawiłby się monit o podanie nazwy subskrypcji, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="bbd41-198">If they were, you would be prompted to name the subscription, as shown in the following example.</span></span>
> 
> 

![Dodawanie subskrypcji][api-management-add-subscription-multiple]

<span data-ttu-id="bbd41-200">Po kliknięciu przycisku **Subskrybuj** produkt jest wyświetlany na liście **Subskrypcja** danego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bbd41-200">After clicking **Subscribe**, the product appears in the **Subscription** list for the user.</span></span>

![Dodana subskrypcja][api-management-subscription-added]

## <span data-ttu-id="bbd41-202"><a name="test-rate-limit"> </a>Aby wywołać operację i przetestować ograniczanie liczby wywołań</span><span class="sxs-lookup"><span data-stu-id="bbd41-202"><a name="test-rate-limit"> </a>To call an operation and test the rate limit</span></span>
<span data-ttu-id="bbd41-203">Teraz, gdy produkt Bezpłatna wersja próbna jest skonfigurowany i opublikowany, możemy wywołać pewne operacje i przetestować zasadę ograniczania liczby wywołań.</span><span class="sxs-lookup"><span data-stu-id="bbd41-203">Now that the Free Trial product is configured and published, we can call some operations and test the rate limit policy.</span></span>
<span data-ttu-id="bbd41-204">Kliknij opcję **Portal dla deweloperów** w górnym menu po prawej stronie, aby przejść do portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="bbd41-204">Switch to the developer portal by clicking **Developer portal** in the upper-right menu.</span></span>

![Portal dla deweloperów][api-management-developer-portal-menu]

<span data-ttu-id="bbd41-206">Kliknij opcję **Interfejsy API** w górnym menu, a następnie wybierz interfejs **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-206">Click **APIs** in the top menu, and then click **Echo API**.</span></span>

![Portal dla deweloperów][api-management-developer-portal-api-menu]

<span data-ttu-id="bbd41-208">Kliknij operację **GET Resource** (pobieranie zasobu), a następnie kliknij przycisk **Wypróbuj**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-208">Click **GET Resource**, and then click **Try it**.</span></span>

![Otwarta konsola][api-management-open-console]

<span data-ttu-id="bbd41-210">Zachowaj domyślne wartości parametrów, a następnie wybierz klucz subskrypcji dla produktu Bezpłatna wersja próbna.</span><span class="sxs-lookup"><span data-stu-id="bbd41-210">Keep the default parameter values, and then select your subscription key for the Free Trial product.</span></span>

![Klucz subskrypcji][api-management-select-key]

> [!NOTE]
> <span data-ttu-id="bbd41-212">Jeśli masz wiele subskrypcji, koniecznie wybierz klucz dla produktu **Bezpłatna wersja próbna**. W przeciwnym razie zasady skonfigurowane w poprzednich krokach nie będą obowiązywać.</span><span class="sxs-lookup"><span data-stu-id="bbd41-212">If you have multiple subscriptions, be sure to select the key for **Free Trial**, or else the policies that were configured in the previous steps won't be in effect.</span></span>
> 
> 

<span data-ttu-id="bbd41-213">Kliknij przycisk **Wyślij**, a następnie zobacz odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="bbd41-213">Click **Send**, and then view the response.</span></span> <span data-ttu-id="bbd41-214">Zauważ, że **Stan odpowiedzi** to **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="bbd41-214">Note the **Response status** of **200 OK**.</span></span>

![Wyniki operacji][api-management-http-get-results]

<span data-ttu-id="bbd41-216">Kliknij przycisk **Wyślij** szybciej niż pozwala na to zasada ograniczenia liczby wywołań do 10 na minutę.</span><span class="sxs-lookup"><span data-stu-id="bbd41-216">Click **Send** at a rate greater than the rate limit policy of 10 calls per minute.</span></span> <span data-ttu-id="bbd41-217">Po przekroczeniu zasady ograniczania liczby wywołań zwracany jest stan **429 Too Many Requests** (429 Zbyt wiele żądań).</span><span class="sxs-lookup"><span data-stu-id="bbd41-217">After the rate limit policy is exceeded, a response status of **429 Too Many Requests** is returned.</span></span>

![Wyniki operacji][api-management-http-get-429]

<span data-ttu-id="bbd41-219">**Zawartość odpowiedzi** wskazuje pozostały czas, zanim ponowna próba zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="bbd41-219">The **Response content** indicates the remaining interval before retries will be successful.</span></span>

<span data-ttu-id="bbd41-220">Jeśli obowiązuje zasada ograniczania liczby wywołań do 10 na minutę, kolejne wywołania będą kończyć się niepowodzeniem, aż upłynie 60 sekund od pierwszego z 10 pomyślnych wywołań produktu przed przekroczeniem ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="bbd41-220">When the rate limit policy of 10 calls per minute is in effect, subsequent calls will fail until 60 seconds have elapsed from the first of the 10 successful calls to the product before the rate limit was exceeded.</span></span> <span data-ttu-id="bbd41-221">W tym przykładzie pozostały interwał to 54 sekundy.</span><span class="sxs-lookup"><span data-stu-id="bbd41-221">In this example, the remaining interval is 54 seconds.</span></span>

## <span data-ttu-id="bbd41-222"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bbd41-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="bbd41-223">Obejrzyj następujący film z prezentacją ustawiania ograniczeń liczby wywołań i przydziałów.</span><span class="sxs-lookup"><span data-stu-id="bbd41-223">Watch a demo of setting rate limits and quotas in the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How to create and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers to a product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API to the product]: #add-api
[Publish the product]: #publish-product
[Subscribe a developer account to the product]: #subscribe-account
[Call an operation and test the rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
