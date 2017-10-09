---
title: "Zarządzanie interfejsami API Azure Monitor aaaMonitor | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor Azure API Management usługi przy użyciu monitora Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="131ed-103">Monitor interfejsu API zarządzania z Monitorem systemu Azure</span><span class="sxs-lookup"><span data-stu-id="131ed-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="131ed-104">Azure Monitor jest usługą platformy Azure, który udostępnia jedno źródło do monitorowania wszystkich zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="131ed-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="131ed-105">Z monitorem Azure można zwizualizować, zapytania, trasy, archiwizacji i podejmuj działania na powitania metryki i dzienników pochodzących z zasobów platformy Azure, takich jak zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="131ed-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on hello metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="131ed-106">Witaj, po wideo pokazuje, jak toomonitor zarządzanie interfejsami API Azure monitora.</span><span class="sxs-lookup"><span data-stu-id="131ed-106">hello following video shows how toomonitor API Management using Azure Monitor.</span></span> <span data-ttu-id="131ed-107">Aby uzyskać więcej informacji na temat Monitora Azure, zobacz [Rozpoczynanie pracy z monitorem Azure].</span><span class="sxs-lookup"><span data-stu-id="131ed-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="131ed-108">Metryki</span><span class="sxs-lookup"><span data-stu-id="131ed-108">Metrics</span></span>
<span data-ttu-id="131ed-109">Zarządzanie interfejsami API obecnie emituje pięć metryki i planujemy tooadd więcej w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="131ed-109">API Management currently emits five metrics and we plan tooadd more in hello future.</span></span> <span data-ttu-id="131ed-110">Te metryki są emitowane co minutę, umożliwiając niemal w czasie rzeczywistym wgląd w stan hello i kondycji swoje interfejsy API.</span><span class="sxs-lookup"><span data-stu-id="131ed-110">These metrics are emitted every minute, giving you near real-time visibility into hello state and health of your APIs.</span></span> <span data-ttu-id="131ed-111">Poniżej znajduje się podsumowanie hello metryki:</span><span class="sxs-lookup"><span data-stu-id="131ed-111">Following is a summary of hello metrics:</span></span>
* <span data-ttu-id="131ed-112">Całkowita liczba żądań bramy: hello liczba interfejsu API żądań w okresie hello.</span><span class="sxs-lookup"><span data-stu-id="131ed-112">Total Gateway Requests: hello number of API requests in hello period.</span></span> 
* <span data-ttu-id="131ed-113">Pomyślnych żądań bramy: hello liczba żądań interfejsu API, które otrzymały pomyślne kody odpowiedzi HTTP, w tym 304 307 i mniejszego niż 301 (na przykład 200).</span><span class="sxs-lookup"><span data-stu-id="131ed-113">Successful Gateway Requests: hello number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="131ed-114">Nieudane żądania bramy: hello liczba żądań interfejsu API, które odebrano błędną kody odpowiedzi HTTP, w tym 400 i niczego większych niż 500.</span><span class="sxs-lookup"><span data-stu-id="131ed-114">Failed Gateway Requests: hello number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="131ed-115">Nieautoryzowanych żądań bramy: hello liczba żądań interfejsu API, które otrzymały kody odpowiedzi HTTP 401, 403 i 429 w tym.</span><span class="sxs-lookup"><span data-stu-id="131ed-115">Unauthorized Gateway Requests: hello number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="131ed-116">Inne żądania bramy: hello liczba żądań interfejsu API, które otrzymały kody odpowiedzi HTTP, które nie należą tooany hello poprzedzających kategorii (na przykład 418).</span><span class="sxs-lookup"><span data-stu-id="131ed-116">Other Gateway Requests: hello number of API requests that received HTTP response codes that do not belong tooany of hello preceding categories (for example, 418).</span></span>

<span data-ttu-id="131ed-117">Dostępne metryki w usłudze API Management lub metryki dostęp do wszystkich zasobów platformy Azure w monitorze Azure.</span><span class="sxs-lookup"><span data-stu-id="131ed-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="131ed-118">metryki tooview w usłudze API Management:</span><span class="sxs-lookup"><span data-stu-id="131ed-118">tooview metrics in your API Management service:</span></span>
1. <span data-ttu-id="131ed-119">Otwórz hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="131ed-119">Open hello Azure portal.</span></span>
2. <span data-ttu-id="131ed-120">Przejdź usługi Zarządzanie interfejsami API tooyour.</span><span class="sxs-lookup"><span data-stu-id="131ed-120">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="131ed-121">Kliknij przycisk **metryki**.</span><span class="sxs-lookup"><span data-stu-id="131ed-121">Click **Metrics**.</span></span>

![Metryki bloku][metrics-blade]

<span data-ttu-id="131ed-123">Aby uzyskać więcej informacji o tym, jak toouse metryki, zobacz [omówienie metryki].</span><span class="sxs-lookup"><span data-stu-id="131ed-123">For more information about how toouse Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="131ed-124">Dzienniki aktywności</span><span class="sxs-lookup"><span data-stu-id="131ed-124">Activity Logs</span></span>
<span data-ttu-id="131ed-125">Dzienniki aktywności zapewniają wgląd w operacji hello, wykonywane na usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="131ed-125">Activity logs provide insight into hello operations that were performed on your API Management services.</span></span> <span data-ttu-id="131ed-126">Został on wcześniej znana jako "dzienników inspekcji" lub "operacyjne dzienniki".</span><span class="sxs-lookup"><span data-stu-id="131ed-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="131ed-127">Przy użyciu dzienników działania, można określić hello ", co, która i kiedy" dla operacji (PUT, POST, DELETE) podejmowaną w odniesieniu do usługi API Management żadnego zapisu.</span><span class="sxs-lookup"><span data-stu-id="131ed-127">Using activity logs, you can determine hello "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="131ed-128">Dzienniki aktywności nie obejmują operacji odczytu (GET) lub operacje wykonywane w hello klasyczny Portal wydawcy lub przy użyciu hello oryginalnego interfejsów API Management.</span><span class="sxs-lookup"><span data-stu-id="131ed-128">Activity logs do not include read (GET) operations or operations performed in hello classic Publisher Portal or using hello original Management APIs.</span></span>

<span data-ttu-id="131ed-129">Dostęp do dzienników aktywności w usłudze API Management lub uzyskać dostępu do dzienników wszystkich zasobów platformy Azure w monitorze Azure.</span><span class="sxs-lookup"><span data-stu-id="131ed-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="131ed-130">rejestruje działania tooview w usłudze API Management:</span><span class="sxs-lookup"><span data-stu-id="131ed-130">tooview activity logs in your API Management service:</span></span>
1. <span data-ttu-id="131ed-131">Otwórz hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="131ed-131">Open hello Azure portal.</span></span>
2. <span data-ttu-id="131ed-132">Przejdź usługi Zarządzanie interfejsami API tooyour.</span><span class="sxs-lookup"><span data-stu-id="131ed-132">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="131ed-133">Kliknij przycisk **dziennik aktywności**.</span><span class="sxs-lookup"><span data-stu-id="131ed-133">Click **Activity log**.</span></span>

![Blok Dzienniki aktywności][activity-logs-blade]

<span data-ttu-id="131ed-135">Aby uzyskać więcej informacji o tym, jak toouse metryki, zobacz [omówienie Dzienniki aktywności].</span><span class="sxs-lookup"><span data-stu-id="131ed-135">For more information about how toouse Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="131ed-136">Alerty</span><span class="sxs-lookup"><span data-stu-id="131ed-136">Alerts</span></span>
<span data-ttu-id="131ed-137">Można skonfigurować alerty tooreceive oparte na dzienniki metryki i działania.</span><span class="sxs-lookup"><span data-stu-id="131ed-137">You can configure tooreceive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="131ed-138">Azure Monitor pozwala tooconfigure toodo alertu powitania po wyzwala:</span><span class="sxs-lookup"><span data-stu-id="131ed-138">Azure Monitor allows you tooconfigure an alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="131ed-139">Wyślij wiadomość e-mail z powiadomieniem</span><span class="sxs-lookup"><span data-stu-id="131ed-139">Send an email notification</span></span>
* <span data-ttu-id="131ed-140">Wywołanie elementu webhook</span><span class="sxs-lookup"><span data-stu-id="131ed-140">Call a webhook</span></span>
* <span data-ttu-id="131ed-141">Wywołanie aplikacji logiki platformy Azure</span><span class="sxs-lookup"><span data-stu-id="131ed-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="131ed-142">Reguły alertów można skonfigurować w usłudze API Management lub w monitorze Azure.</span><span class="sxs-lookup"><span data-stu-id="131ed-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="131ed-143">tooconfigure ich w usłudze API Management:</span><span class="sxs-lookup"><span data-stu-id="131ed-143">tooconfigure them in API Management:</span></span> 
1. <span data-ttu-id="131ed-144">Otwórz hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="131ed-144">Open hello Azure portal.</span></span>
2. <span data-ttu-id="131ed-145">Przejdź usługi Zarządzanie interfejsami API tooyour.</span><span class="sxs-lookup"><span data-stu-id="131ed-145">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="131ed-146">Kliknij przycisk **reguły alertów**.</span><span class="sxs-lookup"><span data-stu-id="131ed-146">Click **Alert rules**.</span></span>

![Blok reguły alertów][alert-rules-blade]

<span data-ttu-id="131ed-148">Aby uzyskać więcej informacji o korzystaniu z alertami, zobacz [Przegląd alertów].</span><span class="sxs-lookup"><span data-stu-id="131ed-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="131ed-149">Dzienniki diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="131ed-149">Diagnostic Logs</span></span>
<span data-ttu-id="131ed-150">Dzienniki diagnostyczne zawierają zaawansowane informacje o operacje i błędy, które są ważne w przypadku inspekcji, a także rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="131ed-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="131ed-151">Dzienniki diagnostyczne różnią się od Dzienniki aktywności.</span><span class="sxs-lookup"><span data-stu-id="131ed-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="131ed-152">Dzienniki aktywności wgląd w działania hello, wykonywane na zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="131ed-152">Activity logs provide insights into hello operations that were performed on your Azure resources.</span></span> <span data-ttu-id="131ed-153">Dzienniki diagnostyczne zapewniają wgląd w operacje, w zasobie wykonanie samego.</span><span class="sxs-lookup"><span data-stu-id="131ed-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="131ed-154">Zarządzanie interfejsami API zawiera obecnie diagnostyki dzienniki (umieścić w zadaniu wsadowym co godzinę) o poszczególnych interfejsu API żądania z każdego wpisu o hello następujące struktury:</span><span class="sxs-lookup"><span data-stu-id="131ed-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having hello following structure:</span></span>

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

<span data-ttu-id="131ed-155">Można uzyskać dostępu do dzienników diagnostycznych w usłudze API Management lub uzyskać dostępu do dzienników wszystkich zasobów platformy Azure w monitorze Azure.</span><span class="sxs-lookup"><span data-stu-id="131ed-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="131ed-156">dzienniki diagnostyczne tooview w usłudze API Management:</span><span class="sxs-lookup"><span data-stu-id="131ed-156">tooview diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="131ed-157">Otwórz hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="131ed-157">Open hello Azure portal.</span></span>
2. <span data-ttu-id="131ed-158">Przejdź usługi Zarządzanie interfejsami API tooyour.</span><span class="sxs-lookup"><span data-stu-id="131ed-158">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="131ed-159">Kliknij przycisk **dziennik diagnostyczny**.</span><span class="sxs-lookup"><span data-stu-id="131ed-159">Click **Diagnostic log**.</span></span>

![Blok dzienników diagnostycznych][diagnostic-logs-blade]

<span data-ttu-id="131ed-161">Aby uzyskać więcej informacji o tym, jak toouse metryki, zobacz [Przegląd dzienników diagnostycznych].</span><span class="sxs-lookup"><span data-stu-id="131ed-161">For more information about how toouse Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="131ed-162">Następny krok</span><span class="sxs-lookup"><span data-stu-id="131ed-162">Next Step</span></span>

* <span data-ttu-id="131ed-163">[Rozpoczynanie pracy z monitorem Azure]</span><span class="sxs-lookup"><span data-stu-id="131ed-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="131ed-164">[omówienie metryki]</span><span class="sxs-lookup"><span data-stu-id="131ed-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="131ed-165">[omówienie Dzienniki aktywności]</span><span class="sxs-lookup"><span data-stu-id="131ed-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="131ed-166">[Przegląd dzienników diagnostycznych]</span><span class="sxs-lookup"><span data-stu-id="131ed-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="131ed-167">[Przegląd alertów]</span><span class="sxs-lookup"><span data-stu-id="131ed-167">[Overview of Alerts]</span></span>

[Rozpoczynanie pracy z monitorem Azure]: ../monitoring-and-diagnostics/monitoring-get-started.md
[omówienie metryki]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[omówienie Dzienniki aktywności]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[Przegląd dzienników diagnostycznych]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[Przegląd alertów]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
