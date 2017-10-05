---
title: "Monitorowanie działań, zdarzenia i liczniki dla usługi równoważenia obciążenia | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak włączyć zdarzenia alertu i sondy kondycji stanu rejestrowania dla usługi równoważenia obciążenia Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 638ecd5e02889bd8cb6e7429dfcec335feaac4a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="b0bf8-103">Analiza dzienników dotyczących usługi Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="b0bf8-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="b0bf8-104">Różne typy dzienników Azure umożliwia zarządzanie i rozwiązywanie problemów z usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-104">You can use different types of logs in Azure to manage and troubleshoot load balancers.</span></span> <span data-ttu-id="b0bf8-105">Niektóre z tych dzienników jest możliwy za pośrednictwem portalu.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-105">Some of these logs can be accessed through the portal.</span></span> <span data-ttu-id="b0bf8-106">Wszystkie dzienniki można wyodrębnić z magazynu obiektów blob platformy Azure i wyświetlane w różnych narzędzi, takich jak program Excel i Power BI.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="b0bf8-107">Możesz można dowiedzieć się więcej o różnych typach dzienników z poniższej listy.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-107">You can learn more about the different types of logs from the list below.</span></span>

* <span data-ttu-id="b0bf8-108">**Dzienniki inspekcji:** można użyć [dzienników inspekcji platformy Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (wcześniej znane jako operacyjne dzienniki), aby wyświetlić wszystkie operacje przesyłany do Twojej subskrypcji platformy Azure i ich stan.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) to view all operations being submitted to your Azure subscription(s), and their status.</span></span> <span data-ttu-id="b0bf8-109">Dzienniki inspekcji są domyślnie włączone i mogą być wyświetlane w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-109">Audit logs are enabled by default, and can be viewed in the Azure portal.</span></span>
* <span data-ttu-id="b0bf8-110">**Dzienniki zdarzeń alertów:** ten dziennik służy do wyświetlania alertów rasied przez moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-110">**Alert event logs:** You can use this log to view alerts rasied by the load balancer.</span></span> <span data-ttu-id="b0bf8-111">Stan usługi równoważenia obciążenia są gromadzone co pięć minut.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-111">The status for the load balancer is collected every five minutes.</span></span> <span data-ttu-id="b0bf8-112">Ten dziennik napisano tylko, jeśli zdarzenia alertu modułu równoważenia obciążenia jest wywoływane.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="b0bf8-113">**Dzienniki badania kondycji:** ten dziennik służy do wyświetlania problemów wykrytych przez użytkownika sondy kondycji, takie jak liczba wystąpień w puli zaplecza, które nie są odbierane żądań z modułu równoważenia obciążenia z powodu błędów sondy kondycji.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-113">**Health probe logs:** You can use this log to view problems detected by your health probe, such as the number of instances in your backend-pool that are not receiving requests from the load balancer because of health probe failures.</span></span> <span data-ttu-id="b0bf8-114">Ten dziennik jest zapisywany po zmianie stanu sondy kondycji.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-114">This log is written to when there is a change in the health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0bf8-115">Zaloguj się analytics jest obecnie obsługiwane tylko w przypadku internetowy usług równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="b0bf8-116">Dzienniki są dostępne tylko dla zasobów wdrożone w modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-116">Logs are only available for resources deployed in the Resource Manager deployment model.</span></span> <span data-ttu-id="b0bf8-117">Nie można używać dzienników zasobów w klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-117">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="b0bf8-118">Aby uzyskać więcej informacji na temat modeli wdrażania, zobacz [wdrożenia Understanding Resource Manager oraz wdrażania klasycznego](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b0bf8-118">For more information about the deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="b0bf8-119">Włącz rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="b0bf8-119">Enable logging</span></span>

<span data-ttu-id="b0bf8-120">Rejestrowanie inspekcji jest automatycznie włączona dla każdego zasobu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="b0bf8-121">Musisz włączyć zdarzeń i rejestrowania sondy kondycji w celu rozpoczęcia, zbierania danych dostępne za pośrednictwem tych dzienników.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-121">You need to enable event and health probe logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="b0bf8-122">Wykonaj następujące kroki, aby włączyć rejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-122">Use the following steps to enable logging.</span></span>

<span data-ttu-id="b0bf8-123">Zaloguj się do [portalu Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b0bf8-123">Sign-in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="b0bf8-124">Jeśli nie masz już usługę równoważenia obciążenia, [tworzenia modułu równoważenia obciążenia](load-balancer-get-started-internet-arm-ps.md) przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="b0bf8-125">W portalu kliknij **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-125">In the portal, click **Browse**.</span></span>
2. <span data-ttu-id="b0bf8-126">Wybierz **usługi równoważenia obciążenia**.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-126">Select **Load Balancers**.</span></span>

    ![Portal — moduł równoważenia obciążenia](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="b0bf8-128">Wybierz istniejący moduł równoważenia obciążenia >> **wszystkie ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="b0bf8-129">Po prawej stronie okna dialogowego pod nazwą usługi równoważenia obciążenia, przewiń do **monitorowanie**, kliknij przycisk **diagnostyki**.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-129">On the right side of the dialog under the name of the load balancer, scroll to **Monitoring**, click **Diagnostics**.</span></span>

    ![Portal — ustawienia usługi równoważenia obciążenia](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="b0bf8-131">W **diagnostyki** okienku w obszarze **stan**, wybierz pozycję **na**.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-131">In the **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="b0bf8-132">Kliknij przycisk **konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="b0bf8-133">W obszarze **DZIENNIKI**, wybrać istniejące konto magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="b0bf8-134">Aby określić liczbę dni ważności danych zdarzenia będą przechowywane w dziennikach zdarzeń za pomocą suwaka.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-134">Use the slider to determine how many days worth of event data will be stored in the event logs.</span></span> 
8. <span data-ttu-id="b0bf8-135">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-135">Click **Save**.</span></span>

    ![Portal — dzienniki diagnostyczne](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="b0bf8-137">Dzienniki inspekcji nie wymagają oddzielnego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="b0bf8-138">Użycie magazynu dla zdarzeń i kondycji sondowania rejestrowania będą naliczane opłaty za usługę.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-138">The use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="b0bf8-139">Dziennik inspekcji</span><span class="sxs-lookup"><span data-stu-id="b0bf8-139">Audit log</span></span>

<span data-ttu-id="b0bf8-140">Dziennik inspekcji jest generowany domyślnie.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-140">The audit log is generated by default.</span></span> <span data-ttu-id="b0bf8-141">Dzienniki są zachowywane przez 90 dni w magazynie dzienniki zdarzeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-141">The logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="b0bf8-142">Dowiedz się więcej o tych dzienników, odczytując [wyświetlania zdarzeń i dzienniki inspekcji](../monitoring-and-diagnostics/insights-debugging-with-events.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-142">Learn more about these logs by reading the [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="b0bf8-143">Dziennik zdarzeń alertów</span><span class="sxs-lookup"><span data-stu-id="b0bf8-143">Alert event log</span></span>

<span data-ttu-id="b0bf8-144">Ten dziennik jest generowany tylko, jeśli włączono na poszczególnych usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="b0bf8-145">Zdarzenia są rejestrowane w formacie JSON i przechowywane na koncie magazynu, określone po włączeniu rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-145">The events are logged in JSON format and stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="b0bf8-146">Oto przykład zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-146">The following is an example of an event.</span></span>

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

<span data-ttu-id="b0bf8-147">Przedstawia dane wyjściowe JSON *eventname* właściwość, która będzie opisywać Przyczyna dla usługi równoważenia obciążenia utworzony alert.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-147">The JSON output shows the *eventname* property which will describe the reason for the load balancer created an alert.</span></span> <span data-ttu-id="b0bf8-148">W takim przypadku alert wygenerowany został z powodu wyczerpania port TCP spowodowane przez źródło IP translatora adresów Sieciowych limity (SNAT).</span><span class="sxs-lookup"><span data-stu-id="b0bf8-148">In this case, the alert generated was due to TCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="b0bf8-149">Dziennik badania kondycji</span><span class="sxs-lookup"><span data-stu-id="b0bf8-149">Health probe log</span></span>

<span data-ttu-id="b0bf8-150">Ten dziennik jest generowany tylko, jeśli włączono na poszczególnych obciążenia równoważenia zgodnie z opisem powyżej.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="b0bf8-151">Dane są przechowywane na koncie magazynu, określone po włączeniu rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-151">The data is stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="b0bf8-152">Kontener o nazwie "insights dzienniki loadbalancerprobehealthstatus" jest tworzony i rejestrowane są następujące dane:</span><span class="sxs-lookup"><span data-stu-id="b0bf8-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and the following data is logged:</span></span>

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

<span data-ttu-id="b0bf8-153">Dane wyjściowe JSON w polu właściwości zawiera podstawowe informacje dotyczące stanu kondycji sondowania.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-153">The JSON output shows in the properties field the basic information for the probe health status.</span></span> <span data-ttu-id="b0bf8-154">*DipDownCount* właściwość zawiera całkowitą liczbę wystąpień na zaplecza, które nie są odbierane ruchu sieciowego z powodu odpowiedzi sondy nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-154">The *dipDownCount* property shows the total number of instances on the back-end which are not receiving network traffic due to failed probe responses.</span></span>

## <a name="view-and-analyze-the-audit-log"></a><span data-ttu-id="b0bf8-155">Wyświetlanie i analizowanie dzienników inspekcji</span><span class="sxs-lookup"><span data-stu-id="b0bf8-155">View and analyze the audit log</span></span>

<span data-ttu-id="b0bf8-156">Można wyświetlać i analizować dane dzienników inspekcji przy użyciu dowolnej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="b0bf8-156">You can view and analyze audit log data using any of the following methods:</span></span>

* <span data-ttu-id="b0bf8-157">**Narzędzia platformy Azure:** pobieranie informacji z dzienników inspekcji za pośrednictwem programu Azure PowerShell, interfejsu wiersza polecenia platformy Azure (CLI), interfejsu API REST Azure lub w portalu Azure w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-157">**Azure tools:** Retrieve information from the audit logs through Azure PowerShell, the Azure Command Line Interface (CLI), the Azure REST API, or the Azure preview portal.</span></span> <span data-ttu-id="b0bf8-158">Instrukcje krok po kroku dla każdej metody wyszczególnione w [inspekcji operacji za pomocą Menedżera zasobów](../azure-resource-manager/resource-group-audit.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-158">Step-by-step instructions for each method are detailed in the [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="b0bf8-159">**Usługa Power BI:** Jeśli jeszcze nie masz [usługi Power BI](https://powerbi.microsoft.com/pricing) konta, możesz spróbować ją bezpłatnie.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="b0bf8-160">Przy użyciu [dzienników inspekcji platformy Azure zawartości pakietu dla usługi Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs)można analizować danych za pomocą wstępnie skonfigurowanych pulpitów nawigacyjnych i można dostosowywać widoki ze swoimi potrzebami.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-160">Using the [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views to suit your requirements.</span></span>

## <a name="view-and-analyze-the-health-probe-and-event-log"></a><span data-ttu-id="b0bf8-161">Wyświetlanie i analizowanie sondy kondycji i dziennika zdarzeń</span><span class="sxs-lookup"><span data-stu-id="b0bf8-161">View and analyze the health probe and event log</span></span>

<span data-ttu-id="b0bf8-162">Należy do łączenia się z kontem magazynu i pobierania JSON wpisów dziennika zdarzeń i kondycji dzienników sondowania.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-162">You need to connect to your storage account and retrieve the JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="b0bf8-163">Po pobraniu pliki w formacie JSON, należy przekonwertować je na CSV i widoku w programie Excel, usłudze PowerBI lub inne narzędzie do wizualizacji danych.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-163">Once you download the JSON files, you can convert them to CSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="b0bf8-164">Jeśli znasz podstawowe koncepcje zmiany wartości stałych i zmiennych w języku C# i Visual Studio, możesz użyć [dziennika narzędzia konwertera](https://github.com/Azure-Samples/networking-dotnet-log-converter) dostępne w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b0bf8-165">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b0bf8-165">Additional resources</span></span>

* <span data-ttu-id="b0bf8-166">[Wizualizuj dzienników inspekcji Azure przy użyciu usługi Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) wpis w blogu.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="b0bf8-167">[Wyświetlanie i analizowanie dzienników inspekcji platformy Azure w usłudze Power BI i nie tylko](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) wpis w blogu.</span><span class="sxs-lookup"><span data-stu-id="b0bf8-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0bf8-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b0bf8-168">Next steps</span></span>

[<span data-ttu-id="b0bf8-169">Opis sond modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="b0bf8-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
