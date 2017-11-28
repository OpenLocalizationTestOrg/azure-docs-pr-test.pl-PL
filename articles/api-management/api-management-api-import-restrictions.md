---
title: "Ograniczenia i znane problemy podczas importowania interfejsu API usługi Azure API Management | Dokumentacja firmy Microsoft"
description: "Szczegóły znane problemy i ograniczenia dotyczące importowania do usługi Azure API Management przy użyciu interfejsu API otwarty, WSDL lub WADL formatów."
services: api-management
documentationcenter: 
author: mattfarm
manager: vlvinogr
editor: 
ms.assetid: 7a5a63f0-3e72-49d3-a28c-1bb23ab495e2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: apipm
ms.openlocfilehash: ac799d66b5038c207413086b0fa71239ff2a332f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="api-import-restrictions-and-known-issues"></a><span data-ttu-id="0f725-103">Ograniczenia importu interfejsu API i znane problemy</span><span class="sxs-lookup"><span data-stu-id="0f725-103">API import restrictions and known issues</span></span>
## <a name="about-this-list"></a><span data-ttu-id="0f725-104">Ta lista — informacje</span><span class="sxs-lookup"><span data-stu-id="0f725-104">About this list</span></span>
<span data-ttu-id="0f725-105">Czasie wszelkich starań, aby upewnić się, że importowanie interfejsu API usługi Azure API Management jest jako bezproblemowe i bezproblemowe jak to możliwe, firma Microsoft od czasu do czasu nakłada ograniczenia lub zidentyfikować problemy, które należy rozwiązać, aby można było pomyślnie zaimportować.</span><span class="sxs-lookup"><span data-stu-id="0f725-105">While every effort is made to ensure that importing your API into Azure API Management is as seamless and problem-free as possible, we do occasionally impose restrictions or identify issues that will need to be rectified before you can successfully import.</span></span> <span data-ttu-id="0f725-106">W tym artykule opisano, zorganizowanych w formacie importu interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="0f725-106">This article documents these, organised by the import format of the API.</span></span>

## <span data-ttu-id="0f725-107"><a name="open-api"></a>Otwórz interfejs API/Swagger</span><span class="sxs-lookup"><span data-stu-id="0f725-107"><a name="open-api"> </a>Open API/Swagger</span></span>
<span data-ttu-id="0f725-108">Ogólnie rzecz biorąc, w przypadku otrzymania błędy importowania dokument otwarty interfejs API, upewnij się, zweryfikowaniu jej — przy użyciu narzędzia Projektant nowego portalu Azure (projekt - Front End — Otwórz interfejs API specyfikacji Edytor), lub z 3rd strony narzędzia takie jak <a href="http://www.swagger.io">edytora programu Swagger</a>.</span><span class="sxs-lookup"><span data-stu-id="0f725-108">In general, if you are receiving errors importing your Open API document, please ensure you have validated it - either using the designer in the new Azure Portal (Design - Front End - Open API Specification Editor), or with a 3rd party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.</span></span>

* <span data-ttu-id="0f725-109">**Nazwa hosta** wymagamy atrybutu nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="0f725-109">**Host Name** we require a host name attribute.</span></span>
* <span data-ttu-id="0f725-110">**Podstawowa ścieżka** wymagamy atrybut ścieżki podstawowej.</span><span class="sxs-lookup"><span data-stu-id="0f725-110">**Base Path** we require a base path attribute.</span></span>
* <span data-ttu-id="0f725-111">**Schematy** wymagamy tablicy schematu.</span><span class="sxs-lookup"><span data-stu-id="0f725-111">**Schemes** we require a scheme array.</span></span> 

## <span data-ttu-id="0f725-112"><a name="wsdl"></a>WSDL</span><span class="sxs-lookup"><span data-stu-id="0f725-112"><a name="wsdl"> </a>WSDL</span></span>
<span data-ttu-id="0f725-113">Pliki WSDL są używane do generowania interfejsów API przekazywanego SOAP lub służyć jako zaplecza interfejsu API SOAP-REST.</span><span class="sxs-lookup"><span data-stu-id="0f725-113">WSDL files are used to generate SOAP Pass-through APIs, or serve as the backend of a SOAP-to-REST API.</span></span>

* <span data-ttu-id="0f725-114">**WSDL: import** interfejsów API przy użyciu tego atrybutu nie jest obecnie obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="0f725-114">**WSDL:Import** we do not currently support APIs using this attribute.</span></span> <span data-ttu-id="0f725-115">Klienci, należy scalić importowanych elementów w jednym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="0f725-115">Customers should merge the imported elements into one document.</span></span>
* <span data-ttu-id="0f725-116">**Komunikaty z wielu części** nie są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="0f725-116">**Messages with multiple parts** are currently not supported.</span></span>
* <span data-ttu-id="0f725-117">**WCF wsHttpBinding** usług SOAP utworzone za pomocą programu Windows Communication Foundation należy użyć klasy basicHttpBinding — wsHttpBinding nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="0f725-117">**WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.</span></span>
* <span data-ttu-id="0f725-118">**MTOM** usług przy użyciu mechanizmu MTOM <em>może</em> pracy.</span><span class="sxs-lookup"><span data-stu-id="0f725-118">**MTOM** Services using MTOM <em>may</em> work.</span></span> <span data-ttu-id="0f725-119">W tej chwili nie jest oferowany oficjalnego wsparcia.</span><span class="sxs-lookup"><span data-stu-id="0f725-119">Official support is not offered at this time.</span></span>
* <span data-ttu-id="0f725-120">**Rekursja** typy, które są zdefiniowane cyklicznie (np. Zobacz tablicę sami) nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="0f725-120">**Recursion** types that are defined recursively (e.g. refer to an array of themselves) are not supported.</span></span>

## <span data-ttu-id="0f725-121"><a name="wadl"></a>WADL</span><span class="sxs-lookup"><span data-stu-id="0f725-121"><a name="wadl"> </a>WADL</span></span>
<span data-ttu-id="0f725-122">Obecnie nie istnieją żadne znane problemy importu WADL.</span><span class="sxs-lookup"><span data-stu-id="0f725-122">There are no known WADL import issues currently.</span></span>


[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to cache operation results in Azure API Management]: api-management-howto-cache.md
