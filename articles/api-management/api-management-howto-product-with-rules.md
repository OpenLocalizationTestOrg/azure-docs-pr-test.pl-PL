---
title: "aaaProtect interfejs API usługi Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprotect interfejs API przydziały i ograniczenia przepustowości (limitów szybkości) zasady."
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
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a><span data-ttu-id="54496-103">Ochrona interfejsu API za pomocą ograniczania liczby wywołań przy użyciu usługi Azure API Management</span><span class="sxs-lookup"><span data-stu-id="54496-103">Protect your API with rate limits using Azure API Management</span></span>
<span data-ttu-id="54496-104">Ten przewodnik przedstawia, jak łatwo jest tooadd ochronę interfejs API zaplecza przez skonfigurowanie zasad limitu i przydziału szybkość z usługą Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="54496-104">This guide shows you how easy it is tooadd protection for your backend API by configuring rate limit and quota policies with Azure API Management.</span></span>

<span data-ttu-id="54496-105">W tym samouczku utworzysz produkt "Bezpłatnej wersji próbnej" interfejsu API, który umożliwia deweloperom stosowanie toomake rozmowy too10 na minutę oraz tooa maksymalnie 200 wywołań na tydzień tooyour API przy użyciu hello [częstotliwość wywołań Limit subskrypcji](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) i [ Ustawianie użycie przydziału dla subskrypcji](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) zasad.</span><span class="sxs-lookup"><span data-stu-id="54496-105">In this tutorial, you will create a "Free Trial" API product that allows developers toomake up too10 calls per minute and up tooa maximum of 200 calls per week tooyour API using hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="54496-106">Następnie zostanie publikowanie hello interfejsu API i testowania zasad limitu szybkości hello.</span><span class="sxs-lookup"><span data-stu-id="54496-106">You will then publish hello API and test hello rate limit policy.</span></span>

<span data-ttu-id="54496-107">Bardziej zaawansowanych scenariuszy przy użyciu hello ograniczania [szybkość limit przez klucz](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) i [limitu przydziału przez klucz](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) zasad, zobacz [Zaawansowane żądanie ograniczania z usługą Azure API Management](api-management-sample-flexible-throttling.md).</span><span class="sxs-lookup"><span data-stu-id="54496-107">For more advanced throttling scenarios using hello [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies, see [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md).</span></span>

## <span data-ttu-id="54496-108"><a name="create-product"></a>toocreate produktu</span><span class="sxs-lookup"><span data-stu-id="54496-108"><a name="create-product"> </a>toocreate a product</span></span>
<span data-ttu-id="54496-109">W tym kroku utworzysz produkt Bezpłatna wersja próbna, który nie wymaga zatwierdzania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="54496-109">In this step, you will create a Free Trial product that does not require subscription approval.</span></span>

> [!NOTE]
> <span data-ttu-id="54496-110">Jeśli już korzystasz z produktem skonfigurowane i chcesz toouse go w tym samouczku, można przejść dalej zbyt[Konfiguruj wywołać szybkość zasady, a limit przydziału] [ Configure call rate limit and quota policies] i postępuj zgodnie z samouczkiem hello stamtąd pomocą produktu zamiast hello bezpłatnej wersji próbnej produktu.</span><span class="sxs-lookup"><span data-stu-id="54496-110">If you already have a product configured and want toouse it for this tutorial, you can jump ahead too[Configure call rate limit and quota policies][Configure call rate limit and quota policies] and follow hello tutorial from there using your product in place of hello Free Trial product.</span></span>
> 
> 

<span data-ttu-id="54496-111">tooget pracę, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="54496-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portal wydawcy][api-management-management-console]

> <span data-ttu-id="54496-113">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [Zarządzanie pierwszy interfejs API usługi Azure API Management] [ Manage your first API in Azure API Management] samouczka.</span><span class="sxs-lookup"><span data-stu-id="54496-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API in Azure API Management][Manage your first API in Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="54496-114">Kliknij przycisk **produktów** w hello **zarządzanie interfejsami API** menu na powitania po lewej stronie toodisplay hello **produktów** strony.</span><span class="sxs-lookup"><span data-stu-id="54496-114">Click **Products** in hello **API Management** menu on hello left toodisplay hello **Products** page.</span></span>

![Dodawanie produktu][api-management-add-product]

<span data-ttu-id="54496-116">Kliknij przycisk **produktu Dodaj** toodisplay hello **Dodaj nowy produkt** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="54496-116">Click **Add product** toodisplay hello **Add new product** dialog box.</span></span>

![Dodawanie nowego produktu][api-management-new-product-window]

<span data-ttu-id="54496-118">W hello **tytuł** wpisz **bezpłatnej wersji próbnej**.</span><span class="sxs-lookup"><span data-stu-id="54496-118">In hello **Title** box, type **Free Trial**.</span></span>

<span data-ttu-id="54496-119">W hello **opis** okno, hello typu następującego tekstu: **subskrybenci będą mogli toorun 10 wywołań/minutę w górę tooa maksymalnie 200 wywołania na tydzień po upływie którego dostęp jest zabroniony.**</span><span class="sxs-lookup"><span data-stu-id="54496-119">In hello **Description** box, type hello following text: **Subscribers will be able toorun 10 calls/minute up tooa maximum of 200 calls/week after which access is denied.**</span></span>

<span data-ttu-id="54496-120">Produkty w usłudze API Management mogą być chronione lub otwarte.</span><span class="sxs-lookup"><span data-stu-id="54496-120">Products in API Management can be protected or open.</span></span> <span data-ttu-id="54496-121">Produkty chronione muszą być subskrybowanego toobefore, które mogą być używane.</span><span class="sxs-lookup"><span data-stu-id="54496-121">Protected products must be subscribed toobefore they can be used.</span></span> <span data-ttu-id="54496-122">Produkty otwarte mogą być używane bez subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="54496-122">Open products can be used without a subscription.</span></span> <span data-ttu-id="54496-123">Upewnij się, że **wymagają subskrypcji** jest wybrany toocreate chronionych produkt, który wymaga subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="54496-123">Ensure that **Require subscription** is selected toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="54496-124">To jest ustawienie domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="54496-124">This is hello default setting.</span></span>

<span data-ttu-id="54496-125">Jeśli chcesz tooreview administratora i zaakceptuj lub Odrzuć subskrypcji prób toothis produktu, wybierz **wymagają zatwierdzenia subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="54496-125">If you want an administrator tooreview and accept or reject subscription attempts toothis product, select **Require subscription approval**.</span></span> <span data-ttu-id="54496-126">Jeśli nie zaznaczono pola wyboru hello, prób subskrypcji zostaną automatycznie zatwierdzone.</span><span class="sxs-lookup"><span data-stu-id="54496-126">If hello check box is not selected, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="54496-127">W tym przykładzie subskrypcje są automatycznie zatwierdzane, więc nie zaznaczaj pola hello.</span><span class="sxs-lookup"><span data-stu-id="54496-127">In this example, subscriptions are automatically approved, so do not select hello box.</span></span>

<span data-ttu-id="54496-128">Deweloper tooallow kont toosubscribe wielokrotnie toohello nowego produktu wybierz hello **zezwalać na wiele równoczesnych subskrypcji** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="54496-128">tooallow developer accounts toosubscribe multiple times toohello new product, select hello **Allow multiple simultaneous subscriptions** check box.</span></span> <span data-ttu-id="54496-129">Ten samouczek nie wykorzystuje wielu jednoczesnych subskrypcji, więc pozostaw to pole niezaznaczone.</span><span class="sxs-lookup"><span data-stu-id="54496-129">This tutorial does not utilize multiple simultaneous subscriptions, so leave it unchecked.</span></span>

<span data-ttu-id="54496-130">Po wprowadzeniu wszystkich wartości kliknij **zapisać** toocreate hello produktu.</span><span class="sxs-lookup"><span data-stu-id="54496-130">After all values are entered, click **Save** toocreate hello product.</span></span>

![Dodany produkt][api-management-product-added]

<span data-ttu-id="54496-132">Domyślnie nowe produkty są widoczne toousers w hello **Administratorzy** grupy.</span><span class="sxs-lookup"><span data-stu-id="54496-132">By default, new products are visible toousers in hello **Administrators** group.</span></span> <span data-ttu-id="54496-133">Zamierzamy tooadd hello **deweloperzy** grupy.</span><span class="sxs-lookup"><span data-stu-id="54496-133">We are going tooadd hello **Developers** group.</span></span> <span data-ttu-id="54496-134">Kliknij przycisk **bezpłatnej wersji próbnej**, a następnie kliknij przycisk hello **widoczność** kartę.</span><span class="sxs-lookup"><span data-stu-id="54496-134">Click **Free Trial**, and then click hello **Visibility** tab.</span></span>

> <span data-ttu-id="54496-135">W usłudze API Management grupy są używane toomanage widoczność hello toodevelopers produktów.</span><span class="sxs-lookup"><span data-stu-id="54496-135">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="54496-136">Produkty Udziel toogroups widoczność i deweloperzy mogą wyświetlać i subskrybować toohello produktów, które są widoczne toohello grup, w których one należą.</span><span class="sxs-lookup"><span data-stu-id="54496-136">Products grant visibility toogroups, and developers can view and subscribe toohello products that are visible toohello groups in which they belong.</span></span> <span data-ttu-id="54496-137">Aby uzyskać więcej informacji, zobacz [jak toocreate i użycie grup w usłudze Azure API Management][How toocreate and use groups in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="54496-137">For more information, see [How toocreate and use groups in Azure API Management][How toocreate and use groups in Azure API Management].</span></span>
> 
> 

![Dodawanie grupy deweloperów][api-management-add-developers-group]

<span data-ttu-id="54496-139">Wybierz hello **deweloperzy** pole wyboru, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="54496-139">Select hello **Developers** check box, and then click **Save**.</span></span>

## <span data-ttu-id="54496-140"><a name="add-api"></a>produktu toohello tooadd interfejsu API</span><span class="sxs-lookup"><span data-stu-id="54496-140"><a name="add-api"> </a>tooadd an API toohello product</span></span>
<span data-ttu-id="54496-141">W tym kroku samouczka hello dodamy hello Echo API toohello nowego bezpłatnej wersji próbnej produktu.</span><span class="sxs-lookup"><span data-stu-id="54496-141">In this step of hello tutorial, we will add hello Echo API toohello new Free Trial product.</span></span>

> <span data-ttu-id="54496-142">Każde wystąpienie usługi API Management jest wstępnie skonfigurowany z użyciem interfejsu API Echo, które można tooexperiment używanych z i więcej informacji na temat interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="54496-142">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="54496-143">Aby uzyskać więcej informacji, zobacz [Zarządzanie pierwszym interfejsem API w usłudze Azure API Management][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="54496-143">For more information, see [Manage your first API in Azure API Management][Manage your first API in Azure API Management].</span></span>
> 
> 

<span data-ttu-id="54496-144">Kliknij przycisk **produktów** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **bezpłatnej wersji próbnej** tooconfigure hello produktu.</span><span class="sxs-lookup"><span data-stu-id="54496-144">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Konfigurowanie produktu][api-management-configure-product]

<span data-ttu-id="54496-146">Kliknij przycisk **tooproduct dodać interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="54496-146">Click **Add API tooproduct**.</span></span>

![Dodaj tooproduct interfejsu API][api-management-add-api]

<span data-ttu-id="54496-148">Wybierz interfejs **Echo API**, a następnie kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="54496-148">Select **Echo API**, and then click **Save**.</span></span>

![Dodawanie interfejsu Echo API][api-management-add-echo-api]

## <span data-ttu-id="54496-150"><a name="policies"></a>tooconfigure wywołać szybkość zasady, a limit przydziału</span><span class="sxs-lookup"><span data-stu-id="54496-150"><a name="policies"> </a>tooconfigure call rate limit and quota policies</span></span>
<span data-ttu-id="54496-151">Limity szybkości i przydziały są skonfigurowane w edytorze zasad hello.</span><span class="sxs-lookup"><span data-stu-id="54496-151">Rate limits and quotas are configured in hello policy editor.</span></span> <span data-ttu-id="54496-152">Witaj dwie zasady dodamy w tym samouczku są hello [częstotliwość wywołań Limit subskrypcji](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) i [przydział użycia zestawu na subskrypcję](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) zasad.</span><span class="sxs-lookup"><span data-stu-id="54496-152">hello two policies we will be adding in this tutorial are hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="54496-153">Te zasady muszą być stosowane w zakresie produktu hello.</span><span class="sxs-lookup"><span data-stu-id="54496-153">These policies must be applied at hello product scope.</span></span>

<span data-ttu-id="54496-154">Kliknij przycisk **zasady** w obszarze hello **zarządzanie interfejsami API** menu po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="54496-154">Click **Policies** under hello **API Management** menu on hello left.</span></span> <span data-ttu-id="54496-155">W hello **produktu** kliknij **bezpłatnej wersji próbnej**.</span><span class="sxs-lookup"><span data-stu-id="54496-155">In hello **Product** list, click **Free Trial**.</span></span>

![Zasady produktu][api-management-product-policy]

<span data-ttu-id="54496-157">Kliknij przycisk **Dodaj zasady** tooimport hello szablonu zasad i rozpocząć tworzenie hello szybkość zasad limitu i przydziału.</span><span class="sxs-lookup"><span data-stu-id="54496-157">Click **Add Policy** tooimport hello policy template and begin creating hello rate limit and quota policies.</span></span>

![Dodawanie zasad][api-management-add-policy]

<span data-ttu-id="54496-159">Zasady, a limit przydziału szybkość są zasady ruchu przychodzącego, tak pozycji hello kursora w elemencie przychodzących hello.</span><span class="sxs-lookup"><span data-stu-id="54496-159">Rate limit and quota policies are inbound policies, so position hello cursor in hello inbound element.</span></span>

![Edytor zasad][api-management-policy-editor-inbound]

<span data-ttu-id="54496-161">Przewiń listę hello zasad i Znajdź hello **częstotliwość wywołań Limit subskrypcji** wpis zasad.</span><span class="sxs-lookup"><span data-stu-id="54496-161">Scroll through hello list of policies and locate hello **Limit call rate per subscription** policy entry.</span></span>

![Instrukcje zasad][api-management-limit-policies]

<span data-ttu-id="54496-163">Po hello kursor znajduje się w hello **przychodzących** elementu zasad, kliknij strzałkę hello obok **częstotliwość wywołań Limit subskrypcji** tooinsert jego szablonu zasad.</span><span class="sxs-lookup"><span data-stu-id="54496-163">After hello cursor is positioned in hello **inbound** policy element, click hello arrow beside **Limit call rate per subscription** tooinsert its policy template.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

<span data-ttu-id="54496-164">Jak widać w hello fragment, zasad hello umożliwia ustawianie limitów interfejsów API i operacje hello produktu.</span><span class="sxs-lookup"><span data-stu-id="54496-164">As you can see from hello snippet, hello policy allows setting limits for hello product's APIs and operations.</span></span> <span data-ttu-id="54496-165">W tym samouczku firma Microsoft nie używać tej funkcji, aby usunąć hello **interfejsu api** i **operacji** elementy z hello **limit szybkości** element, taki sposób, że tylko hello zewnętrzne **limit szybkości** element pozostaje, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="54496-165">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **rate-limit** element, such that only hello outer **rate-limit** element remains, as shown in hello following example.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

<span data-ttu-id="54496-166">W hello bezpłatnej wersji próbnej produktu, szybkość maksymalna dopuszczalna wywołania hello jest 10 połączeń na minutę, wpisać **10** jako wartość hello hello **wywołania** atrybutu i **60** dla hello **okres odnawiania** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="54496-166">In hello Free Trial product, hello maximum allowable call rate is 10 calls per minute, so type **10** as hello value for hello **calls** attribute, and **60** for hello **renewal-period** attribute.</span></span>

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

<span data-ttu-id="54496-167">tooconfigure hello **przydział użycia zestawu na subskrypcję** zasad, pozycja kursora bezpośrednio pod hello nowo dodanych **limit szybkości** elementu w obrębie hello **przychodzących** element, a następnie odszukaj i kliknij hello Strzałka toohello lewej strony **przydział użycia zestawu na subskrypcję**.</span><span class="sxs-lookup"><span data-stu-id="54496-167">tooconfigure hello **Set usage quota per subscription** policy, position your cursor immediately below hello newly added **rate-limit** element within hello **inbound** element, and then locate and click hello arrow toohello left of **Set usage quota per subscription**.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

<span data-ttu-id="54496-168">Podobnie toohello **przydział użycia zestawu na subskrypcję** zasad, **przydział użycia zestawu na subskrypcję** zasad pozwala na ustawienie informacji o możliwościach dla interfejsów API i operacje hello produktu.</span><span class="sxs-lookup"><span data-stu-id="54496-168">Similarly toohello **Set usage quota per subscription** policy, **Set usage quota per subscription** policy allows setting caps for on hello product's APIs and operations.</span></span> <span data-ttu-id="54496-169">W tym samouczku firma Microsoft nie używać tej funkcji, aby usunąć hello **interfejsu api** i **operacji** elementy z hello **przydziału** element, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="54496-169">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **quota** element, as shown in hello following example.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

<span data-ttu-id="54496-170">Przydziały może bazować na powitania liczba wywołań na interwał i przepustowości.</span><span class="sxs-lookup"><span data-stu-id="54496-170">Quotas can be based on hello number of calls per interval, bandwidth, or both.</span></span> <span data-ttu-id="54496-171">W tym samouczku będziemy są nie ograniczania przepustowości na podstawie, więc usunięcie hello **przepustowości** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="54496-171">In this tutorial, we are not throttling based on bandwidth, so delete hello **bandwidth** attribute.</span></span>

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

<span data-ttu-id="54496-172">Hello bezpłatnej wersji próbnej produktu przydział hello jest wywołania 200 punktów w tygodniu.</span><span class="sxs-lookup"><span data-stu-id="54496-172">In hello Free Trial product, hello quota is 200 calls per week.</span></span> <span data-ttu-id="54496-173">Określ **200** jako wartość hello hello **wywołania** atrybutu, a następnie określ **604800** jako wartość hello hello **okres odnawiania** atrybut.</span><span class="sxs-lookup"><span data-stu-id="54496-173">Specify **200** as hello value for hello **calls** attribute, and then specify **604800** as hello value for hello **renewal-period** attribute.</span></span>

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> <span data-ttu-id="54496-174">Interwały zasad są określane w sekundach.</span><span class="sxs-lookup"><span data-stu-id="54496-174">Policy intervals are specified in seconds.</span></span> <span data-ttu-id="54496-175">Interwał powitania toocalculate na tydzień, należy pomnożyć hello liczbę dni (7) do hello liczbę godzin w ciągu dnia (24) hello liczbę minut w ciągu godziny (60) hello liczby sekund na minutę (60): 7 * 24 * 60 * 60 = 604800.</span><span class="sxs-lookup"><span data-stu-id="54496-175">toocalculate hello interval for a week, you can multiply hello number of days (7) by hello number of hours in a day (24) by hello number of minutes in an hour (60) by hello number of seconds in a minute (60): 7 * 24 * 60 * 60 = 604800.</span></span>
> 
> 

<span data-ttu-id="54496-176">Po zakończeniu konfigurowania zasad hello powinna być zgodna hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="54496-176">When you have finished configuring hello policy, it should match hello following example.</span></span>

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

<span data-ttu-id="54496-177">Po hello potrzeby skonfigurowano zasad, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="54496-177">After hello desired policies are configured, click **Save**.</span></span>

![Zapisywanie zasad][api-management-policy-save]

## <span data-ttu-id="54496-179"><a name="publish-product"></a> toopublish hello produktu</span><span class="sxs-lookup"><span data-stu-id="54496-179"><a name="publish-product"> </a> toopublish hello product</span></span>
<span data-ttu-id="54496-180">Witaj hello dodano interfejsy API i hello zasad są skonfigurowane, hello produktu musi zostać opublikowany, dzięki czemu mogą być używane przez deweloperów.</span><span class="sxs-lookup"><span data-stu-id="54496-180">Now that hello hello APIs are added and hello policies are configured, hello product must be published so that it can be used by developers.</span></span> <span data-ttu-id="54496-181">Kliknij przycisk **produktów** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **bezpłatnej wersji próbnej** tooconfigure hello produktu.</span><span class="sxs-lookup"><span data-stu-id="54496-181">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Konfigurowanie produktu][api-management-configure-product]

<span data-ttu-id="54496-183">Kliknij przycisk **publikowania**, a następnie kliknij przycisk **tak, przed opublikowaniem** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="54496-183">Click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span>

![Publikowanie produktu][api-management-publish-product]

## <span data-ttu-id="54496-185"><a name="subscribe-account"></a>toosubscribe produktu toohello konta dewelopera</span><span class="sxs-lookup"><span data-stu-id="54496-185"><a name="subscribe-account"> </a>toosubscribe a developer account toohello product</span></span>
<span data-ttu-id="54496-186">Teraz tego produktu hello zostanie opublikowana, jest używane przez programistów tooand toobe dostępnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="54496-186">Now that hello product is published, it is available toobe subscribed tooand used by developers.</span></span>

> <span data-ttu-id="54496-187">Administratorzy wystąpienia interfejsu API zarządzania są automatycznie subskrybowanego tooevery produktu.</span><span class="sxs-lookup"><span data-stu-id="54496-187">Administrators of an API Management instance are automatically subscribed tooevery product.</span></span> <span data-ttu-id="54496-188">W tym kroku samouczka firma Microsoft będzie subskrypcji jedną hello dewelopera z systemem innym niż administrator konta toohello bezpłatnej wersji próbnej produktu.</span><span class="sxs-lookup"><span data-stu-id="54496-188">In this tutorial step, we will subscribe one of hello non-administrator developer accounts toohello Free Trial product.</span></span> <span data-ttu-id="54496-189">Jeśli konta dewelopera jest częścią roli Administratorzy hello, następnie można wykonać wraz z tego kroku, nawet jeśli masz już subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="54496-189">If your developer account is part of hello Administrators role, then you can follow along with this step, even though you are already subscribed.</span></span>
> 
> 

<span data-ttu-id="54496-190">Kliknij przycisk **użytkowników** na powitania **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij nazwę hello konta dewelopera.</span><span class="sxs-lookup"><span data-stu-id="54496-190">Click **Users** on hello **API Management** menu on hello left, and then click hello name of your developer account.</span></span> <span data-ttu-id="54496-191">W tym przykładzie używamy hello **Gragg Borowik** konta dewelopera.</span><span class="sxs-lookup"><span data-stu-id="54496-191">In this example, we are using hello **Clayton Gragg** developer account.</span></span>

![Konfigurowanie konta dewelopera][api-management-configure-developer]

<span data-ttu-id="54496-193">Kliknij przycisk **Dodaj subskrypcję**.</span><span class="sxs-lookup"><span data-stu-id="54496-193">Click **Add Subscription**.</span></span>

![Dodawanie subskrypcji][api-management-add-subscription-menu]

<span data-ttu-id="54496-195">Wybierz produkt **Bezpłatna wersja próbna**, a następnie kliknij przycisk **Subskrybuj**.</span><span class="sxs-lookup"><span data-stu-id="54496-195">Select **Free Trial**, and then click **Subscribe**.</span></span>

![Dodawanie subskrypcji][api-management-add-subscription]

> [!NOTE]
> <span data-ttu-id="54496-197">W tym samouczku wiele równoczesnych subskrypcji nie są włączone hello bezpłatnej wersji próbnej produktu.</span><span class="sxs-lookup"><span data-stu-id="54496-197">In this tutorial, multiple simultaneous subscriptions are not enabled for hello Free Trial product.</span></span> <span data-ttu-id="54496-198">Jeśli były, jak pokazano w hello poniższy przykład użytkownik będzie zostanie wyświetlony monit o tooname hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="54496-198">If they were, you would be prompted tooname hello subscription, as shown in hello following example.</span></span>
> 
> 

![Dodawanie subskrypcji][api-management-add-subscription-multiple]

<span data-ttu-id="54496-200">Po kliknięciu przycisku **Subskrybuj**, produktu hello jest wyświetlana w hello **subskrypcji** listę hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="54496-200">After clicking **Subscribe**, hello product appears in hello **Subscription** list for hello user.</span></span>

![Dodana subskrypcja][api-management-subscription-added]

## <span data-ttu-id="54496-202"><a name="test-rate-limit"></a>toocall operacji i testowania limit szybkości hello</span><span class="sxs-lookup"><span data-stu-id="54496-202"><a name="test-rate-limit"> </a>toocall an operation and test hello rate limit</span></span>
<span data-ttu-id="54496-203">Witaj bezpłatnej wersji próbnej produktu jest skonfigurowany, a opublikowana, firma Microsoft wywoływanie niektórych operacji i testowania zasad limitu szybkości hello.</span><span class="sxs-lookup"><span data-stu-id="54496-203">Now that hello Free Trial product is configured and published, we can call some operations and test hello rate limit policy.</span></span>
<span data-ttu-id="54496-204">Przełącznik toohello portalu dla deweloperów, klikając **portalu dla deweloperów** hello prawym górnym menu.</span><span class="sxs-lookup"><span data-stu-id="54496-204">Switch toohello developer portal by clicking **Developer portal** in hello upper-right menu.</span></span>

![Portal dla deweloperów][api-management-developer-portal-menu]

<span data-ttu-id="54496-206">Kliknij przycisk **interfejsów API** w hello menu u góry, a następnie kliknij przycisk **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="54496-206">Click **APIs** in hello top menu, and then click **Echo API**.</span></span>

![Portal dla deweloperów][api-management-developer-portal-api-menu]

<span data-ttu-id="54496-208">Kliknij operację **GET Resource** (pobieranie zasobu), a następnie kliknij przycisk **Wypróbuj**.</span><span class="sxs-lookup"><span data-stu-id="54496-208">Click **GET Resource**, and then click **Try it**.</span></span>

![Otwarta konsola][api-management-open-console]

<span data-ttu-id="54496-210">Zachowaj hello domyślne wartości parametrów, a następnie wybierz klucz subskrypcji hello bezpłatnej wersji próbnej produktu.</span><span class="sxs-lookup"><span data-stu-id="54496-210">Keep hello default parameter values, and then select your subscription key for hello Free Trial product.</span></span>

![Klucz subskrypcji][api-management-select-key]

> [!NOTE]
> <span data-ttu-id="54496-212">Jeśli masz wiele subskrypcji, należy się, że klucz hello tooselect dla **bezpłatnej wersji próbnej**, lub inne zasady hello, które zostały skonfigurowane w poprzednich krokach hello nie będzie obowiązywać.</span><span class="sxs-lookup"><span data-stu-id="54496-212">If you have multiple subscriptions, be sure tooselect hello key for **Free Trial**, or else hello policies that were configured in hello previous steps won't be in effect.</span></span>
> 
> 

<span data-ttu-id="54496-213">Kliknij przycisk **wysyłania**, a następnie Wyświetl hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="54496-213">Click **Send**, and then view hello response.</span></span> <span data-ttu-id="54496-214">Uwaga hello **stanu odpowiedzi** z **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="54496-214">Note hello **Response status** of **200 OK**.</span></span>

![Wyniki operacji][api-management-http-get-results]

<span data-ttu-id="54496-216">Kliknij przycisk **wysyłania** szybkością większa niż hello polityka limit 10 połączeń na minutę.</span><span class="sxs-lookup"><span data-stu-id="54496-216">Click **Send** at a rate greater than hello rate limit policy of 10 calls per minute.</span></span> <span data-ttu-id="54496-217">Po przekroczeniu zasad limitu szybkości hello stan odpowiedzi **429 zbyt wiele żądań** jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="54496-217">After hello rate limit policy is exceeded, a response status of **429 Too Many Requests** is returned.</span></span>

![Wyniki operacji][api-management-http-get-429]

<span data-ttu-id="54496-219">Witaj **zawartości odpowiedzi** wskazuje hello pozostałych Interwał ponownych prób zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="54496-219">hello **Response content** indicates hello remaining interval before retries will be successful.</span></span>

<span data-ttu-id="54496-220">Jeśli obowiązuje zasada limit szybkości hello 10 połączeń na minutę, kolejne wywołania zakończy się niepowodzeniem przed upływem 60 sekund od hello pierwszy hello 10 pomyślnych wywołań toohello produktu przed został przekroczony limit szybkości hello.</span><span class="sxs-lookup"><span data-stu-id="54496-220">When hello rate limit policy of 10 calls per minute is in effect, subsequent calls will fail until 60 seconds have elapsed from hello first of hello 10 successful calls toohello product before hello rate limit was exceeded.</span></span> <span data-ttu-id="54496-221">W tym przykładzie hello pozostałych interwał to 54 sekund.</span><span class="sxs-lookup"><span data-stu-id="54496-221">In this example, hello remaining interval is 54 seconds.</span></span>

## <span data-ttu-id="54496-222"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="54496-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="54496-223">Obejrzyj pokaz ustawienia limitów szybkości i przydziały w powitania po wideo.</span><span class="sxs-lookup"><span data-stu-id="54496-223">Watch a demo of setting rate limits and quotas in hello following video.</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
