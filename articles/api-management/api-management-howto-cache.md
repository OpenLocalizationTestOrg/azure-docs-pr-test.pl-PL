---
title: "buforowanie tooimprove wydajności w usłudze Azure API Management aaaAdd | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak załadować tooimprove hello opóźnień, przepustowości i usługi sieci web dla wywołania usługi Zarządzanie interfejsami API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a><span data-ttu-id="d3e24-103">Dodaj buforowania wydajności tooimprove w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="d3e24-103">Add caching tooimprove performance in Azure API Management</span></span>
<span data-ttu-id="d3e24-104">Operacje w usłudze API Management można skonfigurować do buforowania odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d3e24-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="d3e24-105">Buforowanie odpowiedzi może znacznie zmniejszyć opóźnienie interfejsu API, zużycie przepustowości i obciążenie usługi sieci Web w przypadku danych, które nie zmieniają się często.</span><span class="sxs-lookup"><span data-stu-id="d3e24-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="d3e24-106">W tym przewodniku przedstawiono odpowiedzi tooadd buforowanie do interfejsu API i skonfigurować zasady dla operacji interfejsu API Echo przykład hello.</span><span class="sxs-lookup"><span data-stu-id="d3e24-106">This guide shows you how tooadd response caching for your API and configure policies for hello sample Echo API operations.</span></span> <span data-ttu-id="d3e24-107">Następnie można wywołać operacji hello w pamięci podręcznej tooverify portalu deweloperów hello w akcji.</span><span class="sxs-lookup"><span data-stu-id="d3e24-107">You can then call hello operation from hello developer portal tooverify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="d3e24-108">Aby poznać informacje na temat buforowania elementów według kluczy przy użyciu wyrażeń zasad, zobacz artykuł [Custom caching in Azure API Management](api-management-sample-cache-by-key.md) (Niestandardowe buforowanie w usłudze Azure API Management).</span><span class="sxs-lookup"><span data-stu-id="d3e24-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d3e24-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d3e24-109">Prerequisites</span></span>
<span data-ttu-id="d3e24-110">Przed hello następujące kroki w tym przewodniku, należy dysponować wystąpienia usługi Zarządzanie interfejsami API z interfejsu API i skonfigurować produkt.</span><span class="sxs-lookup"><span data-stu-id="d3e24-110">Before following hello steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="d3e24-111">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.</span><span class="sxs-lookup"><span data-stu-id="d3e24-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="d3e24-112"><a name="configure-caching"> </a>Konfigurowanie operacji do buforowania</span><span class="sxs-lookup"><span data-stu-id="d3e24-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="d3e24-113">W tym kroku należy przejrzeć ustawienia hello buforowania hello **UZYSKAĆ zasobów (buforowanej)** operacji próbki hello Echo interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d3e24-113">In this step, you will review hello caching settings of hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="d3e24-114">Każde wystąpienie usługi Zarządzanie interfejsami API ma wstępnie skonfigurowane z interfejsem API Echo, które można tooexperiment używanych z i więcej informacji na temat interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="d3e24-114">Each API Management service instance comes preconfigured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="d3e24-115">Aby uzyskać więcej informacji, zobacz [Wprowadzenie do usługi Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="d3e24-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="d3e24-116">tooget pracę, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="d3e24-116">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="d3e24-117">Trwa toohello zarządzanie interfejsami API wydawcy portalu.</span><span class="sxs-lookup"><span data-stu-id="d3e24-117">This takes you toohello API Management publisher portal.</span></span>

![Portal wydawcy][api-management-management-console]

<span data-ttu-id="d3e24-119">Kliknij przycisk **interfejsów API** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="d3e24-119">Click **APIs** from hello **API Management** menu on hello left, and then click **Echo API**.</span></span>

![Interfejs Echo API][api-management-echo-api]

<span data-ttu-id="d3e24-121">Kliknij hello **operacji** , a następnie kliknij pozycję hello **UZYSKAĆ zasobów (buforowanej)** operacji hello **operacji** listy.</span><span class="sxs-lookup"><span data-stu-id="d3e24-121">Click hello **Operations** tab, and then click hello **GET Resource (cached)** operation from hello **Operations** list.</span></span>

![Operacje interfejsu Echo API][api-management-echo-api-operations]

<span data-ttu-id="d3e24-123">Kliknij przycisk hello **buforowanie** hello tooview kartę Ustawienia dla tej operacji pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d3e24-123">Click hello **Caching** tab tooview hello caching settings for this operation.</span></span>

![Karta Buforowanie][api-management-caching-tab]

<span data-ttu-id="d3e24-125">tooenable buforowanie dla operacji select hello **włączyć** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="d3e24-125">tooenable caching for an operation, select hello **Enable** check box.</span></span> <span data-ttu-id="d3e24-126">W tym przykładzie buforowanie jest włączone.</span><span class="sxs-lookup"><span data-stu-id="d3e24-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="d3e24-127">Wyznaczaną każdej operacji odpowiedzi, na podstawie wartości hello w hello **różne parametry ciągu zapytania** i **Vary przez nagłówki** pola.</span><span class="sxs-lookup"><span data-stu-id="d3e24-127">Each operation response is keyed, based on hello values in hello **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="d3e24-128">Jeśli chcesz toocache wiele odpowiedzi na podstawie parametrów ciągu zapytania lub nagłówków, można je skonfigurować w tych dwóch pól.</span><span class="sxs-lookup"><span data-stu-id="d3e24-128">If you want toocache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="d3e24-129">**Czas trwania** Określa interwał wygaśnięcia powitania hello buforowane odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d3e24-129">**Duration** specifies hello expiration interval of hello cached responses.</span></span> <span data-ttu-id="d3e24-130">W tym przykładzie jest interwał powitania **3600** sekund, co jest równoważne tooone godzinę.</span><span class="sxs-lookup"><span data-stu-id="d3e24-130">In this example, hello interval is **3600** seconds, which is equivalent tooone hour.</span></span>

<span data-ttu-id="d3e24-131">Przy użyciu hello konfiguracji w tym przykładzie buforowania, hello pierwszego żądania toohello **UZYSKAĆ zasobów (buforowanej)** operacji zwraca odpowiedź z usługi zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="d3e24-131">Using hello caching configuration in this example, hello first request toohello **GET Resource (cached)** operation returns a response from hello backend service.</span></span> <span data-ttu-id="d3e24-132">Tej odpowiedzi będą buforowane, wyznaczaną przez hello określone parametry nagłówki i zapytania.</span><span class="sxs-lookup"><span data-stu-id="d3e24-132">This response will be cached, keyed by hello specified headers and query string parameters.</span></span> <span data-ttu-id="d3e24-133">Kolejne wywołania operacji toohello z pasujących parametrów, będzie mieć hello buforować odpowiedź zwrócona, dopóki interwał czasu trwania pamięci podręcznej hello utracił ważność.</span><span class="sxs-lookup"><span data-stu-id="d3e24-133">Subsequent calls toohello operation, with matching parameters, will have hello cached response returned, until hello cache duration interval has expired.</span></span>

## <span data-ttu-id="d3e24-134"><a name="caching-policies"></a>Hello przeglądu buforowanie zasad</span><span class="sxs-lookup"><span data-stu-id="d3e24-134"><a name="caching-policies"> </a>Review hello caching policies</span></span>
<span data-ttu-id="d3e24-135">W tym kroku, przejrzyj hello buforowanie ustawienia hello **UZYSKAĆ zasobów (buforowanej)** operacji próbki hello Echo interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d3e24-135">In this step, you review hello caching settings for hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

<span data-ttu-id="d3e24-136">Jeśli skonfigurowano ustawienia buforowania dla operacji na powitania **buforowanie** karcie buforowanie zasad są dodawane do operacji hello.</span><span class="sxs-lookup"><span data-stu-id="d3e24-136">When caching settings are configured for an operation on hello **Caching** tab, caching policies are added for hello operation.</span></span> <span data-ttu-id="d3e24-137">Te zasady można wyświetlać i edytować w edytorze zasad hello.</span><span class="sxs-lookup"><span data-stu-id="d3e24-137">These policies can be viewed and edited in hello policy editor.</span></span>

<span data-ttu-id="d3e24-138">Kliknij przycisk **zasady** z hello **zarządzanie interfejsami API** menu na powitania po lewej stronie, a następnie wybierz **Echo API / GET zasobów (buforowanej)** z hello **operacji**listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d3e24-138">Click **Policies** from hello **API Management** menu on hello left, and then select **Echo API / GET Resource (cached)** from hello **Operation** drop-down list.</span></span>

![Operacja zakresu zasad][api-management-operation-dropdown]

<span data-ttu-id="d3e24-140">W edytorze zasad hello zostaną wyświetlone powitalne zasad dla tej operacji.</span><span class="sxs-lookup"><span data-stu-id="d3e24-140">This displays hello policies for this operation in hello policy editor.</span></span>

![Edytor zasad usługi API Management][api-management-policy-editor]

<span data-ttu-id="d3e24-142">Witaj definicji zasad dla tej operacji zawiera zasady hello definiujące hello buforowanie konfiguracji, które zostały sprawdzone za pomocą hello **buforowanie** kartę hello poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="d3e24-142">hello policy definition for this operation includes hello policies that define hello caching configuration that were reviewed using hello **Caching** tab in hello previous step.</span></span>

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> <span data-ttu-id="d3e24-143">Buforowanie zasad w edytorze zasad hello toohello zmiany zostaną odzwierciedlone na powitania **buforowanie** kartę operację, i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="d3e24-143">Changes made toohello caching policies in hello policy editor will be reflected on hello **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="d3e24-144"><a name="test-operation"></a>Wywołania operacji i przetestować hello buforowanie</span><span class="sxs-lookup"><span data-stu-id="d3e24-144"><a name="test-operation"> </a>Call an operation and test hello caching</span></span>
<span data-ttu-id="d3e24-145">Witaj toosee buforowania w akcji, możemy wywołać operację hello z hello portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="d3e24-145">toosee hello caching in action, we can call hello operation from hello developer portal.</span></span> <span data-ttu-id="d3e24-146">Kliknij przycisk **portalu dla deweloperów** w menu u góry prawo hello.</span><span class="sxs-lookup"><span data-stu-id="d3e24-146">Click **Developer portal** in hello top right menu.</span></span>

![Portal dla deweloperów][api-management-developer-portal-menu]

<span data-ttu-id="d3e24-148">Kliknij przycisk **interfejsów API** w hello menu u góry, a następnie wybierz **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="d3e24-148">Click **APIs** in hello top menu, and then select **Echo API**.</span></span>

![Interfejs Echo API][api-management-apis-echo-api]

> <span data-ttu-id="d3e24-150">Jeśli masz tylko jeden interfejs API skonfigurowane lub tooyour widoczne konta, klikając interfejsów API przejście bezpośrednio toohello operacji dla tego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d3e24-150">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="d3e24-151">Wybierz hello **UZYSKAĆ zasobów (buforowanej)** operacji, a następnie kliknij przycisk **Otwórz konsolę**.</span><span class="sxs-lookup"><span data-stu-id="d3e24-151">Select hello **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![Otwarta konsola][api-management-open-console]

<span data-ttu-id="d3e24-153">Konsola Hello umożliwia operacji tooinvoke bezpośrednio z portalu dla deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="d3e24-153">hello console allows you tooinvoke operations directly from hello developer portal.</span></span>

![Konsola][api-management-console]

<span data-ttu-id="d3e24-155">Zachowaj wartości domyślne hello **param1** i **param2**.</span><span class="sxs-lookup"><span data-stu-id="d3e24-155">Keep hello default values for **param1** and **param2**.</span></span>

<span data-ttu-id="d3e24-156">Wybierz hello inny klawisz z hello **klucza subskrypcji** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d3e24-156">Select hello desired key from hello **subscription-key** drop-down list.</span></span> <span data-ttu-id="d3e24-157">Jeśli Twoje konto ma tylko jedną subskrypcję, zostanie ona od razu wybrana.</span><span class="sxs-lookup"><span data-stu-id="d3e24-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="d3e24-158">Wprowadź **sampleheader:value1** w hello **nagłówki żądań** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d3e24-158">Enter **sampleheader:value1** in hello **Request headers** text box.</span></span>

<span data-ttu-id="d3e24-159">Kliknij przycisk **HTTP Get** i zanotuj hello nagłówków odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d3e24-159">Click **HTTP Get** and make a note of hello response headers.</span></span>

<span data-ttu-id="d3e24-160">Wprowadź **sampleheader:value2** w hello **nagłówki żądań** polu tekstowym, a następnie kliknij przycisk **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="d3e24-160">Enter **sampleheader:value2** in hello **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="d3e24-161">Należy zwrócić uwagę tej wartości hello **sampleheader** jest nadal **wartość1** hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d3e24-161">Note that hello value of **sampleheader** is still **value1** in hello response.</span></span> <span data-ttu-id="d3e24-162">Spróbuj niektórych różne wartości i należy pamiętać, że hello buforowanej odpowiedzi z pierwszym wywołaniu hello są zwracane.</span><span class="sxs-lookup"><span data-stu-id="d3e24-162">Try some different values and note that hello cached response from hello first call is returned.</span></span>

<span data-ttu-id="d3e24-163">Wprowadź **25** do hello **param2** pola, a następnie kliknij przycisk **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="d3e24-163">Enter **25** into hello **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="d3e24-164">Należy zwrócić uwagę tej wartości hello **sampleheader** w hello odpowiedź jest teraz **wartość2**.</span><span class="sxs-lookup"><span data-stu-id="d3e24-164">Note that hello value of **sampleheader** in hello response is now **value2**.</span></span> <span data-ttu-id="d3e24-165">Ponieważ wyniki operacji hello są wyznaczaną przez ciąg zapytania, nie został zwrócony hello poprzedniej odpowiedzi pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d3e24-165">Because hello operation results are keyed by query string, hello previous cached response was not returned.</span></span>

## <span data-ttu-id="d3e24-166"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d3e24-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="d3e24-167">Aby uzyskać więcej informacji na temat zasad buforowania, zobacz [buforowanie zasad] [ Caching policies] w hello [informacje o zasadach usługi API Management][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="d3e24-167">For more information about caching policies, see [Caching policies][Caching policies] in hello [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="d3e24-168">Aby poznać informacje na temat buforowania elementów według kluczy przy użyciu wyrażeń zasad, zobacz artykuł [Custom caching in Azure API Management](api-management-sample-cache-by-key.md) (Niestandardowe buforowanie w usłudze Azure API Management).</span><span class="sxs-lookup"><span data-stu-id="d3e24-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
