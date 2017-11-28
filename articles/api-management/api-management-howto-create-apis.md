---
title: "toocreate aaaHow interfejsów API w usłudze Azure API Management"
description: "Dowiedz się, jak toocreate i skonfigurować interfejsów API w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a><span data-ttu-id="9aedc-103">Jak toocreate interfejsów API w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="9aedc-103">How toocreate APIs in Azure API Management</span></span>
<span data-ttu-id="9aedc-104">Interfejs API w usłudze API Management reprezentuje zestaw operacji, które może być wywoływany przez aplikacje klienckie.</span><span class="sxs-lookup"><span data-stu-id="9aedc-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="9aedc-105">Nowe interfejsy API są tworzone w portalu wydawcy hello, a następnie hello potrzebne, że operacje są dodawane.</span><span class="sxs-lookup"><span data-stu-id="9aedc-105">New APIs are created in hello publisher portal, and then hello desired operations are added.</span></span> <span data-ttu-id="9aedc-106">Po dodaniu hello operacje, hello interfejsu API jest dodawany tooa produktu i mogą być publikowane.</span><span class="sxs-lookup"><span data-stu-id="9aedc-106">Once hello operations are added, hello API is added tooa product and can be published.</span></span> <span data-ttu-id="9aedc-107">Po opublikowaniu interfejsu API można subskrybowanego tooand używane przez programistów.</span><span class="sxs-lookup"><span data-stu-id="9aedc-107">Once an API is published, it can be subscribed tooand used by developers.</span></span>

<span data-ttu-id="9aedc-108">Ten przewodnik przedstawia hello pierwszym krokiem w procesie hello: jak toocreate i skonfiguruj nowy interfejs API w usłudze API Management.</span><span class="sxs-lookup"><span data-stu-id="9aedc-108">This guide shows hello first step in hello process: how toocreate and configure a new API in API Management.</span></span> <span data-ttu-id="9aedc-109">Aby uzyskać więcej informacji na operacje dodawania i publikowania produktu, zobacz [jak tooadd tooan operacje interfejsu API] [ How tooadd operations tooan API] i [jak toocreate i opublikuj produktu] [ How toocreate and publish a product].</span><span class="sxs-lookup"><span data-stu-id="9aedc-109">For more information on adding operations and publishing a product, see [How tooadd operations tooan API][How tooadd operations tooan API] and [How toocreate and publish a product][How toocreate and publish a product].</span></span>

## <span data-ttu-id="9aedc-110"><a name="create-new-api"></a>Utwórz nowy interfejs API</span><span class="sxs-lookup"><span data-stu-id="9aedc-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="9aedc-111">Interfejsy API są tworzone i skonfigurować w portalu wydawcy hello.</span><span class="sxs-lookup"><span data-stu-id="9aedc-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="9aedc-112">tooaccess hello wydawcy portalu, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="9aedc-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portal wydawcy][api-management-management-console]

> <span data-ttu-id="9aedc-114">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.</span><span class="sxs-lookup"><span data-stu-id="9aedc-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="9aedc-115">Kliknij przycisk **interfejsów API** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **dodać interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="9aedc-115">Click **APIs** from hello **API Management** menu on hello left, and then click **add API**.</span></span>

![Tworzenie interfejsu API][api-management-create-api]

<span data-ttu-id="9aedc-117">Użyj hello **dodać nowy interfejs API** tooconfigure okna hello nowy interfejs API.</span><span class="sxs-lookup"><span data-stu-id="9aedc-117">Use hello **Add new API** window tooconfigure hello new API.</span></span>

![Dodawanie nowego interfejsu API][api-management-add-new-api]

<span data-ttu-id="9aedc-119">Hello następujące pola są używane tooconfigure hello nowy interfejs API.</span><span class="sxs-lookup"><span data-stu-id="9aedc-119">hello following fields are used tooconfigure hello new API.</span></span>

* <span data-ttu-id="9aedc-120">**Nazwa interfejsu API sieci Web** to unikatowa i opisowa nazwa hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9aedc-120">**Web API name** provides a unique and descriptive name for hello API.</span></span> <span data-ttu-id="9aedc-121">Jest on wyświetlany w portalach hello deweloperów i wydawcy.</span><span class="sxs-lookup"><span data-stu-id="9aedc-121">It is displayed in hello developer and publisher portals.</span></span>
* <span data-ttu-id="9aedc-122">**Adres URL usługi sieci Web** odwołania hello implementacja interfejsu API hello usługi HTTP.</span><span class="sxs-lookup"><span data-stu-id="9aedc-122">**Web service URL** references hello HTTP service implementing hello API.</span></span> <span data-ttu-id="9aedc-123">Zarządzanie interfejsami API przekazuje żądania toothis adres.</span><span class="sxs-lookup"><span data-stu-id="9aedc-123">API management forwards requests toothis address.</span></span>
* <span data-ttu-id="9aedc-124">**Sufiks adresu URL interfejsu API sieci Web** jest dołączany toohello podstawowego adresu URL dla usługi zarządzania hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9aedc-124">**Web API URL suffix** is appended toohello base URL for hello API management service.</span></span> <span data-ttu-id="9aedc-125">podstawowy adres URL Hello jest typowe dla wszystkich interfejsów API hostowanych przez wystąpienie usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="9aedc-125">hello base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="9aedc-126">Zarządzanie interfejsami API odróżnia interfejsy API według ich sufiks i w związku z tym sufiks hello muszą być unikatowe dla każdego interfejsu API dla danego wydawcy.</span><span class="sxs-lookup"><span data-stu-id="9aedc-126">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="9aedc-127">**Schemat adresu URL interfejsu API sieci Web** określa protokoły mogą być używane tooaccess hello API.</span><span class="sxs-lookup"><span data-stu-id="9aedc-127">**Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span> <span data-ttu-id="9aedc-128">HTTPs jest określony, domyślnie.</span><span class="sxs-lookup"><span data-stu-id="9aedc-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="9aedc-129">toooptionally dodać produkt tooa interfejsu API, kliknij polecenie hello **produktów (opcjonalnie)** listy rozwijanej i wybierz produkt.</span><span class="sxs-lookup"><span data-stu-id="9aedc-129">toooptionally add this new API tooa product, click hello **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="9aedc-130">Ten krok może być powtarzane wiele razy tooadd hello interfejsu API toomultiple produktów.</span><span class="sxs-lookup"><span data-stu-id="9aedc-130">This step can be repeated multiple times tooadd hello API toomultiple products.</span></span>

<span data-ttu-id="9aedc-131">Po hello potrzebne wartości są skonfigurowane, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="9aedc-131">Once hello desired values are configured, click **Save**.</span></span> <span data-ttu-id="9aedc-132">Po utworzeniu nowego interfejsu API hello hello strony podsumowania dla interfejsu API hello jest wyświetlana w hello wydawcy portalu.</span><span class="sxs-lookup"><span data-stu-id="9aedc-132">Once hello new API is created, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![Podsumowanie interfejsu API][api-management-api-summary]

## <span data-ttu-id="9aedc-134"><a name="configure-api-settings"></a>Ustawień skonfiguruj interfejsu API</span><span class="sxs-lookup"><span data-stu-id="9aedc-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="9aedc-135">Można użyć hello **ustawienia** karcie tooverify i edytować hello konfigurację interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9aedc-135">You can use hello **Settings** tab tooverify and edit hello configuration for an API.</span></span> <span data-ttu-id="9aedc-136">**Nazwa interfejsu API sieci Web**, **adres URL usługi sieci Web**, i **sufiks adresu URL interfejsu API sieci Web** początkowo są ustawiane podczas hello interfejsu API jest tworzony i mogą być modyfikowane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="9aedc-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when hello API is created and can be modified here.</span></span> <span data-ttu-id="9aedc-137">**Opis** zapewnia opcjonalny opis, a **schemat adresu URL interfejsu API sieci Web** określa protokoły mogą być używane tooaccess hello API.</span><span class="sxs-lookup"><span data-stu-id="9aedc-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span>

![Ustawienia interfejsu API][api-management-api-settings]

<span data-ttu-id="9aedc-139">Uwierzytelnianie bramy tooconfigure hello wewnętrznej bazy danych usługi implementującej hello interfejsu API, wybierz hello **zabezpieczeń** hello kartę **przy użyciu poświadczeń** listy rozwijanej mogą być używane tooconfigure **HTTP podstawowe** lub **certyfikaty klienta** uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="9aedc-139">tooconfigure gateway authentication for hello backend service implementing hello API, select hello **Security** tab. hello **With credentials** drop-down can be used tooconfigure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="9aedc-140">Uwierzytelnianie podstawowe toouse HTTP, wystarczy wprowadzić poświadczenia hello potrzebne.</span><span class="sxs-lookup"><span data-stu-id="9aedc-140">toouse HTTP basic authentication, simply enter hello desired credentials.</span></span> <span data-ttu-id="9aedc-141">Uzyskać przy użyciu uwierzytelniania certyfikatu klienta, zobacz [jak za pomocą klienta usług zaplecza toosecure certyfikatów uwierzytelniania w usłudze Azure API Management][How toosecure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="9aedc-141">For information on using client certificate authentication, see [How toosecure back-end services using client certificate authentication in Azure API Management][How toosecure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="9aedc-142">Witaj **zabezpieczeń** karty mogą być również używane tooconfigure **autoryzacji użytkownika** przy użyciu protokołu OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="9aedc-142">hello **Security** tab can also be used tooconfigure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="9aedc-143">Aby uzyskać więcej informacji, zobacz [jak kont przy użyciu narzędzia Projektant tooauthorize OAuth 2.0 w usłudze Azure API Management][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="9aedc-143">For more information, see [How tooauthorize developer accounts using OAuth 2.0 in Azure API Management][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Ustawień uwierzytelniania podstawowego][api-management-api-settings-credentials]

<span data-ttu-id="9aedc-145">Kliknij przycisk **zapisać** toosave wszystkie wprowadzone zmiany toohello ustawień interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9aedc-145">Click **Save** toosave any changes you make toohello API settings.</span></span>

## <span data-ttu-id="9aedc-146"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9aedc-146"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="9aedc-147">Po utworzeniu interfejsu API i skonfigurowane ustawienia hello, hello następne kroki są tooadd hello operacji toohello interfejsu API, Dodaj hello interfejsu API tooa produktu, a następnie opublikować go, aby była ona dostępna dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="9aedc-147">Once an API is created and hello settings configured, hello next steps are tooadd hello operations toohello API, add hello API tooa product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="9aedc-148">Aby uzyskać więcej informacji zobacz następujące artykuły hello.</span><span class="sxs-lookup"><span data-stu-id="9aedc-148">For more information, see hello following articles.</span></span>

* <span data-ttu-id="9aedc-149">[Jak tooadd tooan operacje interfejsu API][How tooadd operations tooan API]</span><span class="sxs-lookup"><span data-stu-id="9aedc-149">[How tooadd operations tooan API][How tooadd operations tooan API]</span></span>
* <span data-ttu-id="9aedc-150">[Jak toocreate i opublikuj produktu][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="9aedc-150">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
