---
title: "Śledzenie schematy B2B aaaCustom monitorowania - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Utwórz schematy śledzenia niestandardowych toomonitor B2B wiadomości transakcji na koncie integracji Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="0d450-103">Włącz śledzenie toomonitor ukończenia przepływu pracy, end-to-end</span><span class="sxs-lookup"><span data-stu-id="0d450-103">Enable tracking toomonitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="0d450-104">Są wbudowane, śledzenie, możesz włączyć dla różnych części przepływu pracy business-to-business, takie jak śledzenie AS2 lub X12 wiadomości.</span><span class="sxs-lookup"><span data-stu-id="0d450-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="0d450-105">Podczas tworzenia przepływów pracy, które zawiera aplikację logiki, BizTalk Server, SQL Server lub inną warstwę, można włączyć śledzenie niestandardowej, która zapisuje zdarzenia z hello początek toohello koniec przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="0d450-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from hello beginning toohello end of your workflow.</span></span> 

<span data-ttu-id="0d450-106">Ten temat zawiera kod niestandardowy, który można użyć w warstwach hello poza aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="0d450-106">This topic provides custom code that you can use in hello layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="0d450-107">Schemat niestandardowy śledzenia</span><span class="sxs-lookup"><span data-stu-id="0d450-107">Custom tracking schema</span></span>
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| <span data-ttu-id="0d450-108">Właściwość</span><span class="sxs-lookup"><span data-stu-id="0d450-108">Property</span></span> | <span data-ttu-id="0d450-109">Typ</span><span class="sxs-lookup"><span data-stu-id="0d450-109">Type</span></span> | <span data-ttu-id="0d450-110">Opis</span><span class="sxs-lookup"><span data-stu-id="0d450-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d450-111">Źródłowa</span><span class="sxs-lookup"><span data-stu-id="0d450-111">sourceType</span></span> |   | <span data-ttu-id="0d450-112">Typ źródła hello Uruchom.</span><span class="sxs-lookup"><span data-stu-id="0d450-112">Type of hello run source.</span></span> <span data-ttu-id="0d450-113">Dozwolone wartości to **Microsoft.Logic/workflows** i **niestandardowych**.</span><span class="sxs-lookup"><span data-stu-id="0d450-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="0d450-114">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="0d450-114">(Mandatory)</span></span> |
| <span data-ttu-id="0d450-115">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="0d450-115">Source</span></span> |   | <span data-ttu-id="0d450-116">Jeśli typ źródła hello jest **Microsoft.Logic/workflows**, informacje o źródle hello musi toofollow tego schematu.</span><span class="sxs-lookup"><span data-stu-id="0d450-116">If hello source type is **Microsoft.Logic/workflows**, hello source information needs toofollow this schema.</span></span> <span data-ttu-id="0d450-117">Jeśli typ źródła hello jest **niestandardowe**, schemat hello jest JToken.</span><span class="sxs-lookup"><span data-stu-id="0d450-117">If hello source type is **custom**, hello schema is a JToken.</span></span> <span data-ttu-id="0d450-118">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="0d450-118">(Mandatory)</span></span> |
| <span data-ttu-id="0d450-119">systemId</span><span class="sxs-lookup"><span data-stu-id="0d450-119">systemId</span></span> | <span data-ttu-id="0d450-120">Ciąg</span><span class="sxs-lookup"><span data-stu-id="0d450-120">String</span></span> | <span data-ttu-id="0d450-121">Identyfikator logiki aplikacji systemu.</span><span class="sxs-lookup"><span data-stu-id="0d450-121">Logic app system ID.</span></span> <span data-ttu-id="0d450-122">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="0d450-122">(Mandatory)</span></span> |
| <span data-ttu-id="0d450-123">przebiegu</span><span class="sxs-lookup"><span data-stu-id="0d450-123">runId</span></span> | <span data-ttu-id="0d450-124">Ciąg</span><span class="sxs-lookup"><span data-stu-id="0d450-124">String</span></span> | <span data-ttu-id="0d450-125">Uruchom identyfikatora aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="0d450-125">Logic app run ID.</span></span> <span data-ttu-id="0d450-126">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="0d450-126">(Mandatory)</span></span> |
| <span data-ttu-id="0d450-127">operationName</span><span class="sxs-lookup"><span data-stu-id="0d450-127">operationName</span></span> | <span data-ttu-id="0d450-128">Ciąg</span><span class="sxs-lookup"><span data-stu-id="0d450-128">String</span></span> | <span data-ttu-id="0d450-129">Nazwa operacji hello (na przykład, akcji lub wyzwalacz).</span><span class="sxs-lookup"><span data-stu-id="0d450-129">Name of hello operation (for example, action or trigger).</span></span> <span data-ttu-id="0d450-130">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="0d450-130">(Mandatory)</span></span> |
| <span data-ttu-id="0d450-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="0d450-131">repeatItemScopeName</span></span> | <span data-ttu-id="0d450-132">Ciąg</span><span class="sxs-lookup"><span data-stu-id="0d450-132">String</span></span> | <span data-ttu-id="0d450-133">Powtórz nazwa elementu, jeśli akcja hello znajduje się wewnątrz `foreach` / `until` pętli.</span><span class="sxs-lookup"><span data-stu-id="0d450-133">Repeat item name if hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="0d450-134">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="0d450-134">(Mandatory)</span></span> |
| <span data-ttu-id="0d450-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="0d450-135">repeatItemIndex</span></span> | <span data-ttu-id="0d450-136">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="0d450-136">Integer</span></span> | <span data-ttu-id="0d450-137">Czy hello akcji znajduje się wewnątrz `foreach` / `until` pętli.</span><span class="sxs-lookup"><span data-stu-id="0d450-137">Whether hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="0d450-138">Wskazuje indeks elementu powtarzanego hello.</span><span class="sxs-lookup"><span data-stu-id="0d450-138">Indicates hello repeated item index.</span></span> <span data-ttu-id="0d450-139">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="0d450-139">(Mandatory)</span></span> |
| <span data-ttu-id="0d450-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="0d450-140">trackingId</span></span> | <span data-ttu-id="0d450-141">Ciąg</span><span class="sxs-lookup"><span data-stu-id="0d450-141">String</span></span> | <span data-ttu-id="0d450-142">Identyfikator śledzenia wiadomości powitania toocorrelate.</span><span class="sxs-lookup"><span data-stu-id="0d450-142">Tracking ID, toocorrelate hello messages.</span></span> <span data-ttu-id="0d450-143">(Opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="0d450-143">(Optional)</span></span> |
| <span data-ttu-id="0d450-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="0d450-144">correlationId</span></span> | <span data-ttu-id="0d450-145">Ciąg</span><span class="sxs-lookup"><span data-stu-id="0d450-145">String</span></span> | <span data-ttu-id="0d450-146">Identyfikator korelacji wiadomości powitania toocorrelate.</span><span class="sxs-lookup"><span data-stu-id="0d450-146">Correlation ID, toocorrelate hello messages.</span></span> <span data-ttu-id="0d450-147">(Opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="0d450-147">(Optional)</span></span> |
| <span data-ttu-id="0d450-148">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="0d450-148">clientRequestId</span></span> | <span data-ttu-id="0d450-149">Ciąg</span><span class="sxs-lookup"><span data-stu-id="0d450-149">String</span></span> | <span data-ttu-id="0d450-150">Klienta można umieścić w nim toocorrelate wiadomości.</span><span class="sxs-lookup"><span data-stu-id="0d450-150">Client can populate it toocorrelate messages.</span></span> <span data-ttu-id="0d450-151">(Opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="0d450-151">(Optional)</span></span> |
| <span data-ttu-id="0d450-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="0d450-152">eventLevel</span></span> |   | <span data-ttu-id="0d450-153">Poziom hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="0d450-153">Level of hello event.</span></span> <span data-ttu-id="0d450-154">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="0d450-154">(Mandatory)</span></span> |
| <span data-ttu-id="0d450-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="0d450-155">eventTime</span></span> |   | <span data-ttu-id="0d450-156">Godzina zdarzenia hello w formacie UTC RRRR-MM-DDTHH:MM:SS.00000Z.</span><span class="sxs-lookup"><span data-stu-id="0d450-156">Time of hello event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="0d450-157">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="0d450-157">(Mandatory)</span></span> |
| <span data-ttu-id="0d450-158">recordType</span><span class="sxs-lookup"><span data-stu-id="0d450-158">recordType</span></span> |   | <span data-ttu-id="0d450-159">Typ hello ścieżki.</span><span class="sxs-lookup"><span data-stu-id="0d450-159">Type of hello track record.</span></span> <span data-ttu-id="0d450-160">Dozwolone wartości to **niestandardowych**.</span><span class="sxs-lookup"><span data-stu-id="0d450-160">Allowed value is **custom**.</span></span> <span data-ttu-id="0d450-161">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="0d450-161">(Mandatory)</span></span> |
| <span data-ttu-id="0d450-162">rekord</span><span class="sxs-lookup"><span data-stu-id="0d450-162">record</span></span> |   | <span data-ttu-id="0d450-163">Typ niestandardowy rekord.</span><span class="sxs-lookup"><span data-stu-id="0d450-163">Custom record type.</span></span> <span data-ttu-id="0d450-164">Dozwolony format to JToken.</span><span class="sxs-lookup"><span data-stu-id="0d450-164">Allowed format is JToken.</span></span> <span data-ttu-id="0d450-165">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="0d450-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="0d450-166">Schematy śledzenia protokołu B2B</span><span class="sxs-lookup"><span data-stu-id="0d450-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="0d450-167">Aby uzyskać informacji na temat protokołu B2B śledzenia schematów zobacz:</span><span class="sxs-lookup"><span data-stu-id="0d450-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="0d450-168">Schematy śledzenia AS2</span><span class="sxs-lookup"><span data-stu-id="0d450-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="0d450-169">Schematy śledzenia X12</span><span class="sxs-lookup"><span data-stu-id="0d450-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="0d450-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0d450-170">Next steps</span></span>
* <span data-ttu-id="0d450-171">Dowiedz się więcej o [monitorowanie wiadomości B2B](logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="0d450-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="0d450-172">Dowiedz się więcej o [śledzenie wiadomości B2B w portalu usługi Operations Management Suite hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="0d450-172">Learn about [tracking B2B messages in hello Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="0d450-173">Dowiedz się więcej o hello [pakiet integracyjny dla przedsiębiorstw](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0d450-173">Learn more about hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
