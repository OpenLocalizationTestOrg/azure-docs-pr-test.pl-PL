---
title: "Śledzenie niestandardowych schematów B2B monitorowania - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Utwórz schematy śledzenia niestandardowych do monitorowania wiadomości B2B transakcji na koncie Azure integracji."
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
ms.openlocfilehash: b71a4938dde2a71f1ce29403af7aa9101358d64c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-tracking-to-monitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="466b1-103">Włącz śledzenie w celu monitorowania ukończenia przepływu pracy, end-to-end</span><span class="sxs-lookup"><span data-stu-id="466b1-103">Enable tracking to monitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="466b1-104">Są wbudowane, śledzenie, możesz włączyć dla różnych części przepływu pracy business-to-business, takie jak śledzenie AS2 lub X12 wiadomości.</span><span class="sxs-lookup"><span data-stu-id="466b1-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="466b1-105">Podczas tworzenia przepływów pracy zawiera aplikację logiki, BizTalk Server, SQL Server lub inną warstwę, można włączyć śledzenie niestandardowej, która zapisuje zdarzenia od początku do końca przepływu pracy, a następnie.</span><span class="sxs-lookup"><span data-stu-id="466b1-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from the beginning to the end of your workflow.</span></span> 

<span data-ttu-id="466b1-106">Ten temat zawiera kod niestandardowy, który można użyć w warstwach poza aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="466b1-106">This topic provides custom code that you can use in the layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="466b1-107">Schemat niestandardowy śledzenia</span><span class="sxs-lookup"><span data-stu-id="466b1-107">Custom tracking schema</span></span>
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

| <span data-ttu-id="466b1-108">Właściwość</span><span class="sxs-lookup"><span data-stu-id="466b1-108">Property</span></span> | <span data-ttu-id="466b1-109">Typ</span><span class="sxs-lookup"><span data-stu-id="466b1-109">Type</span></span> | <span data-ttu-id="466b1-110">Opis</span><span class="sxs-lookup"><span data-stu-id="466b1-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="466b1-111">Źródłowa</span><span class="sxs-lookup"><span data-stu-id="466b1-111">sourceType</span></span> |   | <span data-ttu-id="466b1-112">Typ działania źródłowego.</span><span class="sxs-lookup"><span data-stu-id="466b1-112">Type of the run source.</span></span> <span data-ttu-id="466b1-113">Dozwolone wartości to **Microsoft.Logic/workflows** i **niestandardowych**.</span><span class="sxs-lookup"><span data-stu-id="466b1-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="466b1-114">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="466b1-114">(Mandatory)</span></span> |
| <span data-ttu-id="466b1-115">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="466b1-115">Source</span></span> |   | <span data-ttu-id="466b1-116">Jeśli typ źródła jest **Microsoft.Logic/workflows**, informacje o źródle musi wykonać tego schematu.</span><span class="sxs-lookup"><span data-stu-id="466b1-116">If the source type is **Microsoft.Logic/workflows**, the source information needs to follow this schema.</span></span> <span data-ttu-id="466b1-117">Jeśli typ źródła jest **niestandardowe**, schemat jest JToken.</span><span class="sxs-lookup"><span data-stu-id="466b1-117">If the source type is **custom**, the schema is a JToken.</span></span> <span data-ttu-id="466b1-118">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="466b1-118">(Mandatory)</span></span> |
| <span data-ttu-id="466b1-119">systemId</span><span class="sxs-lookup"><span data-stu-id="466b1-119">systemId</span></span> | <span data-ttu-id="466b1-120">Ciąg</span><span class="sxs-lookup"><span data-stu-id="466b1-120">String</span></span> | <span data-ttu-id="466b1-121">Identyfikator logiki aplikacji systemu.</span><span class="sxs-lookup"><span data-stu-id="466b1-121">Logic app system ID.</span></span> <span data-ttu-id="466b1-122">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="466b1-122">(Mandatory)</span></span> |
| <span data-ttu-id="466b1-123">przebiegu</span><span class="sxs-lookup"><span data-stu-id="466b1-123">runId</span></span> | <span data-ttu-id="466b1-124">Ciąg</span><span class="sxs-lookup"><span data-stu-id="466b1-124">String</span></span> | <span data-ttu-id="466b1-125">Uruchom identyfikatora aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="466b1-125">Logic app run ID.</span></span> <span data-ttu-id="466b1-126">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="466b1-126">(Mandatory)</span></span> |
| <span data-ttu-id="466b1-127">operationName</span><span class="sxs-lookup"><span data-stu-id="466b1-127">operationName</span></span> | <span data-ttu-id="466b1-128">Ciąg</span><span class="sxs-lookup"><span data-stu-id="466b1-128">String</span></span> | <span data-ttu-id="466b1-129">Nazwa operacji (na przykład, akcji lub wyzwalacz).</span><span class="sxs-lookup"><span data-stu-id="466b1-129">Name of the operation (for example, action or trigger).</span></span> <span data-ttu-id="466b1-130">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="466b1-130">(Mandatory)</span></span> |
| <span data-ttu-id="466b1-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="466b1-131">repeatItemScopeName</span></span> | <span data-ttu-id="466b1-132">Ciąg</span><span class="sxs-lookup"><span data-stu-id="466b1-132">String</span></span> | <span data-ttu-id="466b1-133">Powtórz nazwy elementu, jeśli akcja jest wewnątrz `foreach` / `until` pętli.</span><span class="sxs-lookup"><span data-stu-id="466b1-133">Repeat item name if the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="466b1-134">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="466b1-134">(Mandatory)</span></span> |
| <span data-ttu-id="466b1-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="466b1-135">repeatItemIndex</span></span> | <span data-ttu-id="466b1-136">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="466b1-136">Integer</span></span> | <span data-ttu-id="466b1-137">Czy akcja jest wewnątrz `foreach` / `until` pętli.</span><span class="sxs-lookup"><span data-stu-id="466b1-137">Whether the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="466b1-138">Wskazuje indeks elementu powtarzanego.</span><span class="sxs-lookup"><span data-stu-id="466b1-138">Indicates the repeated item index.</span></span> <span data-ttu-id="466b1-139">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="466b1-139">(Mandatory)</span></span> |
| <span data-ttu-id="466b1-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="466b1-140">trackingId</span></span> | <span data-ttu-id="466b1-141">Ciąg</span><span class="sxs-lookup"><span data-stu-id="466b1-141">String</span></span> | <span data-ttu-id="466b1-142">Identyfikator, aby skorelować komunikaty śledzenia.</span><span class="sxs-lookup"><span data-stu-id="466b1-142">Tracking ID, to correlate the messages.</span></span> <span data-ttu-id="466b1-143">(Opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="466b1-143">(Optional)</span></span> |
| <span data-ttu-id="466b1-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="466b1-144">correlationId</span></span> | <span data-ttu-id="466b1-145">Ciąg</span><span class="sxs-lookup"><span data-stu-id="466b1-145">String</span></span> | <span data-ttu-id="466b1-146">Identyfikator korelacji służące do skorelowania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="466b1-146">Correlation ID, to correlate the messages.</span></span> <span data-ttu-id="466b1-147">(Opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="466b1-147">(Optional)</span></span> |
| <span data-ttu-id="466b1-148">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="466b1-148">clientRequestId</span></span> | <span data-ttu-id="466b1-149">Ciąg</span><span class="sxs-lookup"><span data-stu-id="466b1-149">String</span></span> | <span data-ttu-id="466b1-150">Klienta można umieścić w nim służące do skorelowania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="466b1-150">Client can populate it to correlate messages.</span></span> <span data-ttu-id="466b1-151">(Opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="466b1-151">(Optional)</span></span> |
| <span data-ttu-id="466b1-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="466b1-152">eventLevel</span></span> |   | <span data-ttu-id="466b1-153">Poziom zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="466b1-153">Level of the event.</span></span> <span data-ttu-id="466b1-154">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="466b1-154">(Mandatory)</span></span> |
| <span data-ttu-id="466b1-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="466b1-155">eventTime</span></span> |   | <span data-ttu-id="466b1-156">Godzina zdarzenia w formacie UTC RRRR-MM-DDTHH:MM:SS.00000Z.</span><span class="sxs-lookup"><span data-stu-id="466b1-156">Time of the event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="466b1-157">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="466b1-157">(Mandatory)</span></span> |
| <span data-ttu-id="466b1-158">recordType</span><span class="sxs-lookup"><span data-stu-id="466b1-158">recordType</span></span> |   | <span data-ttu-id="466b1-159">Typ rekordu śledzenia.</span><span class="sxs-lookup"><span data-stu-id="466b1-159">Type of the track record.</span></span> <span data-ttu-id="466b1-160">Dozwolone wartości to **niestandardowych**.</span><span class="sxs-lookup"><span data-stu-id="466b1-160">Allowed value is **custom**.</span></span> <span data-ttu-id="466b1-161">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="466b1-161">(Mandatory)</span></span> |
| <span data-ttu-id="466b1-162">rekord</span><span class="sxs-lookup"><span data-stu-id="466b1-162">record</span></span> |   | <span data-ttu-id="466b1-163">Typ niestandardowy rekord.</span><span class="sxs-lookup"><span data-stu-id="466b1-163">Custom record type.</span></span> <span data-ttu-id="466b1-164">Dozwolony format to JToken.</span><span class="sxs-lookup"><span data-stu-id="466b1-164">Allowed format is JToken.</span></span> <span data-ttu-id="466b1-165">(Wymagane)</span><span class="sxs-lookup"><span data-stu-id="466b1-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="466b1-166">Schematy śledzenia protokołu B2B</span><span class="sxs-lookup"><span data-stu-id="466b1-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="466b1-167">Aby uzyskać informacji na temat protokołu B2B śledzenia schematów zobacz:</span><span class="sxs-lookup"><span data-stu-id="466b1-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="466b1-168">Schematy śledzenia AS2</span><span class="sxs-lookup"><span data-stu-id="466b1-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="466b1-169">Schematy śledzenia X12</span><span class="sxs-lookup"><span data-stu-id="466b1-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="466b1-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="466b1-170">Next steps</span></span>
* <span data-ttu-id="466b1-171">Dowiedz się więcej o [monitorowanie wiadomości B2B](logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="466b1-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="466b1-172">Dowiedz się więcej o [śledzenie wiadomości B2B w portalu usługi Operations Management Suite](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="466b1-172">Learn about [tracking B2B messages in the Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="466b1-173">Dowiedz się więcej o [pakiet integracyjny dla przedsiębiorstw](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="466b1-173">Learn more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
