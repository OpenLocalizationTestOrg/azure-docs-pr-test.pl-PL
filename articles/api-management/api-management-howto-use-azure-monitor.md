---
title: "Monitorowanie zarządzanie interfejsami API Azure Monitor | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie monitorowania usługi Zarządzanie interfejsami API Azure za pomocą monitora Azure."
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
ms.openlocfilehash: 0f64947755c79739bb6f15325929bd074cfd7210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="eb908-103">Monitor interfejsu API zarządzania z Monitorem systemu Azure</span><span class="sxs-lookup"><span data-stu-id="eb908-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="eb908-104">Azure Monitor jest usługą platformy Azure, który udostępnia jedno źródło do monitorowania wszystkich zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eb908-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="eb908-105">Z monitorem Azure można zwizualizować, zapytania, trasy, archiwum i podejmuj działania na metryki i dzienników pochodzących z zasobów platformy Azure, takich jak zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="eb908-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on the metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="eb908-106">Poniższe wideo pokazuje, jak monitorować zarządzanie interfejsami API Azure monitora.</span><span class="sxs-lookup"><span data-stu-id="eb908-106">The following video shows how to monitor API Management using Azure Monitor.</span></span> <span data-ttu-id="eb908-107">Aby uzyskać więcej informacji na temat Monitora Azure, zobacz [Rozpoczynanie pracy z monitorem Azure].</span><span class="sxs-lookup"><span data-stu-id="eb908-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="eb908-108">Metryki</span><span class="sxs-lookup"><span data-stu-id="eb908-108">Metrics</span></span>
<span data-ttu-id="eb908-109">Zarządzanie interfejsami API obecnie emituje pięć metryki i planujemy dodać więcej w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="eb908-109">API Management currently emits five metrics and we plan to add more in the future.</span></span> <span data-ttu-id="eb908-110">Te metryki są emitowane co minutę, umożliwiając niemal w czasie rzeczywistym wgląd w stan i kondycję swoje interfejsy API.</span><span class="sxs-lookup"><span data-stu-id="eb908-110">These metrics are emitted every minute, giving you near real-time visibility into the state and health of your APIs.</span></span> <span data-ttu-id="eb908-111">Poniżej znajduje się podsumowanie metryki:</span><span class="sxs-lookup"><span data-stu-id="eb908-111">Following is a summary of the metrics:</span></span>
* <span data-ttu-id="eb908-112">Całkowita liczba żądań bramy: liczba interfejsu API żądań w okresie.</span><span class="sxs-lookup"><span data-stu-id="eb908-112">Total Gateway Requests: the number of API requests in the period.</span></span> 
* <span data-ttu-id="eb908-113">Liczba pomyślnych żądań bramy: liczba żądań interfejsu API, które otrzymały pomyślne kody odpowiedzi HTTP, w tym 304 307 i mniejszego niż 301 (na przykład 200).</span><span class="sxs-lookup"><span data-stu-id="eb908-113">Successful Gateway Requests: the number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="eb908-114">Żądań zakończonych niepowodzeniem bramy: liczba żądań interfejsu API, które odebrano błędną kody odpowiedzi HTTP, w tym 400 i niczego większych niż 500.</span><span class="sxs-lookup"><span data-stu-id="eb908-114">Failed Gateway Requests: the number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="eb908-115">Nieautoryzowanych żądań bramy: liczba żądań interfejsu API, które otrzymały kody odpowiedzi HTTP 401, 403 i 429 w tym.</span><span class="sxs-lookup"><span data-stu-id="eb908-115">Unauthorized Gateway Requests: the number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="eb908-116">Inne żądania bramy: liczba żądań interfejsu API, które otrzymały kody odpowiedzi HTTP, które nie należą do żadnej z powyższych kategorii (na przykład 418).</span><span class="sxs-lookup"><span data-stu-id="eb908-116">Other Gateway Requests: the number of API requests that received HTTP response codes that do not belong to any of the preceding categories (for example, 418).</span></span>

<span data-ttu-id="eb908-117">Dostępne metryki w usłudze API Management lub metryki dostęp do wszystkich zasobów platformy Azure w monitorze Azure.</span><span class="sxs-lookup"><span data-stu-id="eb908-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="eb908-118">Aby wyświetlić metryki w usłudze API Management:</span><span class="sxs-lookup"><span data-stu-id="eb908-118">To view metrics in your API Management service:</span></span>
1. <span data-ttu-id="eb908-119">Otwórz Azure portal.</span><span class="sxs-lookup"><span data-stu-id="eb908-119">Open the Azure portal.</span></span>
2. <span data-ttu-id="eb908-120">Przejdź do usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="eb908-120">Go to your API Management service.</span></span>
3. <span data-ttu-id="eb908-121">Kliknij przycisk **metryki**.</span><span class="sxs-lookup"><span data-stu-id="eb908-121">Click **Metrics**.</span></span>

![Metryki bloku][metrics-blade]

<span data-ttu-id="eb908-123">Aby uzyskać więcej informacji o sposobie używania metryki, zobacz [omówienie metryki].</span><span class="sxs-lookup"><span data-stu-id="eb908-123">For more information about how to use Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="eb908-124">Dzienniki aktywności</span><span class="sxs-lookup"><span data-stu-id="eb908-124">Activity Logs</span></span>
<span data-ttu-id="eb908-125">Dzienniki aktywności zapewniają wgląd w operacje wykonywane na usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="eb908-125">Activity logs provide insight into the operations that were performed on your API Management services.</span></span> <span data-ttu-id="eb908-126">Został on wcześniej znana jako "dzienników inspekcji" lub "operacyjne dzienniki".</span><span class="sxs-lookup"><span data-stu-id="eb908-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="eb908-127">Korzystając z Dzienniki aktywności, można określić ", co, która i kiedy" dla żadnego zapisu (PUT, POST, DELETE) podejmowaną w odniesieniu do usług interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="eb908-127">Using activity logs, you can determine the "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="eb908-128">Dzienniki aktywności nie obejmują operacji odczytu (GET) lub operacje wykonywane w klasycznym portalu wydawcy lub przy użyciu oryginalnego interfejsów API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="eb908-128">Activity logs do not include read (GET) operations or operations performed in the classic Publisher Portal or using the original Management APIs.</span></span>

<span data-ttu-id="eb908-129">Dostęp do dzienników aktywności w usłudze API Management lub uzyskać dostępu do dzienników wszystkich zasobów platformy Azure w monitorze Azure.</span><span class="sxs-lookup"><span data-stu-id="eb908-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="eb908-130">Aby wyświetlić aktywności logowania w usłudze API Management:</span><span class="sxs-lookup"><span data-stu-id="eb908-130">To view activity logs in your API Management service:</span></span>
1. <span data-ttu-id="eb908-131">Otwórz Azure portal.</span><span class="sxs-lookup"><span data-stu-id="eb908-131">Open the Azure portal.</span></span>
2. <span data-ttu-id="eb908-132">Przejdź do usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="eb908-132">Go to your API Management service.</span></span>
3. <span data-ttu-id="eb908-133">Kliknij przycisk **dziennik aktywności**.</span><span class="sxs-lookup"><span data-stu-id="eb908-133">Click **Activity log**.</span></span>

![Blok Dzienniki aktywności][activity-logs-blade]

<span data-ttu-id="eb908-135">Aby uzyskać więcej informacji o sposobie używania metryki, zobacz [omówienie Dzienniki aktywności].</span><span class="sxs-lookup"><span data-stu-id="eb908-135">For more information about how to use Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="eb908-136">Alerty</span><span class="sxs-lookup"><span data-stu-id="eb908-136">Alerts</span></span>
<span data-ttu-id="eb908-137">Można skonfigurować do odbierania alertów w oparciu metryki i działania dzienników.</span><span class="sxs-lookup"><span data-stu-id="eb908-137">You can configure to receive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="eb908-138">Azure Monitor umożliwia skonfigurowanie alert o konieczności wyzwala, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="eb908-138">Azure Monitor allows you to configure an alert to do the following when it triggers:</span></span>

* <span data-ttu-id="eb908-139">Wyślij wiadomość e-mail z powiadomieniem</span><span class="sxs-lookup"><span data-stu-id="eb908-139">Send an email notification</span></span>
* <span data-ttu-id="eb908-140">Wywołanie elementu webhook</span><span class="sxs-lookup"><span data-stu-id="eb908-140">Call a webhook</span></span>
* <span data-ttu-id="eb908-141">Wywołanie aplikacji logiki platformy Azure</span><span class="sxs-lookup"><span data-stu-id="eb908-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="eb908-142">Reguły alertów można skonfigurować w usłudze API Management lub w monitorze Azure.</span><span class="sxs-lookup"><span data-stu-id="eb908-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="eb908-143">Aby skonfigurować je w usłudze API Management:</span><span class="sxs-lookup"><span data-stu-id="eb908-143">To configure them in API Management:</span></span> 
1. <span data-ttu-id="eb908-144">Otwórz Azure portal.</span><span class="sxs-lookup"><span data-stu-id="eb908-144">Open the Azure portal.</span></span>
2. <span data-ttu-id="eb908-145">Przejdź do usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="eb908-145">Go to your API Management service.</span></span>
3. <span data-ttu-id="eb908-146">Kliknij przycisk **reguły alertów**.</span><span class="sxs-lookup"><span data-stu-id="eb908-146">Click **Alert rules**.</span></span>

![Blok reguły alertów][alert-rules-blade]

<span data-ttu-id="eb908-148">Aby uzyskać więcej informacji o korzystaniu z alertami, zobacz [Przegląd alertów].</span><span class="sxs-lookup"><span data-stu-id="eb908-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="eb908-149">Dzienniki diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="eb908-149">Diagnostic Logs</span></span>
<span data-ttu-id="eb908-150">Dzienniki diagnostyczne zawierają zaawansowane informacje o operacje i błędy, które są ważne w przypadku inspekcji, a także rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="eb908-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="eb908-151">Dzienniki diagnostyczne różnią się od Dzienniki aktywności.</span><span class="sxs-lookup"><span data-stu-id="eb908-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="eb908-152">Dzienniki aktywności wgląd w operacje wykonywane na zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eb908-152">Activity logs provide insights into the operations that were performed on your Azure resources.</span></span> <span data-ttu-id="eb908-153">Dzienniki diagnostyczne zapewniają wgląd w operacje, w zasobie wykonanie samego.</span><span class="sxs-lookup"><span data-stu-id="eb908-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="eb908-154">Zarządzanie interfejsami API zawiera obecnie diagnostyki dzienniki (umieścić w zadaniu wsadowym co godzinę) o poszczególnych interfejsu API żądania z każdego wpisu o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="eb908-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having the following structure:</span></span>

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

<span data-ttu-id="eb908-155">Można uzyskać dostępu do dzienników diagnostycznych w usłudze API Management lub uzyskać dostępu do dzienników wszystkich zasobów platformy Azure w monitorze Azure.</span><span class="sxs-lookup"><span data-stu-id="eb908-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="eb908-156">Aby wyświetlić dzienniki diagnostyczne w usłudze API Management:</span><span class="sxs-lookup"><span data-stu-id="eb908-156">To view diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="eb908-157">Otwórz Azure portal.</span><span class="sxs-lookup"><span data-stu-id="eb908-157">Open the Azure portal.</span></span>
2. <span data-ttu-id="eb908-158">Przejdź do usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="eb908-158">Go to your API Management service.</span></span>
3. <span data-ttu-id="eb908-159">Kliknij przycisk **dziennik diagnostyczny**.</span><span class="sxs-lookup"><span data-stu-id="eb908-159">Click **Diagnostic log**.</span></span>

![Blok dzienników diagnostycznych][diagnostic-logs-blade]

<span data-ttu-id="eb908-161">Aby uzyskać więcej informacji o sposobie używania metryki, zobacz [Przegląd dzienników diagnostycznych].</span><span class="sxs-lookup"><span data-stu-id="eb908-161">For more information about how to use Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="eb908-162">Następny krok</span><span class="sxs-lookup"><span data-stu-id="eb908-162">Next Step</span></span>

* <span data-ttu-id="eb908-163">[Rozpoczynanie pracy z monitorem Azure]</span><span class="sxs-lookup"><span data-stu-id="eb908-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="eb908-164">[omówienie metryki]</span><span class="sxs-lookup"><span data-stu-id="eb908-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="eb908-165">[omówienie Dzienniki aktywności]</span><span class="sxs-lookup"><span data-stu-id="eb908-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="eb908-166">[Przegląd dzienników diagnostycznych]</span><span class="sxs-lookup"><span data-stu-id="eb908-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="eb908-167">[Przegląd alertów]</span><span class="sxs-lookup"><span data-stu-id="eb908-167">[Overview of Alerts]</span></span>

<span data-ttu-id="eb908-168">[Rozpoczynanie pracy z monitorem Azure]: ../monitoring-and-diagnostics/monitoring-get-started.md</span><span class="sxs-lookup"><span data-stu-id="eb908-168">[Get Started with Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md</span></span>
<span data-ttu-id="eb908-169">[omówienie metryki]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span><span class="sxs-lookup"><span data-stu-id="eb908-169">[Overview of Metrics]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span></span>
<span data-ttu-id="eb908-170">[omówienie Dzienniki aktywności]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span><span class="sxs-lookup"><span data-stu-id="eb908-170">[Overview of Activity Logs]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span></span>
<span data-ttu-id="eb908-171">[Przegląd dzienników diagnostycznych]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span><span class="sxs-lookup"><span data-stu-id="eb908-171">[Overview of Diagnostic Logs]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span></span>
<span data-ttu-id="eb908-172">[Przegląd alertów]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span><span class="sxs-lookup"><span data-stu-id="eb908-172">[Overview of Alerts]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span></span>



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
