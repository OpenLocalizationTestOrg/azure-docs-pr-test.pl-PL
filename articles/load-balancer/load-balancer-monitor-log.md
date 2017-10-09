---
title: "aaaMonitor operacje, zdarzenia i liczniki dla usługi równoważenia obciążenia | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooenable alertów zdarzeń i sondy kondycji stanu rejestrowania dla usługi równoważenia obciążenia Azure"
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
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="30b4d-103">Analiza dzienników dotyczących usługi Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="30b4d-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="30b4d-104">Można użyć różnych typów dzienników w Azure toomanage i rozwiązywanie problemów z usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="30b4d-104">You can use different types of logs in Azure toomanage and troubleshoot load balancers.</span></span> <span data-ttu-id="30b4d-105">Niektóre z tych dzienników jest możliwy za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="30b4d-105">Some of these logs can be accessed through hello portal.</span></span> <span data-ttu-id="30b4d-106">Wszystkie dzienniki można wyodrębnić z magazynu obiektów blob platformy Azure i wyświetlane w różnych narzędzi, takich jak program Excel i Power BI.</span><span class="sxs-lookup"><span data-stu-id="30b4d-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="30b4d-107">Użytkownik może Dowiedz się więcej o hello różne typy dzienników z poniższej listy hello.</span><span class="sxs-lookup"><span data-stu-id="30b4d-107">You can learn more about hello different types of logs from hello list below.</span></span>

* <span data-ttu-id="30b4d-108">**Dzienniki inspekcji:** można użyć [dzienników inspekcji platformy Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (wcześniej znane jako operacyjne dzienniki) tooview wszystkie operacje są przesłane tooyour subskrypcji platformy Azure i ich stan.</span><span class="sxs-lookup"><span data-stu-id="30b4d-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) tooview all operations being submitted tooyour Azure subscription(s), and their status.</span></span> <span data-ttu-id="30b4d-109">Dzienniki inspekcji są domyślnie włączone i mogą być wyświetlane w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="30b4d-109">Audit logs are enabled by default, and can be viewed in hello Azure portal.</span></span>
* <span data-ttu-id="30b4d-110">**Dzienniki zdarzeń alertów:** można użyć tego dziennika tooview alerty rasied przez hello równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="30b4d-110">**Alert event logs:** You can use this log tooview alerts rasied by hello load balancer.</span></span> <span data-ttu-id="30b4d-111">Stan powitania dla usługi równoważenia obciążenia hello są gromadzone co pięć minut.</span><span class="sxs-lookup"><span data-stu-id="30b4d-111">hello status for hello load balancer is collected every five minutes.</span></span> <span data-ttu-id="30b4d-112">Ten dziennik napisano tylko, jeśli zdarzenia alertu modułu równoważenia obciążenia jest wywoływane.</span><span class="sxs-lookup"><span data-stu-id="30b4d-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="30b4d-113">**Dzienniki badania kondycji:** można użyć tego dziennika tooview problemach przez użytkownika sondy kondycji, takich jak hello liczbę wystąpień w puli zaplecza, które nie są odbierane żądań z modułu równoważenia obciążenia hello spowodowane błędami sondy kondycji.</span><span class="sxs-lookup"><span data-stu-id="30b4d-113">**Health probe logs:** You can use this log tooview problems detected by your health probe, such as hello number of instances in your backend-pool that are not receiving requests from hello load balancer because of health probe failures.</span></span> <span data-ttu-id="30b4d-114">Ten dziennik jest zapisywany toowhen nastąpiła zmiana stanu sondy kondycji hello.</span><span class="sxs-lookup"><span data-stu-id="30b4d-114">This log is written toowhen there is a change in hello health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30b4d-115">Zaloguj się analytics jest obecnie obsługiwane tylko w przypadku internetowy usług równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="30b4d-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="30b4d-116">Dzienniki są dostępne tylko dla zasobów wdrożone w modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="30b4d-116">Logs are only available for resources deployed in hello Resource Manager deployment model.</span></span> <span data-ttu-id="30b4d-117">Nie można używać dzienników zasobów w hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="30b4d-117">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="30b4d-118">Aby uzyskać więcej informacji na temat modeli wdrażania hello, zobacz [wdrożenia Understanding Resource Manager oraz wdrażania klasycznego](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="30b4d-118">For more information about hello deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="30b4d-119">Włącz rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="30b4d-119">Enable logging</span></span>

<span data-ttu-id="30b4d-120">Rejestrowanie inspekcji jest automatycznie włączona dla każdego zasobu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="30b4d-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="30b4d-121">Należy tooenable zdarzeń i toostart rejestrowania sondy kondycji zbierania danych hello dostępne za pośrednictwem tych dzienników.</span><span class="sxs-lookup"><span data-stu-id="30b4d-121">You need tooenable event and health probe logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="30b4d-122">Użyj hello następujące kroki tooenable rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="30b4d-122">Use hello following steps tooenable logging.</span></span>

<span data-ttu-id="30b4d-123">Logowanie toohello [portalu Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="30b4d-123">Sign-in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="30b4d-124">Jeśli nie masz już usługę równoważenia obciążenia, [tworzenia modułu równoważenia obciążenia](load-balancer-get-started-internet-arm-ps.md) przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="30b4d-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="30b4d-125">W portalu powitania kliknij **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="30b4d-125">In hello portal, click **Browse**.</span></span>
2. <span data-ttu-id="30b4d-126">Wybierz **usługi równoważenia obciążenia**.</span><span class="sxs-lookup"><span data-stu-id="30b4d-126">Select **Load Balancers**.</span></span>

    ![Portal — moduł równoważenia obciążenia](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="30b4d-128">Wybierz istniejący moduł równoważenia obciążenia >> **wszystkie ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="30b4d-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="30b4d-129">Na powitania po prawej stronie okna dialogowego hello pod nazwą hello hello usługi równoważenia obciążenia, przewiń zbyt**monitorowanie**, kliknij przycisk **diagnostyki**.</span><span class="sxs-lookup"><span data-stu-id="30b4d-129">On hello right side of hello dialog under hello name of hello load balancer, scroll too**Monitoring**, click **Diagnostics**.</span></span>

    ![Portal — ustawienia usługi równoważenia obciążenia](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="30b4d-131">W hello **diagnostyki** okienku w obszarze **stan**, wybierz pozycję **na**.</span><span class="sxs-lookup"><span data-stu-id="30b4d-131">In hello **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="30b4d-132">Kliknij przycisk **konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="30b4d-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="30b4d-133">W obszarze **DZIENNIKI**, wybrać istniejące konto magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="30b4d-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="30b4d-134">Użyj toodetermine suwaka hello ilu dniach danych zdarzenia będą przechowywane w dziennikach zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="30b4d-134">Use hello slider toodetermine how many days worth of event data will be stored in hello event logs.</span></span> 
8. <span data-ttu-id="30b4d-135">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="30b4d-135">Click **Save**.</span></span>

    ![Portal — dzienniki diagnostyczne](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="30b4d-137">Dzienniki inspekcji nie wymagają oddzielnego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="30b4d-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="30b4d-138">Witaj wykorzystania przestrzeni dyskowej na zdarzenie oraz kondycji sondowania rejestrowania będą naliczane opłaty za usługę.</span><span class="sxs-lookup"><span data-stu-id="30b4d-138">hello use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="30b4d-139">Dziennik inspekcji</span><span class="sxs-lookup"><span data-stu-id="30b4d-139">Audit log</span></span>

<span data-ttu-id="30b4d-140">Dziennik inspekcji Hello jest generowany domyślnie.</span><span class="sxs-lookup"><span data-stu-id="30b4d-140">hello audit log is generated by default.</span></span> <span data-ttu-id="30b4d-141">Dzienniki Hello są zachowywane przez 90 dni w magazynie dzienniki zdarzeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="30b4d-141">hello logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="30b4d-142">Dowiedz się więcej o tych dzienników, odczytując hello [wyświetlania zdarzeń i dzienniki inspekcji](../monitoring-and-diagnostics/insights-debugging-with-events.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="30b4d-142">Learn more about these logs by reading hello [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="30b4d-143">Dziennik zdarzeń alertów</span><span class="sxs-lookup"><span data-stu-id="30b4d-143">Alert event log</span></span>

<span data-ttu-id="30b4d-144">Ten dziennik jest generowany tylko, jeśli włączono na poszczególnych usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="30b4d-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="30b4d-145">Hello zdarzenia są rejestrowane w formacie JSON i przechowywane na koncie magazynu hello określone, gdy włączone rejestrowanie hello.</span><span class="sxs-lookup"><span data-stu-id="30b4d-145">hello events are logged in JSON format and stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="30b4d-146">Witaj poniżej znajduje się przykład zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="30b4d-146">hello following is an example of an event.</span></span>

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

<span data-ttu-id="30b4d-147">Pokazuje hello output Hello JSON *eventname* właściwość, która będzie opisywać hello Przyczyna hello modułu równoważenia obciążenia utworzony alert.</span><span class="sxs-lookup"><span data-stu-id="30b4d-147">hello JSON output shows hello *eventname* property which will describe hello reason for hello load balancer created an alert.</span></span> <span data-ttu-id="30b4d-148">W takim przypadku hello alert wygenerowany został powodu tooTCP portu wyczerpania spowodowane przez źródło, który ogranicza IP translatora adresów Sieciowych (SNAT).</span><span class="sxs-lookup"><span data-stu-id="30b4d-148">In this case, hello alert generated was due tooTCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="30b4d-149">Dziennik badania kondycji</span><span class="sxs-lookup"><span data-stu-id="30b4d-149">Health probe log</span></span>

<span data-ttu-id="30b4d-150">Ten dziennik jest generowany tylko, jeśli włączono na poszczególnych obciążenia równoważenia zgodnie z opisem powyżej.</span><span class="sxs-lookup"><span data-stu-id="30b4d-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="30b4d-151">Witaj dane są przechowywane na koncie magazynu hello określone, gdy włączone rejestrowanie hello.</span><span class="sxs-lookup"><span data-stu-id="30b4d-151">hello data is stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="30b4d-152">Kontener o nazwie "insights dzienniki loadbalancerprobehealthstatus" jest tworzony i jest rejestrowany hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="30b4d-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and hello following data is logged:</span></span>

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

<span data-ttu-id="30b4d-153">dane wyjściowe JSON Hello zawiera hello właściwości pola hello podstawowe informacje dotyczące stanu kondycji hello sondowania.</span><span class="sxs-lookup"><span data-stu-id="30b4d-153">hello JSON output shows in hello properties field hello basic information for hello probe health status.</span></span> <span data-ttu-id="30b4d-154">Witaj *dipDownCount* właściwość pokazuje hello całkowita liczba wystąpień na zaplecza hello, które nie są odbierane ruchu sieciowego powodu toofailed sondowania odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="30b4d-154">hello *dipDownCount* property shows hello total number of instances on hello back-end which are not receiving network traffic due toofailed probe responses.</span></span>

## <a name="view-and-analyze-hello-audit-log"></a><span data-ttu-id="30b4d-155">Wyświetlanie i analizowanie dzienników inspekcji hello</span><span class="sxs-lookup"><span data-stu-id="30b4d-155">View and analyze hello audit log</span></span>

<span data-ttu-id="30b4d-156">Można wyświetlać i analizować dane dzienników inspekcji przy użyciu dowolnej z następujących metod hello:</span><span class="sxs-lookup"><span data-stu-id="30b4d-156">You can view and analyze audit log data using any of hello following methods:</span></span>

* <span data-ttu-id="30b4d-157">**Narzędzia platformy Azure:** pobieranie informacji z dzienników inspekcji hello za pomocą programu Azure PowerShell, hello Azure interfejsu wiersza polecenia (CLI), hello interfejsu API REST Azure lub hello Azure w wersji zapoznawczej portalu.</span><span class="sxs-lookup"><span data-stu-id="30b4d-157">**Azure tools:** Retrieve information from hello audit logs through Azure PowerShell, hello Azure Command Line Interface (CLI), hello Azure REST API, or hello Azure preview portal.</span></span> <span data-ttu-id="30b4d-158">Instrukcje krok po kroku dla każdej metody wyszczególnione w hello [inspekcji operacji za pomocą Menedżera zasobów](../azure-resource-manager/resource-group-audit.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="30b4d-158">Step-by-step instructions for each method are detailed in hello [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="30b4d-159">**Usługa Power BI:** Jeśli jeszcze nie masz [usługi Power BI](https://powerbi.microsoft.com/pricing) konta, możesz spróbować ją bezpłatnie.</span><span class="sxs-lookup"><span data-stu-id="30b4d-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="30b4d-160">Przy użyciu hello [dzienników inspekcji platformy Azure zawartości pakietu dla usługi Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs)można analizować danych za pomocą wstępnie skonfigurowanych pulpitów nawigacyjnych i można dostosowywać widoki toosuit wymagań.</span><span class="sxs-lookup"><span data-stu-id="30b4d-160">Using hello [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views toosuit your requirements.</span></span>

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a><span data-ttu-id="30b4d-161">Wyświetlanie i analizowanie hello sondy kondycji i dziennika zdarzeń</span><span class="sxs-lookup"><span data-stu-id="30b4d-161">View and analyze hello health probe and event log</span></span>

<span data-ttu-id="30b4d-162">Potrzebny jest magazyn tooyour tooconnect konta i pobieranie hello wpisy dziennika JSON dla dziennikami sondy kondycji i zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="30b4d-162">You need tooconnect tooyour storage account and retrieve hello JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="30b4d-163">Po pobraniu hello pliki w formacie JSON można konwertować tooCSV i widoku w programie Excel, usłudze PowerBI lub inne narzędzie do wizualizacji danych.</span><span class="sxs-lookup"><span data-stu-id="30b4d-163">Once you download hello JSON files, you can convert them tooCSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="30b4d-164">Jeśli znasz podstawowe koncepcje zmiany wartości stałych i zmiennych w języku C# i Visual Studio, możesz użyć hello [dziennika narzędzia konwertera](https://github.com/Azure-Samples/networking-dotnet-log-converter) dostępne w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="30b4d-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="30b4d-165">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="30b4d-165">Additional resources</span></span>

* <span data-ttu-id="30b4d-166">[Wizualizuj dzienników inspekcji Azure przy użyciu usługi Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) wpis w blogu.</span><span class="sxs-lookup"><span data-stu-id="30b4d-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="30b4d-167">[Wyświetlanie i analizowanie dzienników inspekcji platformy Azure w usłudze Power BI i nie tylko](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) wpis w blogu.</span><span class="sxs-lookup"><span data-stu-id="30b4d-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30b4d-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="30b4d-168">Next steps</span></span>

[<span data-ttu-id="30b4d-169">Opis sond modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="30b4d-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
