---
title: "Transakcje aaaMonitor B2B i skonfigurować rejestrowanie - Azure Logic Apps | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: a6745ebf41aab331020bfec072f5806711d125bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a><span data-ttu-id="194a4-103">Monitorowanie i konfigurowanie rejestrowania diagnostyki dla komunikacji B2B w konta integracji</span><span class="sxs-lookup"><span data-stu-id="194a4-103">Monitor and set up diagnostics logging for B2B communication in integration accounts</span></span>

<span data-ttu-id="194a4-104">Po skonfigurowaniu B2B komunikacji między dwiema uruchomionych procesów biznesowych lub aplikacji za pośrednictwem konta integracji tych jednostek mogą wymieniać komunikaty ze sobą.</span><span class="sxs-lookup"><span data-stu-id="194a4-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="194a4-105">tooconfirm tej komunikacji działa zgodnie z oczekiwaniami, można skonfigurować monitorowanie AS2, X12, i EDIFACT komunikaty, wraz z rejestrowania diagnostyki dla Twojego konta integracji za pośrednictwem hello [Azure Log Analytics](../log-analytics/log-analytics-overview.md) usługi.</span><span class="sxs-lookup"><span data-stu-id="194a4-105">tooconfirm this communication works as expected, you can set up monitoring for AS2, X12, and EDIFACT messages, along with diagnostics logging for your integration account through hello [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span></span> <span data-ttu-id="194a4-106">Usługa ta [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitoruje chmurze i lokalnych środowiskach, pomaga zachować ich dostępności i wydajności i zbiera również szczegóły środowiska uruchomieniowego i zdarzeń dla bardziej zaawansowane funkcje debugowania.</span><span class="sxs-lookup"><span data-stu-id="194a4-106">This service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitors your cloud and on-premises environments, helping you maintain their availability and performance, and also collects runtime details and events for richer debugging.</span></span> <span data-ttu-id="194a4-107">Możesz również [użyć danych diagnostycznych z innymi usługami](#extend-diagnostic-data), takie jak usługi Azure Storage i Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="194a4-107">You can also [use your diagnostic data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span>

## <a name="requirements"></a><span data-ttu-id="194a4-108">Wymagania</span><span class="sxs-lookup"><span data-stu-id="194a4-108">Requirements</span></span>

* <span data-ttu-id="194a4-109">Aplikację logiki, który został skonfigurowany z rejestrowania diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="194a4-109">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="194a4-110">Dowiedz się [jak tooset rejestrowanie dla danej aplikacji logiki danych](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="194a4-110">Learn [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

  > [!NOTE]
  > <span data-ttu-id="194a4-111">Po tego wymagania zostały spełnione, powinien mieć obszar roboczy w hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="194a4-111">After you've met this requirement, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="194a4-112">Należy używać hello sam obszar roboczy OMS po skonfigurowaniu rejestrowania dla Twojego konta integracji.</span><span class="sxs-lookup"><span data-stu-id="194a4-112">You should use hello same OMS workspace when you set up logging for your integration account.</span></span> <span data-ttu-id="194a4-113">Dowiedz się, jeśli nie masz obszar roboczy OMS [jak toocreate obszarem roboczym pakietu OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="194a4-113">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

* <span data-ttu-id="194a4-114">Konta integracji, które zawiera połączone tooyour aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="194a4-114">An integration account that's linked tooyour logic app.</span></span> <span data-ttu-id="194a4-115">Dowiedz się [jak konto toocreate integracji z aplikacji logiki tooyour łącze](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="194a4-115">Learn [how toocreate an integration account with a link tooyour logic app](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a><span data-ttu-id="194a4-116">Włącz diagnostykę rejestrowania dla Twojego konta integracji</span><span class="sxs-lookup"><span data-stu-id="194a4-116">Turn on diagnostics logging for your integration account</span></span>

<span data-ttu-id="194a4-117">Można włączyć rejestrowanie albo bezpośrednio z Twojego konta integracji lub [za pośrednictwem hello Azure monitorowania usługi](#azure-monitor-service).</span><span class="sxs-lookup"><span data-stu-id="194a4-117">You can turn on logging either directly from your integration account or [through hello Azure Monitor service](#azure-monitor-service).</span></span> <span data-ttu-id="194a4-118">Azure Monitor udostępnia podstawowe monitorowanie za pomocą danych na poziomie infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="194a4-118">Azure Monitor provides basic monitoring with infrastructure-level data.</span></span> <span data-ttu-id="194a4-119">Dowiedz się więcej o [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="194a4-119">Learn more about [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span>

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a><span data-ttu-id="194a4-120">Włącz diagnostykę, rejestrowanie bezpośrednio z Twojego konta integracji</span><span class="sxs-lookup"><span data-stu-id="194a4-120">Turn on diagnostics logging directly from your integration account</span></span>

1. <span data-ttu-id="194a4-121">W hello [portalu Azure](https://portal.azure.com), Znajdź i wybierz konto integracji.</span><span class="sxs-lookup"><span data-stu-id="194a4-121">In hello [Azure portal](https://portal.azure.com), find and select your integration account.</span></span> <span data-ttu-id="194a4-122">W obszarze **monitorowanie**, wybierz **dzienników diagnostycznych** w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="194a4-122">Under **Monitoring**, choose **Diagnostics logs** as shown here:</span></span>

   ![Znajdź i wybierz konto integracji, wybierz polecenie "Dzienniki diagnostyczne"](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. <span data-ttu-id="194a4-124">Po wybraniu konta integracji hello następujące wartości zostaną zaznaczone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="194a4-124">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="194a4-125">Jeśli te wartości są prawidłowe, wybierz **Włącz diagnostykę**.</span><span class="sxs-lookup"><span data-stu-id="194a4-125">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="194a4-126">W przeciwnym razie wybierz hello wartości, które mają:</span><span class="sxs-lookup"><span data-stu-id="194a4-126">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="194a4-127">W obszarze **subskrypcji**, wybierz hello subskrypcji platformy Azure korzystające z Twoim kontem integracji.</span><span class="sxs-lookup"><span data-stu-id="194a4-127">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="194a4-128">W obszarze **grupy zasobów**, wybierz grupę zasobów hello używanej z Twoim kontem integracji.</span><span class="sxs-lookup"><span data-stu-id="194a4-128">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="194a4-129">W obszarze **typu zasobu**, wybierz pozycję **konta integracji**.</span><span class="sxs-lookup"><span data-stu-id="194a4-129">Under **Resource type**, select **Integration accounts**.</span></span> 
   4. <span data-ttu-id="194a4-130">W obszarze **zasobów**, wybierz konto integracji.</span><span class="sxs-lookup"><span data-stu-id="194a4-130">Under **Resource**, select your integration account.</span></span> 
   5. <span data-ttu-id="194a4-131">Wybierz **Włącz diagnostykę**.</span><span class="sxs-lookup"><span data-stu-id="194a4-131">Choose **Turn on diagnostics**.</span></span>

   ![Ustawienia diagnostyki dla Twojego konta integracji](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="194a4-133">W obszarze **ustawień diagnostycznych**, a następnie **stan**, wybierz **na**.</span><span class="sxs-lookup"><span data-stu-id="194a4-133">Under **Diagnostics settings**, and then **Status**, choose **On**.</span></span>

   ![Włącz diagnostykę Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="194a4-135">Teraz wybierz hello toouse obszaru roboczego i dane OMS logowania, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="194a4-135">Now select hello OMS workspace and data toouse for logging as shown:</span></span>

   1. <span data-ttu-id="194a4-136">Wybierz **wysyłania tooLog Analytics**.</span><span class="sxs-lookup"><span data-stu-id="194a4-136">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="194a4-137">W obszarze **analizy dzienników**, wybierz **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="194a4-137">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="194a4-138">W obszarze **obszarów roboczych OMS**, wybierz toouse obszar roboczy OMS hello logowania.</span><span class="sxs-lookup"><span data-stu-id="194a4-138">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="194a4-139">W obszarze **dziennika**, wybierz pozycję hello **IntegrationAccountTrackingEvents** kategorii.</span><span class="sxs-lookup"><span data-stu-id="194a4-139">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="194a4-140">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="194a4-140">Choose **Save**.</span></span>

   ![Konfigurowanie analizy dzienników, możesz wysłać dziennik tooa danych diagnostycznych](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="194a4-142">Teraz [skonfigurować śledzenie wiadomości B2B w OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="194a4-142">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a><span data-ttu-id="194a4-143">Włącz rejestrowanie danych diagnostycznych za pośrednictwem Monitora Azure</span><span class="sxs-lookup"><span data-stu-id="194a4-143">Turn on diagnostics logging through Azure Monitor</span></span>

1. <span data-ttu-id="194a4-144">W hello [portalu Azure](https://portal.azure.com)na temat hello Azure menu głównego, wybierz **Monitor**, **dzienników diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="194a4-144">In hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **Monitor**, **Diagnostics logs**.</span></span> <span data-ttu-id="194a4-145">Następnie wybierz konta integracji, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="194a4-145">Then select your integration account as shown here:</span></span>

   ![Wybierz pozycję "Monitoruj", "Dzienniki diagnostyczne", wybierz konto integracji](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. <span data-ttu-id="194a4-147">Po wybraniu konta integracji hello następujące wartości zostaną zaznaczone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="194a4-147">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="194a4-148">Jeśli te wartości są prawidłowe, wybierz **Włącz diagnostykę**.</span><span class="sxs-lookup"><span data-stu-id="194a4-148">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="194a4-149">W przeciwnym razie wybierz hello wartości, które mają:</span><span class="sxs-lookup"><span data-stu-id="194a4-149">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="194a4-150">W obszarze **subskrypcji**, wybierz hello subskrypcji platformy Azure korzystające z Twoim kontem integracji.</span><span class="sxs-lookup"><span data-stu-id="194a4-150">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="194a4-151">W obszarze **grupy zasobów**, wybierz grupę zasobów hello używanej z Twoim kontem integracji.</span><span class="sxs-lookup"><span data-stu-id="194a4-151">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="194a4-152">W obszarze **typu zasobu**, wybierz pozycję **konta integracji**.</span><span class="sxs-lookup"><span data-stu-id="194a4-152">Under **Resource type**, select **Integration accounts**.</span></span>
   4. <span data-ttu-id="194a4-153">W obszarze **zasobów**, wybierz konto integracji.</span><span class="sxs-lookup"><span data-stu-id="194a4-153">Under **Resource**, select your integration account.</span></span>
   5. <span data-ttu-id="194a4-154">Wybierz **Włącz diagnostykę**.</span><span class="sxs-lookup"><span data-stu-id="194a4-154">Choose **Turn on diagnostics**.</span></span>

   ![Ustawienia diagnostyki dla Twojego konta integracji](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="194a4-156">W obszarze **ustawień diagnostycznych**, wybierz **na**.</span><span class="sxs-lookup"><span data-stu-id="194a4-156">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Włącz diagnostykę Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="194a4-158">Teraz wybierz hello OMS obszaru roboczego i zdarzeń kategorii w celu rejestrowania, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="194a4-158">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="194a4-159">Wybierz **wysyłania tooLog Analytics**.</span><span class="sxs-lookup"><span data-stu-id="194a4-159">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="194a4-160">W obszarze **analizy dzienników**, wybierz **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="194a4-160">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="194a4-161">W obszarze **obszarów roboczych OMS**, wybierz toouse obszar roboczy OMS hello logowania.</span><span class="sxs-lookup"><span data-stu-id="194a4-161">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="194a4-162">W obszarze **dziennika**, wybierz pozycję hello **IntegrationAccountTrackingEvents** kategorii.</span><span class="sxs-lookup"><span data-stu-id="194a4-162">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="194a4-163">Gdy wszystko będzie gotowe, wybierz pozycję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="194a4-163">When you're done, choose **Save**.</span></span>

   ![Konfigurowanie analizy dzienników, możesz wysłać dziennik tooa danych diagnostycznych](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="194a4-165">Teraz [skonfigurować śledzenie wiadomości B2B w OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="194a4-165">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="194a4-166">Rozszerzanie, jak i gdzie używać danych diagnostycznych z innymi usługami</span><span class="sxs-lookup"><span data-stu-id="194a4-166">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="194a4-167">Wraz z Azure Log Analytics można rozszerzyć, jak używasz aplikacji logiki danych diagnostycznych z innymi usługami Azure, na przykład:</span><span class="sxs-lookup"><span data-stu-id="194a4-167">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="194a4-168">Archiwum, które dzienniki diagnostyczne platformy Azure w magazynie Azure</span><span class="sxs-lookup"><span data-stu-id="194a4-168">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="194a4-169">Strumień tooAzure dzienników diagnostyki Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="194a4-169">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="194a4-170">Następnie monitorowanie za pomocą telemetrii i analiza z innych usług, takich jak get w czasie rzeczywistym [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) i [usługi Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="194a4-170">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="194a4-171">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="194a4-171">For example:</span></span>

* [<span data-ttu-id="194a4-172">Strumień danych z usługi Event Hubs tooStream analityka</span><span class="sxs-lookup"><span data-stu-id="194a4-172">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="194a4-173">Analizować dane przesyłane strumieniowo z usługi Stream Analytics i utworzyć pulpit nawigacyjny analiz w czasie rzeczywistym w usłudze Power BI</span><span class="sxs-lookup"><span data-stu-id="194a4-173">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="194a4-174">Oparte na powitania opcje, które chcesz skonfigurować, upewnij się, że możesz pierwszy [utworzyć konto magazynu Azure](../storage/common/storage-create-storage-account.md) lub [tworzenia Centrum zdarzeń Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="194a4-174">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="194a4-175">Następnie wybierz opcje hello miejscu toosend danych diagnostycznych:</span><span class="sxs-lookup"><span data-stu-id="194a4-175">Then select hello options for where you want toosend diagnostic data:</span></span>

![Wysyłanie danych tooAzure magazynu konta lub zdarzenia Centrum](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="194a4-177">Okresy przechowywania mają zastosowanie tylko wtedy, gdy wybierzesz toouse konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="194a4-177">Retention periods apply only when you choose toouse a storage account.</span></span>

## <a name="supported-tracking-schemas"></a><span data-ttu-id="194a4-178">Obsługiwane schematy śledzenia</span><span class="sxs-lookup"><span data-stu-id="194a4-178">Supported tracking schemas</span></span>

<span data-ttu-id="194a4-179">Azure obsługuje tych typów schematów, które ustalone schematów z wyjątkiem hello niestandardowy typ śledzenia.</span><span class="sxs-lookup"><span data-stu-id="194a4-179">Azure supports these tracking schema types, which all have fixed schemas except hello Custom type.</span></span>

* [<span data-ttu-id="194a4-180">Schemat śledzenia AS2</span><span class="sxs-lookup"><span data-stu-id="194a4-180">AS2 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="194a4-181">Schemat śledzenia X12</span><span class="sxs-lookup"><span data-stu-id="194a4-181">X12 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="194a4-182">Niestandardowe schematy śledzenia</span><span class="sxs-lookup"><span data-stu-id="194a4-182">Custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="194a4-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="194a4-183">Next steps</span></span>

* [<span data-ttu-id="194a4-184">Śledzenie wiadomości B2B w OMS</span><span class="sxs-lookup"><span data-stu-id="194a4-184">Track B2B messages in OMS</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "wiadomości B2B śledzenie w OMS")
* [<span data-ttu-id="194a4-185">Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="194a4-185">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw")

