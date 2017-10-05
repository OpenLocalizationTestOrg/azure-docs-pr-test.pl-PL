---
title: "Tworzenie interfejsów API w usłudze Azure API Management"
description: "Dowiedz się, jak utworzyć i skonfigurować interfejsów API w usłudze Azure API Management."
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
ms.openlocfilehash: ab08256fbc3caca05bf23a12016ad2acf4fc7412
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-apis-in-azure-api-management"></a><span data-ttu-id="2a2c1-103">Tworzenie interfejsów API w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="2a2c1-103">How to create APIs in Azure API Management</span></span>
<span data-ttu-id="2a2c1-104">Interfejs API w usłudze API Management reprezentuje zestaw operacji, które może być wywoływany przez aplikacje klienckie.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="2a2c1-105">Nowe interfejsy API są tworzone w portalu wydawcy, a następnie są dodawane żądanej operacji.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-105">New APIs are created in the publisher portal, and then the desired operations are added.</span></span> <span data-ttu-id="2a2c1-106">Po dodaniu działania, interfejsu API jest dodawany do produktu i mogą być publikowane.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-106">Once the operations are added, the API is added to a product and can be published.</span></span> <span data-ttu-id="2a2c1-107">Po opublikowaniu interfejsu API można zasubskrybować i używane przez programistów.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-107">Once an API is published, it can be subscribed to and used by developers.</span></span>

<span data-ttu-id="2a2c1-108">Ten przewodnik przedstawia pierwszym krokiem w procesie: jak tworzyć i konfigurować nowy interfejs API w usłudze API Management.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-108">This guide shows the first step in the process: how to create and configure a new API in API Management.</span></span> <span data-ttu-id="2a2c1-109">Aby uzyskać więcej informacji na operacje dodawania i publikowania produktu, zobacz [sposób dodawania działań do interfejsu API] [ How to add operations to an API] i [jak tworzyć i publikować produktu][How to create and publish a product].</span><span class="sxs-lookup"><span data-stu-id="2a2c1-109">For more information on adding operations and publishing a product, see [How to add operations to an API][How to add operations to an API] and [How to create and publish a product][How to create and publish a product].</span></span>

## <span data-ttu-id="2a2c1-110"><a name="create-new-api"></a>Utwórz nowy interfejs API</span><span class="sxs-lookup"><span data-stu-id="2a2c1-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="2a2c1-111">Interfejsy API są tworzone i skonfigurować w portalu wydawcy.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="2a2c1-112">Aby uzyskać dostęp do portalu wydawcy, kliknij przycisk **portal wydawcy** w portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portal wydawcy][api-management-management-console]

> <span data-ttu-id="2a2c1-114">Jeśli jeszcze nie masz utworzonego wystąpienia usługi API Management, zobacz [Tworzenie wystąpienia usługi API Management][Create an API Management service instance] w samouczku [Wprowadzenie do usługi Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2a2c1-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="2a2c1-115">Kliknij przycisk **interfejsów API** z **zarządzanie interfejsami API** menu po lewej stronie, a następnie kliknij przycisk **dodać interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-115">Click **APIs** from the **API Management** menu on the left, and then click **add API**.</span></span>

![Tworzenie interfejsu API][api-management-create-api]

<span data-ttu-id="2a2c1-117">Użyj **dodać nowy interfejs API** okno, aby skonfigurować nowy interfejs API.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-117">Use the **Add new API** window to configure the new API.</span></span>

![Dodawanie nowego interfejsu API][api-management-add-new-api]

<span data-ttu-id="2a2c1-119">Następujące pola są używane do konfigurowania nowego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-119">The following fields are used to configure the new API.</span></span>

* <span data-ttu-id="2a2c1-120">**Nazwa interfejsu API sieci Web** to unikatowa i opisowa nazwa interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-120">**Web API name** provides a unique and descriptive name for the API.</span></span> <span data-ttu-id="2a2c1-121">Jest on wyświetlany w portalach deweloperów i wydawcy.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-121">It is displayed in the developer and publisher portals.</span></span>
* <span data-ttu-id="2a2c1-122">**Adres URL usługi sieci Web** odwołuje się do usługi HTTP implementacja interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-122">**Web service URL** references the HTTP service implementing the API.</span></span> <span data-ttu-id="2a2c1-123">Zarządzanie interfejsami API przekazuje żądania do tego adresu.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-123">API management forwards requests to this address.</span></span>
* <span data-ttu-id="2a2c1-124">**Sufiks adresu URL interfejsu API sieci Web** jest dołączany do podstawowego adresu URL dla interfejsu API usługi zarządzania.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-124">**Web API URL suffix** is appended to the base URL for the API management service.</span></span> <span data-ttu-id="2a2c1-125">Element podstawowy adres URL jest wspólne dla wszystkich interfejsów API hostowanych przez wystąpienie usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-125">The base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="2a2c1-126">Zarządzanie interfejsami API odróżnia interfejsy API według ich sufiks i w związku z tym sufiks muszą być unikatowe dla każdego interfejsu API dla danego wydawcy.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-126">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="2a2c1-127">**Schemat adresu URL interfejsu API sieci Web** określa protokoły mogą być używane do dostępu do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-127">**Web API URL scheme** determines which protocols can be used to access the API.</span></span> <span data-ttu-id="2a2c1-128">HTTPs jest określony, domyślnie.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="2a2c1-129">Opcjonalnie można dodać ten nowy interfejs API do produktu, kliknij przycisk **produktów (opcjonalnie)** listy rozwijanej i wybierz produkt.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-129">To optionally add this new API to a product, click the **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="2a2c1-130">Ten krok można powtarzać wielokrotnie dodać interfejsu API do wielu produktów.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-130">This step can be repeated multiple times to add the API to multiple products.</span></span>

<span data-ttu-id="2a2c1-131">Po skonfigurowaniu odpowiednie wartości, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-131">Once the desired values are configured, click **Save**.</span></span> <span data-ttu-id="2a2c1-132">Po utworzeniu nowego interfejsu API, stronie podsumowania dla interfejsu API jest wyświetlana w portalu wydawcy.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-132">Once the new API is created, the summary page for the API is displayed in the publisher portal.</span></span>

![Podsumowanie interfejsu API][api-management-api-summary]

## <span data-ttu-id="2a2c1-134"><a name="configure-api-settings"></a>Ustawień skonfiguruj interfejsu API</span><span class="sxs-lookup"><span data-stu-id="2a2c1-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="2a2c1-135">Można użyć **ustawienia** kartę, aby sprawdzić i Edytuj konfigurację interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-135">You can use the **Settings** tab to verify and edit the configuration for an API.</span></span> <span data-ttu-id="2a2c1-136">**Nazwa interfejsu API sieci Web**, **adres URL usługi sieci Web**, i **sufiks adresu URL interfejsu API sieci Web** początkowo są ustawiane podczas interfejsu API jest tworzony i mogą być modyfikowane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when the API is created and can be modified here.</span></span> <span data-ttu-id="2a2c1-137">**Opis** zapewnia opcjonalny opis, a **schemat adresu URL interfejsu API sieci Web** określa protokoły mogą być używane do dostępu do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used to access the API.</span></span>

![Ustawienia interfejsu API][api-management-api-settings]

<span data-ttu-id="2a2c1-139">Aby skonfigurować uwierzytelnianie bramy dla implementacji interfejsu API usługi wewnętrznej bazy danych, wybierz **zabezpieczeń** kartę.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-139">To configure gateway authentication for the backend service implementing the API, select the **Security** tab.</span></span> <span data-ttu-id="2a2c1-140">**Przy użyciu poświadczeń** listy rozwijanej może służyć do konfigurowania **podstawowe HTTP** lub **certyfikaty klienta** uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-140">The **With credentials** drop-down can be used to configure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="2a2c1-141">Aby użyć uwierzytelniania podstawowego HTTP, wystarczy wprowadzić odpowiednie poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-141">To use HTTP basic authentication, simply enter the desired credentials.</span></span> <span data-ttu-id="2a2c1-142">Uzyskać przy użyciu uwierzytelniania certyfikatu klienta, zobacz [zabezpieczania usług zaplecza za pomocą klienta uwierzytelniania certyfikatów w usłudze Azure API Management][How to secure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2a2c1-142">For information on using client certificate authentication, see [How to secure back-end services using client certificate authentication in Azure API Management][How to secure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="2a2c1-143">**Zabezpieczeń** kartę można również skonfigurować **autoryzacji użytkownika** przy użyciu protokołu OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-143">The **Security** tab can also be used to configure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="2a2c1-144">Aby uzyskać więcej informacji, zobacz [sposób autoryzowania konta dewelopera przy użyciu protokołu OAuth 2.0 w usłudze Azure API Management][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2a2c1-144">For more information, see [How to authorize developer accounts using OAuth 2.0 in Azure API Management][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Ustawień uwierzytelniania podstawowego][api-management-api-settings-credentials]

<span data-ttu-id="2a2c1-146">Kliknij przycisk **zapisać** zapisać jakiekolwiek zmiany ustawień interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-146">Click **Save** to save any changes you make to the API settings.</span></span>

## <span data-ttu-id="2a2c1-147"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2a2c1-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="2a2c1-148">Po utworzeniu interfejsu API i skonfigurowane ustawienia następne kroki jest dodać operacje interfejsu API, Dodaj interfejs API produktu, a następnie opublikować go, aby była ona dostępna dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-148">Once an API is created and the settings configured, the next steps are to add the operations to the API, add the API to a product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="2a2c1-149">Aby uzyskać więcej informacji zobacz następujące artykuły.</span><span class="sxs-lookup"><span data-stu-id="2a2c1-149">For more information, see the following articles.</span></span>

* <span data-ttu-id="2a2c1-150">[Jak dodać operacje do interfejsu API][How to add operations to an API]</span><span class="sxs-lookup"><span data-stu-id="2a2c1-150">[How to add operations to an API][How to add operations to an API]</span></span>
* <span data-ttu-id="2a2c1-151">[Jak utworzyć i opublikować produktu][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="2a2c1-151">[How to create and publish a product][How to create and publish a product]</span></span>

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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How to secure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How to authorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
