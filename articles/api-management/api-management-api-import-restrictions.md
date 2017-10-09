---
title: Importuj aaaRestrictions i znane problemy w Azure API Management API | Dokumentacja firmy Microsoft
description: "Szczegóły znane problemy i ograniczenia dotyczące importowania do formatu hello otwarty interfejs API, WSDL lub WADL zarządzanie interfejsami API Azure."
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
ms.openlocfilehash: 0bed5ace47de6ccbfbecba25ea6b69c5329de089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="api-import-restrictions-and-known-issues"></a><span data-ttu-id="cdd9e-103">Ograniczenia importu interfejsu API i znane problemy</span><span class="sxs-lookup"><span data-stu-id="cdd9e-103">API import restrictions and known issues</span></span>
## <a name="about-this-list"></a><span data-ttu-id="cdd9e-104">Ta lista — informacje</span><span class="sxs-lookup"><span data-stu-id="cdd9e-104">About this list</span></span>
<span data-ttu-id="cdd9e-105">Podczas wszelkich starań, staje się tooensure tego interfejsu API importowania do usługi Azure API Management jest jako bezproblemowe i bezproblemowe jak to możliwe, możemy od czasu do czasu nakładają ograniczenia lub zidentyfikować problemy wymagające naprawy, aby można było pomyślnie zaimportować toobe.</span><span class="sxs-lookup"><span data-stu-id="cdd9e-105">While every effort is made tooensure that importing your API into Azure API Management is as seamless and problem-free as possible, we do occasionally impose restrictions or identify issues that will need toobe rectified before you can successfully import.</span></span> <span data-ttu-id="cdd9e-106">W tym artykule opisano, zorganizowanych przez format importu hello hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="cdd9e-106">This article documents these, organised by hello import format of hello API.</span></span>

## <span data-ttu-id="cdd9e-107"><a name="open-api"></a>Otwórz interfejs API/Swagger</span><span class="sxs-lookup"><span data-stu-id="cdd9e-107"><a name="open-api"> </a>Open API/Swagger</span></span>
<span data-ttu-id="cdd9e-108">Ogólnie rzecz biorąc, jeśli otrzymujesz błędy importowania dokument otwarty interfejs API, sprawdź, czy zweryfikowaniu jej — za pomocą projektanta hello w hello nowego portalu Azure (projekt - Front End — Otwórz Edytor rozszerzenia interfejsu API specyfikacji) lub z 3rd strony narzędzia takie jak <a href="http://www.swagger.io"> Edytora programu swagger</a>.</span><span class="sxs-lookup"><span data-stu-id="cdd9e-108">In general, if you are receiving errors importing your Open API document, please ensure you have validated it - either using hello designer in hello new Azure Portal (Design - Front End - Open API Specification Editor), or with a 3rd party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.</span></span>

* <span data-ttu-id="cdd9e-109">**Nazwa hosta** wymagamy atrybutu nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="cdd9e-109">**Host Name** we require a host name attribute.</span></span>
* <span data-ttu-id="cdd9e-110">**Podstawowa ścieżka** wymagamy atrybut ścieżki podstawowej.</span><span class="sxs-lookup"><span data-stu-id="cdd9e-110">**Base Path** we require a base path attribute.</span></span>
* <span data-ttu-id="cdd9e-111">**Schematy** wymagamy tablicy schematu.</span><span class="sxs-lookup"><span data-stu-id="cdd9e-111">**Schemes** we require a scheme array.</span></span> 

## <span data-ttu-id="cdd9e-112"><a name="wsdl"></a>WSDL</span><span class="sxs-lookup"><span data-stu-id="cdd9e-112"><a name="wsdl"> </a>WSDL</span></span>
<span data-ttu-id="cdd9e-113">Pliki WSDL są używane toogenerate interfejsów API przekazywanego SOAP lub służyć jako hello zaplecza interfejsu API SOAP-REST.</span><span class="sxs-lookup"><span data-stu-id="cdd9e-113">WSDL files are used toogenerate SOAP Pass-through APIs, or serve as hello backend of a SOAP-to-REST API.</span></span>

* <span data-ttu-id="cdd9e-114">**WSDL: import** interfejsów API przy użyciu tego atrybutu nie jest obecnie obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="cdd9e-114">**WSDL:Import** we do not currently support APIs using this attribute.</span></span> <span data-ttu-id="cdd9e-115">Klienci, należy scalić hello zaimportowane elementy jeden dokument.</span><span class="sxs-lookup"><span data-stu-id="cdd9e-115">Customers should merge hello imported elements into one document.</span></span>
* <span data-ttu-id="cdd9e-116">**Komunikaty z wielu części** nie są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="cdd9e-116">**Messages with multiple parts** are currently not supported.</span></span>
* <span data-ttu-id="cdd9e-117">**WCF wsHttpBinding** usług SOAP utworzone za pomocą programu Windows Communication Foundation należy użyć klasy basicHttpBinding — wsHttpBinding nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="cdd9e-117">**WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.</span></span>
* <span data-ttu-id="cdd9e-118">**MTOM** usług przy użyciu mechanizmu MTOM <em>może</em> pracy.</span><span class="sxs-lookup"><span data-stu-id="cdd9e-118">**MTOM** Services using MTOM <em>may</em> work.</span></span> <span data-ttu-id="cdd9e-119">W tej chwili nie jest oferowany oficjalnego wsparcia.</span><span class="sxs-lookup"><span data-stu-id="cdd9e-119">Official support is not offered at this time.</span></span>
* <span data-ttu-id="cdd9e-120">**Rekursja** typy, które są zdefiniowane cyklicznie (np. można znaleźć tablicy tooan swojej) nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="cdd9e-120">**Recursion** types that are defined recursively (e.g. refer tooan array of themselves) are not supported.</span></span>

## <span data-ttu-id="cdd9e-121"><a name="wadl"></a>WADL</span><span class="sxs-lookup"><span data-stu-id="cdd9e-121"><a name="wadl"> </a>WADL</span></span>
<span data-ttu-id="cdd9e-122">Obecnie nie istnieją żadne znane problemy importu WADL.</span><span class="sxs-lookup"><span data-stu-id="cdd9e-122">There are no known WADL import issues currently.</span></span>


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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
