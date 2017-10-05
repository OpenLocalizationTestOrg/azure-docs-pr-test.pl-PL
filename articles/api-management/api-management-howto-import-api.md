---
title: "Importowanie interfejsu API usługi Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zaimportować interfejsu API i jego operacji do usługi Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c851b88fc1067e65044266d07775717c028e75d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-the-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="93af3-103">Jak zaimportować definicję interfejsu API z operacjami w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="93af3-103">How to import the definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="93af3-104">W usłudze API Management można tworzyć nowych interfejsów API i operacje ręcznie dodawać lub interfejsu API, które mogą być importowane wraz z operacji w jednym kroku.</span><span class="sxs-lookup"><span data-stu-id="93af3-104">In API Management, new APIs can be created and the operations added manually, or the API can be imported along with the operations in one step.</span></span>

<span data-ttu-id="93af3-105">Interfejsy API i ich operacje mogą być importowane przy użyciu następujących formatów.</span><span class="sxs-lookup"><span data-stu-id="93af3-105">APIs and their operations can be imported using the following formats.</span></span>

* <span data-ttu-id="93af3-106">WADL</span><span class="sxs-lookup"><span data-stu-id="93af3-106">WADL</span></span>
* <span data-ttu-id="93af3-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="93af3-107">Swagger</span></span>

<span data-ttu-id="93af3-108">W tym przewodniku pokazano, jak tworzyć nowy interfejs API i zaimportować jego operacji w jednym kroku.</span><span class="sxs-lookup"><span data-stu-id="93af3-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="93af3-109">Informacje dotyczące ręcznego tworzenia interfejsu API i dodawanie działań, zobacz [Tworzenie interfejsów API] [ How to create APIs] i [sposób dodawania działań do interfejsu API][How to add operations to an API].</span><span class="sxs-lookup"><span data-stu-id="93af3-109">For information on manually creating an API and adding operations, see [How to create APIs][How to create APIs] and [How to add operations to an API][How to add operations to an API].</span></span>

## <span data-ttu-id="93af3-110"><a name="import-api"> </a>Importowanie interfejsu API</span><span class="sxs-lookup"><span data-stu-id="93af3-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="93af3-111">Interfejsy API są tworzone i skonfigurować w portalu wydawcy.</span><span class="sxs-lookup"><span data-stu-id="93af3-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="93af3-112">Aby uzyskać dostęp do portalu wydawcy, kliknij przycisk **portal wydawcy** w portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="93af3-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="93af3-113">Jeśli jeszcze nie masz utworzonego wystąpienia usługi API Management, zobacz [Tworzenie wystąpienia usługi API Management][Create an API Management service instance] w samouczku [Wprowadzenie do usługi Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="93af3-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portal wydawcy][api-management-management-console]

<span data-ttu-id="93af3-115">Kliknij przycisk **interfejsów API** z **zarządzanie interfejsami API** menu po lewej stronie, a następnie kliknij przycisk **zaimportować interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="93af3-115">Click **APIs** from the **API Management** menu on the left, and then click **import API**.</span></span>

![Interfejs API importu][api-management-import-apis]

<span data-ttu-id="93af3-117">**Import API** okno ma trzy karty, które odpowiadają trzy sposoby zapewnienia specyfikacja interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="93af3-117">The **Import API** window has three tabs that correspond to the three ways to provide the API specification.</span></span>

* <span data-ttu-id="93af3-118">**Ze Schowka** umożliwia wklejanie specyfikacja interfejsu API w polu tekstowym wyznaczonych.</span><span class="sxs-lookup"><span data-stu-id="93af3-118">**From clipboard** allows you to paste the API specification into the designated text box.</span></span>
* <span data-ttu-id="93af3-119">**Z pliku** umożliwia Wyszukaj i wybierz plik, który zawiera specyfikację interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="93af3-119">**From file** allows you to browse to and select the file that contains the API specification.</span></span>
* <span data-ttu-id="93af3-120">**Z adresu URL** pozwala podać adres URL w specyfikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="93af3-120">**From URL** allows you to supply the URL to the specification for the API.</span></span>

![Format importu interfejsu API][api-management-import-api-clipboard]

<span data-ttu-id="93af3-122">Po podaniu specyfikacja interfejsu API, użyj przycisków radiowych po prawej stronie, aby wskazać specyfikacji formatu.</span><span class="sxs-lookup"><span data-stu-id="93af3-122">After providing the API specification, use the radio buttons on the right to indicate the specification format.</span></span> <span data-ttu-id="93af3-123">Obsługiwane są następujące formaty.</span><span class="sxs-lookup"><span data-stu-id="93af3-123">The following formats are supported.</span></span>

* <span data-ttu-id="93af3-124">WADL</span><span class="sxs-lookup"><span data-stu-id="93af3-124">WADL</span></span>
* <span data-ttu-id="93af3-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="93af3-125">Swagger</span></span>

<span data-ttu-id="93af3-126">Następnie wprowadź **sufiks adresu URL interfejsu API sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="93af3-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="93af3-127">To jest dołączany do podstawowego adresu URL dla interfejsu API usługi zarządzania.</span><span class="sxs-lookup"><span data-stu-id="93af3-127">This is appended to the base URL for your API management service.</span></span> <span data-ttu-id="93af3-128">Element podstawowy adres URL jest wspólne dla wszystkich interfejsów API hostowanych na każde wystąpienie usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="93af3-128">The base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="93af3-129">Zarządzanie interfejsami API odróżnia interfejsy API według ich sufiks i w związku z tym sufiks muszą być unikatowe dla każdego interfejsu API w określonym wystąpieniu usługi interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="93af3-129">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="93af3-130">Po wprowadzeniu wszystkich wartości kliknij **zapisać** do tworzenia interfejsu API i skojarzone operacji.</span><span class="sxs-lookup"><span data-stu-id="93af3-130">Once all values are entered, click **Save** to create the API and the associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="93af3-131">Samouczek importowania podstawowe Kalkulator interfejsu API w formacie struktury Swagger, zobacz [Zarządzanie pierwszy interfejs API usługi Azure API Management](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="93af3-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="93af3-132"><a name="export-api"></a> Wyeksportować interfejsu API</span><span class="sxs-lookup"><span data-stu-id="93af3-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="93af3-133">Oprócz importowania nowych interfejsów API, możesz wyeksportować definicje swoje interfejsy API z portalu wydawcy.</span><span class="sxs-lookup"><span data-stu-id="93af3-133">In addition to importing new APIs, you can export the definitions of your APIs from the publisher portal.</span></span> <span data-ttu-id="93af3-134">Aby to zrobić, kliknij przycisk **wyeksportować interfejsu API** z **karta Podsumowanie** z Twojej **interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="93af3-134">To do so, click **Export API** from the **Summary tab** of your **API**.</span></span>

![Eksportuj interfejsu API][api-management-export-api]

<span data-ttu-id="93af3-136">Interfejsy API można wyeksportować za pomocą WADL lub struktury Swagger.</span><span class="sxs-lookup"><span data-stu-id="93af3-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="93af3-137">Zaznacz pożądany format, kliknij przycisk **zapisać**i wybierz lokalizację, w której chcesz zapisać plik.</span><span class="sxs-lookup"><span data-stu-id="93af3-137">Select the desired format, click **Save**, and choose the location in which to save the file.</span></span>

![Format eksportu interfejsu API][api-management-export-api-format]

## <span data-ttu-id="93af3-139"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="93af3-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="93af3-140">Po utworzeniu interfejsu API i operacje zaimportowane, możesz przejrzeć i skonfigurować dodatkowe ustawienia, Dodaj interfejs API produktu, a następnie opublikować go, aby była ona dostępna dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="93af3-140">Once an API is created and the operations imported, you can review and configure any additional settings, add the API to a Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="93af3-141">Aby uzyskać więcej informacji zobacz następujące przewodniki.</span><span class="sxs-lookup"><span data-stu-id="93af3-141">For more information, see the following guides.</span></span>

* <span data-ttu-id="93af3-142">[Jak skonfigurować ustawienia interfejsu API][How to configure API settings]</span><span class="sxs-lookup"><span data-stu-id="93af3-142">[How to configure API settings][How to configure API settings]</span></span>
* <span data-ttu-id="93af3-143">[Jak utworzyć i opublikować produktu][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="93af3-143">[How to create and publish a product][How to create and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to create APIs]: api-management-howto-create-apis.md
[How to configure API settings]: api-management-howto-create-apis.md#configure-api-settings
