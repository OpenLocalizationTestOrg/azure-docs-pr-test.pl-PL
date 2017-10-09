---
title: "aaaImport interfejs API do usługi Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooimport interfejsu API i jego operacji do usługi Azure API Management."
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
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="0306c-103">Jak tooimport hello definicji interfejsu API z operacjami w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="0306c-103">How tooimport hello definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="0306c-104">W usłudze API Management można tworzyć nowych interfejsów API i operacji hello ręcznie dodawać lub hello interfejsu API można zaimportować wraz z operacji hello w jednym kroku.</span><span class="sxs-lookup"><span data-stu-id="0306c-104">In API Management, new APIs can be created and hello operations added manually, or hello API can be imported along with hello operations in one step.</span></span>

<span data-ttu-id="0306c-105">Interfejsy API i ich operacje mogą być importowane przy użyciu następujących formatów hello.</span><span class="sxs-lookup"><span data-stu-id="0306c-105">APIs and their operations can be imported using hello following formats.</span></span>

* <span data-ttu-id="0306c-106">WADL</span><span class="sxs-lookup"><span data-stu-id="0306c-106">WADL</span></span>
* <span data-ttu-id="0306c-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="0306c-107">Swagger</span></span>

<span data-ttu-id="0306c-108">W tym przewodniku pokazano, jak tworzyć nowy interfejs API i zaimportować jego operacji w jednym kroku.</span><span class="sxs-lookup"><span data-stu-id="0306c-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="0306c-109">Informacje dotyczące ręcznego tworzenia interfejsu API i dodawanie działań, zobacz [jak toocreate interfejsów API] [ How toocreate APIs] i [jak tooadd tooan operacje interfejsu API] [ How tooadd operations tooan API].</span><span class="sxs-lookup"><span data-stu-id="0306c-109">For information on manually creating an API and adding operations, see [How toocreate APIs][How toocreate APIs] and [How tooadd operations tooan API][How tooadd operations tooan API].</span></span>

## <span data-ttu-id="0306c-110"><a name="import-api"> </a>Importowanie interfejsu API</span><span class="sxs-lookup"><span data-stu-id="0306c-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="0306c-111">Interfejsy API są tworzone i skonfigurować w portalu wydawcy hello.</span><span class="sxs-lookup"><span data-stu-id="0306c-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="0306c-112">tooaccess hello wydawcy portalu, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="0306c-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="0306c-113">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.</span><span class="sxs-lookup"><span data-stu-id="0306c-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portal wydawcy][api-management-management-console]

<span data-ttu-id="0306c-115">Kliknij przycisk **interfejsów API** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **zaimportować interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="0306c-115">Click **APIs** from hello **API Management** menu on hello left, and then click **import API**.</span></span>

![Interfejs API importu][api-management-import-apis]

<span data-ttu-id="0306c-117">Witaj **Import API** okno ma trzy karty odpowiadające toohello trzy sposoby tooprovide hello interfejsu API specyfikacji.</span><span class="sxs-lookup"><span data-stu-id="0306c-117">hello **Import API** window has three tabs that correspond toohello three ways tooprovide hello API specification.</span></span>

* <span data-ttu-id="0306c-118">**Ze Schowka** umożliwia toopaste specyfikacji hello interfejsu API w polu tekstowym wyznaczonych hello.</span><span class="sxs-lookup"><span data-stu-id="0306c-118">**From clipboard** allows you toopaste hello API specification into hello designated text box.</span></span>
* <span data-ttu-id="0306c-119">**Z pliku** pozwala toobrowse tooand hello wybierz plik, który zawiera specyfikację hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="0306c-119">**From file** allows you toobrowse tooand select hello file that contains hello API specification.</span></span>
* <span data-ttu-id="0306c-120">**Z adresu URL** pozwala toosupply hello adresu URL toohello specyfikacji hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="0306c-120">**From URL** allows you toosupply hello URL toohello specification for hello API.</span></span>

![Format importu interfejsu API][api-management-import-api-clipboard]

<span data-ttu-id="0306c-122">Po podaniu specyfikacji hello interfejsu API, użyj przycisków radiowych hello na powitania prawo tooindicate hello specyfikacji formatu.</span><span class="sxs-lookup"><span data-stu-id="0306c-122">After providing hello API specification, use hello radio buttons on hello right tooindicate hello specification format.</span></span> <span data-ttu-id="0306c-123">Witaj następujące formaty są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="0306c-123">hello following formats are supported.</span></span>

* <span data-ttu-id="0306c-124">WADL</span><span class="sxs-lookup"><span data-stu-id="0306c-124">WADL</span></span>
* <span data-ttu-id="0306c-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="0306c-125">Swagger</span></span>

<span data-ttu-id="0306c-126">Następnie wprowadź **sufiks adresu URL interfejsu API sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="0306c-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="0306c-127">To jest dołączany toohello podstawowego adresu URL dla interfejsu API usługi zarządzania.</span><span class="sxs-lookup"><span data-stu-id="0306c-127">This is appended toohello base URL for your API management service.</span></span> <span data-ttu-id="0306c-128">podstawowy adres URL Hello jest typowe dla wszystkich interfejsów API hostowanych na każde wystąpienie usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="0306c-128">hello base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="0306c-129">Zarządzanie interfejsami API odróżnia interfejsy API według ich sufiks i w związku z tym sufiks hello muszą być unikatowe dla każdego interfejsu API w określonym wystąpieniu usługi interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="0306c-129">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="0306c-130">Po wprowadzeniu wszystkich wartości kliknij **zapisać** toocreate hello API i hello skojarzone operacji.</span><span class="sxs-lookup"><span data-stu-id="0306c-130">Once all values are entered, click **Save** toocreate hello API and hello associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="0306c-131">Samouczek importowania podstawowe Kalkulator interfejsu API w formacie struktury Swagger, zobacz [Zarządzanie pierwszy interfejs API usługi Azure API Management](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0306c-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="0306c-132"><a name="export-api"></a> Wyeksportować interfejsu API</span><span class="sxs-lookup"><span data-stu-id="0306c-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="0306c-133">W tooimporting dodanie nowych interfejsów API, można wyeksportować definicje hello swoje interfejsy API z hello wydawcy portalu.</span><span class="sxs-lookup"><span data-stu-id="0306c-133">In addition tooimporting new APIs, you can export hello definitions of your APIs from hello publisher portal.</span></span> <span data-ttu-id="0306c-134">toodo tak, kliknij przycisk **wyeksportować interfejsu API** z hello **karta Podsumowanie** z Twojej **interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="0306c-134">toodo so, click **Export API** from hello **Summary tab** of your **API**.</span></span>

![Eksportuj interfejsu API][api-management-export-api]

<span data-ttu-id="0306c-136">Interfejsy API można wyeksportować za pomocą WADL lub struktury Swagger.</span><span class="sxs-lookup"><span data-stu-id="0306c-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="0306c-137">Zaznacz pożądany format hello, kliknij przycisk **zapisać**, a następnie wybierz lokalizację hello w plik, który hello toosave.</span><span class="sxs-lookup"><span data-stu-id="0306c-137">Select hello desired format, click **Save**, and choose hello location in which toosave hello file.</span></span>

![Format eksportu interfejsu API][api-management-export-api-format]

## <span data-ttu-id="0306c-139"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0306c-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="0306c-140">Po utworzeniu interfejsu API i operacje hello zaimportowane, można zobaczyć i skonfigurować dodatkowe ustawienia, Dodaj hello interfejsu API tooa produktu, a następnie opublikować go, aby była ona dostępna dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="0306c-140">Once an API is created and hello operations imported, you can review and configure any additional settings, add hello API tooa Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="0306c-141">Aby uzyskać więcej informacji zobacz następujące przewodniki hello.</span><span class="sxs-lookup"><span data-stu-id="0306c-141">For more information, see hello following guides.</span></span>

* <span data-ttu-id="0306c-142">[Jak ustawienia tooconfigure interfejsu API][How tooconfigure API settings]</span><span class="sxs-lookup"><span data-stu-id="0306c-142">[How tooconfigure API settings][How tooconfigure API settings]</span></span>
* <span data-ttu-id="0306c-143">[Jak toocreate i opublikuj produktu][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="0306c-143">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
