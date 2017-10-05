---
title: "Monitorowanie transakcji B2B i skonfigurować rejestrowanie - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Monitor AS2, X 12 i EDIFACT wiadomości, uruchomić rejestrowania diagnostyki dla Twojego konta integracji"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: f717dae9a70a96944b623f22b90cf8c5a943f382
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a><span data-ttu-id="2ce33-103">Monitorowanie i konfigurowanie rejestrowania diagnostyki dla komunikacji B2B w konta integracji</span><span class="sxs-lookup"><span data-stu-id="2ce33-103">Monitor and set up diagnostics logging for B2B communication in integration accounts</span></span>

<span data-ttu-id="2ce33-104">Po skonfigurowaniu B2B komunikacji między dwiema uruchomionych procesów biznesowych lub aplikacji za pośrednictwem konta integracji tych jednostek mogą wymieniać komunikaty ze sobą.</span><span class="sxs-lookup"><span data-stu-id="2ce33-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="2ce33-105">Aby potwierdzić tę komunikację działa zgodnie z oczekiwaniami, można skonfigurować monitorowanie AS2, X12, i EDIFACT komunikaty, wraz z rejestrowania diagnostyki dla Twojego konta integracji za pośrednictwem [Azure Log Analytics](../log-analytics/log-analytics-overview.md) usługi.</span><span class="sxs-lookup"><span data-stu-id="2ce33-105">To confirm this communication works as expected, you can set up monitoring for AS2, X12, and EDIFACT messages, along with diagnostics logging for your integration account through the [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span></span> <span data-ttu-id="2ce33-106">Usługa ta [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitoruje chmurze i lokalnych środowiskach, pomaga zachować ich dostępności i wydajności i zbiera również szczegóły środowiska uruchomieniowego i zdarzeń dla bardziej zaawansowane funkcje debugowania.</span><span class="sxs-lookup"><span data-stu-id="2ce33-106">This service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitors your cloud and on-premises environments, helping you maintain their availability and performance, and also collects runtime details and events for richer debugging.</span></span> <span data-ttu-id="2ce33-107">Możesz również [użyć danych diagnostycznych z innymi usługami](#extend-diagnostic-data), takie jak usługi Azure Storage i Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="2ce33-107">You can also [use your diagnostic data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span>

## <a name="requirements"></a><span data-ttu-id="2ce33-108">Wymagania</span><span class="sxs-lookup"><span data-stu-id="2ce33-108">Requirements</span></span>

* <span data-ttu-id="2ce33-109">Aplikację logiki, który został skonfigurowany z rejestrowania diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="2ce33-109">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="2ce33-110">Dowiedz się [jak skonfigurować rejestrowanie dla danej aplikacji logiki](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="2ce33-110">Learn [how to set up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

  > [!NOTE]
  > <span data-ttu-id="2ce33-111">Po tego wymagania zostały spełnione, powinien mieć obszar roboczy [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ce33-111">After you've met this requirement, you should have a workspace in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="2ce33-112">Po skonfigurowaniu rejestrowania dla Twojego konta integracji, należy używać tego samego obszaru roboczego OMS.</span><span class="sxs-lookup"><span data-stu-id="2ce33-112">You should use the same OMS workspace when you set up logging for your integration account.</span></span> <span data-ttu-id="2ce33-113">Dowiedz się, jeśli nie masz obszar roboczy OMS [jak Utwórz obszar roboczy OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2ce33-113">If you don't have an OMS workspace, learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

* <span data-ttu-id="2ce33-114">Konta integracji połączonego z aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="2ce33-114">An integration account that's linked to your logic app.</span></span> <span data-ttu-id="2ce33-115">Dowiedz się [sposobu tworzenia konta integracji z łączem do aplikacji logiki](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="2ce33-115">Learn [how to create an integration account with a link to your logic app](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a><span data-ttu-id="2ce33-116">Włącz diagnostykę rejestrowania dla Twojego konta integracji</span><span class="sxs-lookup"><span data-stu-id="2ce33-116">Turn on diagnostics logging for your integration account</span></span>

<span data-ttu-id="2ce33-117">Można włączyć rejestrowanie albo bezpośrednio z Twojego konta integracji lub [za pośrednictwem usługi Azure Monitor](#azure-monitor-service).</span><span class="sxs-lookup"><span data-stu-id="2ce33-117">You can turn on logging either directly from your integration account or [through the Azure Monitor service](#azure-monitor-service).</span></span> <span data-ttu-id="2ce33-118">Azure Monitor udostępnia podstawowe monitorowanie za pomocą danych na poziomie infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="2ce33-118">Azure Monitor provides basic monitoring with infrastructure-level data.</span></span> <span data-ttu-id="2ce33-119">Dowiedz się więcej o [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="2ce33-119">Learn more about [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span>

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a><span data-ttu-id="2ce33-120">Włącz diagnostykę, rejestrowanie bezpośrednio z Twojego konta integracji</span><span class="sxs-lookup"><span data-stu-id="2ce33-120">Turn on diagnostics logging directly from your integration account</span></span>

1. <span data-ttu-id="2ce33-121">W [portalu Azure](https://portal.azure.com), Znajdź i wybierz konto integracji.</span><span class="sxs-lookup"><span data-stu-id="2ce33-121">In the [Azure portal](https://portal.azure.com), find and select your integration account.</span></span> <span data-ttu-id="2ce33-122">W obszarze **monitorowanie**, wybierz **dzienników diagnostycznych** w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="2ce33-122">Under **Monitoring**, choose **Diagnostics logs** as shown here:</span></span>

   ![Znajdź i wybierz konto integracji, wybierz polecenie "Dzienniki diagnostyczne"](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. <span data-ttu-id="2ce33-124">Po wybraniu konta integracji następujące wartości zostaną zaznaczone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="2ce33-124">After you select your integration account, the following values are automatically selected.</span></span> <span data-ttu-id="2ce33-125">Jeśli te wartości są prawidłowe, wybierz **Włącz diagnostykę**.</span><span class="sxs-lookup"><span data-stu-id="2ce33-125">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="2ce33-126">W przeciwnym razie wybierz wartości, które mają:</span><span class="sxs-lookup"><span data-stu-id="2ce33-126">Otherwise, select the values that you want:</span></span>

   1. <span data-ttu-id="2ce33-127">W obszarze **subskrypcji**, wybierz subskrypcję platformy Azure korzystające z Twoim kontem integracji.</span><span class="sxs-lookup"><span data-stu-id="2ce33-127">Under **Subscription**, select the Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="2ce33-128">W obszarze **grupy zasobów**, wybierz grupę zasobów, korzystających z Twoim kontem integracji.</span><span class="sxs-lookup"><span data-stu-id="2ce33-128">Under **Resource group**, select the resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="2ce33-129">W obszarze **typu zasobu**, wybierz pozycję **konta integracji**.</span><span class="sxs-lookup"><span data-stu-id="2ce33-129">Under **Resource type**, select **Integration accounts**.</span></span> 
   4. <span data-ttu-id="2ce33-130">W obszarze **zasobów**, wybierz konto integracji.</span><span class="sxs-lookup"><span data-stu-id="2ce33-130">Under **Resource**, select your integration account.</span></span> 
   5. <span data-ttu-id="2ce33-131">Wybierz **Włącz diagnostykę**.</span><span class="sxs-lookup"><span data-stu-id="2ce33-131">Choose **Turn on diagnostics**.</span></span>

   ![Ustawienia diagnostyki dla Twojego konta integracji](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="2ce33-133">W obszarze **ustawień diagnostycznych**, a następnie **stan**, wybierz **na**.</span><span class="sxs-lookup"><span data-stu-id="2ce33-133">Under **Diagnostics settings**, and then **Status**, choose **On**.</span></span>

   ![Włącz diagnostykę Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="2ce33-135">Teraz wybierz obszar roboczy OMS i dane do użycia podczas rejestrowania, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="2ce33-135">Now select the OMS workspace and data to use for logging as shown:</span></span>

   1. <span data-ttu-id="2ce33-136">Wybierz **wysyłać do analizy dzienników**.</span><span class="sxs-lookup"><span data-stu-id="2ce33-136">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="2ce33-137">W obszarze **analizy dzienników**, wybierz **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="2ce33-137">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="2ce33-138">W obszarze **obszarów roboczych OMS**, wybierz obszar roboczy OMS na potrzeby rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="2ce33-138">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="2ce33-139">W obszarze **dziennika**, wybierz pozycję **IntegrationAccountTrackingEvents** kategorii.</span><span class="sxs-lookup"><span data-stu-id="2ce33-139">Under **Log**, select the **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="2ce33-140">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="2ce33-140">Choose **Save**.</span></span>

   ![Konfigurowanie analizy dzienników, aby wysłać dane diagnostyczne dziennika](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="2ce33-142">Teraz [skonfigurować śledzenie wiadomości B2B w OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="2ce33-142">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a><span data-ttu-id="2ce33-143">Włącz rejestrowanie danych diagnostycznych za pośrednictwem Monitora Azure</span><span class="sxs-lookup"><span data-stu-id="2ce33-143">Turn on diagnostics logging through Azure Monitor</span></span>

1. <span data-ttu-id="2ce33-144">W [portalu Azure](https://portal.azure.com), w menu głównym Azure wybierz **Monitor**, **dzienników diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="2ce33-144">In the [Azure portal](https://portal.azure.com), on the main Azure menu, choose **Monitor**, **Diagnostics logs**.</span></span> <span data-ttu-id="2ce33-145">Następnie wybierz konta integracji, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="2ce33-145">Then select your integration account as shown here:</span></span>

   ![Wybierz pozycję "Monitoruj", "Dzienniki diagnostyczne", wybierz konto integracji](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. <span data-ttu-id="2ce33-147">Po wybraniu konta integracji następujące wartości zostaną zaznaczone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="2ce33-147">After you select your integration account, the following values are automatically selected.</span></span> <span data-ttu-id="2ce33-148">Jeśli te wartości są prawidłowe, wybierz **Włącz diagnostykę**.</span><span class="sxs-lookup"><span data-stu-id="2ce33-148">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="2ce33-149">W przeciwnym razie wybierz wartości, które mają:</span><span class="sxs-lookup"><span data-stu-id="2ce33-149">Otherwise, select the values that you want:</span></span>

   1. <span data-ttu-id="2ce33-150">W obszarze **subskrypcji**, wybierz subskrypcję platformy Azure korzystające z Twoim kontem integracji.</span><span class="sxs-lookup"><span data-stu-id="2ce33-150">Under **Subscription**, select the Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="2ce33-151">W obszarze **grupy zasobów**, wybierz grupę zasobów, korzystających z Twoim kontem integracji.</span><span class="sxs-lookup"><span data-stu-id="2ce33-151">Under **Resource group**, select the resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="2ce33-152">W obszarze **typu zasobu**, wybierz pozycję **konta integracji**.</span><span class="sxs-lookup"><span data-stu-id="2ce33-152">Under **Resource type**, select **Integration accounts**.</span></span>
   4. <span data-ttu-id="2ce33-153">W obszarze **zasobów**, wybierz konto integracji.</span><span class="sxs-lookup"><span data-stu-id="2ce33-153">Under **Resource**, select your integration account.</span></span>
   5. <span data-ttu-id="2ce33-154">Wybierz **Włącz diagnostykę**.</span><span class="sxs-lookup"><span data-stu-id="2ce33-154">Choose **Turn on diagnostics**.</span></span>

   ![Ustawienia diagnostyki dla Twojego konta integracji](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="2ce33-156">W obszarze **ustawień diagnostycznych**, wybierz **na**.</span><span class="sxs-lookup"><span data-stu-id="2ce33-156">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Włącz diagnostykę Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="2ce33-158">Teraz wybierz OMS kategorii obszaru roboczego i zdarzenia logowania, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="2ce33-158">Now select the OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="2ce33-159">Wybierz **wysyłać do analizy dzienników**.</span><span class="sxs-lookup"><span data-stu-id="2ce33-159">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="2ce33-160">W obszarze **analizy dzienników**, wybierz **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="2ce33-160">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="2ce33-161">W obszarze **obszarów roboczych OMS**, wybierz obszar roboczy OMS na potrzeby rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="2ce33-161">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="2ce33-162">W obszarze **dziennika**, wybierz pozycję **IntegrationAccountTrackingEvents** kategorii.</span><span class="sxs-lookup"><span data-stu-id="2ce33-162">Under **Log**, select the **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="2ce33-163">Gdy wszystko będzie gotowe, wybierz pozycję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="2ce33-163">When you're done, choose **Save**.</span></span>

   ![Konfigurowanie analizy dzienników, aby wysłać dane diagnostyczne dziennika](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="2ce33-165">Teraz [skonfigurować śledzenie wiadomości B2B w OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="2ce33-165">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="2ce33-166">Rozszerzanie, jak i gdzie używać danych diagnostycznych z innymi usługami</span><span class="sxs-lookup"><span data-stu-id="2ce33-166">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="2ce33-167">Wraz z Azure Log Analytics można rozszerzyć, jak używasz aplikacji logiki danych diagnostycznych z innymi usługami Azure, na przykład:</span><span class="sxs-lookup"><span data-stu-id="2ce33-167">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="2ce33-168">Archiwum, które dzienniki diagnostyczne platformy Azure w magazynie Azure</span><span class="sxs-lookup"><span data-stu-id="2ce33-168">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="2ce33-169">Strumieniowe przesyłanie dzienników diagnostycznych platformy Azure do usługi Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="2ce33-169">Stream Azure Diagnostics Logs to Azure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="2ce33-170">Następnie monitorowanie za pomocą telemetrii i analiza z innych usług, takich jak get w czasie rzeczywistym [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) i [usługi Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="2ce33-170">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="2ce33-171">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="2ce33-171">For example:</span></span>

* [<span data-ttu-id="2ce33-172">Strumień danych z usługi Event Hubs Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2ce33-172">Stream data from Event Hubs to Stream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="2ce33-173">Analizować dane przesyłane strumieniowo z usługi Stream Analytics i utworzyć pulpit nawigacyjny analiz w czasie rzeczywistym w usłudze Power BI</span><span class="sxs-lookup"><span data-stu-id="2ce33-173">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="2ce33-174">Oparte na opcje, które chcesz skonfigurować, upewnij się, że możesz pierwszy [utworzyć konto magazynu Azure](../storage/common/storage-create-storage-account.md) lub [tworzenia Centrum zdarzeń Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="2ce33-174">Based on the options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="2ce33-175">Następnie wybierz opcje dla których chcesz wysyłać dane diagnostyczne:</span><span class="sxs-lookup"><span data-stu-id="2ce33-175">Then select the options for where you want to send diagnostic data:</span></span>

![Wysyłanie danych do magazynu Azure konta lub zdarzenia koncentratora.](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="2ce33-177">Okresy przechowywania mają zastosowanie tylko wtedy, gdy chcesz użyć konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ce33-177">Retention periods apply only when you choose to use a storage account.</span></span>

## <a name="supported-tracking-schemas"></a><span data-ttu-id="2ce33-178">Obsługiwane schematy śledzenia</span><span class="sxs-lookup"><span data-stu-id="2ce33-178">Supported tracking schemas</span></span>

<span data-ttu-id="2ce33-179">Azure obsługuje te śledzenia typów schematów, które ustalone schematów z wyjątkiem typu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="2ce33-179">Azure supports these tracking schema types, which all have fixed schemas except the Custom type.</span></span>

* [<span data-ttu-id="2ce33-180">Schemat śledzenia AS2</span><span class="sxs-lookup"><span data-stu-id="2ce33-180">AS2 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="2ce33-181">Schemat śledzenia X12</span><span class="sxs-lookup"><span data-stu-id="2ce33-181">X12 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="2ce33-182">Niestandardowe schematy śledzenia</span><span class="sxs-lookup"><span data-stu-id="2ce33-182">Custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="2ce33-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2ce33-183">Next steps</span></span>

* [<span data-ttu-id="2ce33-184">Śledzenie wiadomości B2B w OMS</span><span class="sxs-lookup"><span data-stu-id="2ce33-184">Track B2B messages in OMS</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "wiadomości B2B śledzenie w OMS")
* [<span data-ttu-id="2ce33-185">Dowiedz się więcej o pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="2ce33-185">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw")

