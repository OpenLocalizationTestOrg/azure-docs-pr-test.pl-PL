---
title: "aaaStream tooan dzienników diagnostycznych platformy Azure Event Hubs Namespace | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toostream Azure diagnostycznych dzienników tooan centra zdarzeń w przestrzeni nazw."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 42bc4845-c564-4568-b72d-0614591ebd80
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: 00092ea8f3fe4fa1476e3a697bf1e8645dd21e6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a><span data-ttu-id="4b670-103">Strumień dzienników diagnostycznych platformy Azure tooan Namespace centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="4b670-103">Stream Azure Diagnostic Logs tooan Event Hubs Namespace</span></span>
<span data-ttu-id="4b670-104">**[Azure dzienników diagnostycznych](monitoring-overview-of-diagnostic-logs.md)**  mogła być przesłana strumieniowo w pobliżu aplikacji tooany czasu rzeczywistego przy użyciu hello wbudowanych "Eksportuj koncentratory tooEvent" opcji w portalu hello lub przez włączenie hello identyfikator reguły magistrali usług w ustawienie diagnostyczne za pośrednictwem hello Azure PowerShell Polecenia cmdlet lub Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4b670-104">**[Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time tooany application using hello built-in “Export tooEvent Hubs” option in hello Portal, or by enabling hello Service Bus Rule ID in a diagnostic setting via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a><span data-ttu-id="4b670-105">Co można zrobić z dzienników diagnostyki i usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="4b670-105">What you can do with diagnostics logs and Event Hubs</span></span>
<span data-ttu-id="4b670-106">Poniżej przedstawiono kilka sposobów może używać hello przesyłanie strumieniowe możliwości do dzienników diagnostycznych:</span><span class="sxs-lookup"><span data-stu-id="4b670-106">Here are just a few ways you might use hello streaming capability for Diagnostic Logs:</span></span>

* <span data-ttu-id="4b670-107">**Strumień rejestruje systemów firm too3rd rejestrowania i dane telemetryczne** — wraz z upływem czasu przesyłania strumieniowego usługi Event Hubs ma zostać toopipe mechanizmu hello dzienników diagnostycznych w rozwiązań Siem toothird firm a dziennika rozwiązań analitycznych.</span><span class="sxs-lookup"><span data-stu-id="4b670-107">**Stream logs too3rd party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your diagnostic logs in toothird-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="4b670-108">**Wyświetlić kondycję usługi przesyłania strumieniowego "aktywnej ścieżki" tooPowerBI danych** — za pomocą usługi Event Hubs, Stream Analytics i usługi Power BI, dane diagnostyki toonear wgląd w czasie rzeczywistym mogą łatwo przekształcić na usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="4b670-108">**View service health by streaming “hot path” data tooPowerBI** – Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your diagnostics data in toonear real-time insights on your Azure services.</span></span> <span data-ttu-id="4b670-109">[Ten artykuł dokumentacja zawiera wszechstronne omówienie sposobu przetwarzania danych za pomocą usługi Stream Analytics tooset się usługi Event Hubs i używać usługi Power BI jako dane wyjściowe](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="4b670-109">[This documentation article gives a great overview of how tooset up Event Hubs, process data with Stream Analytics, and use PowerBI as an output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="4b670-110">Oto kilka porad dotyczących uzyskiwania skonfigurowany z dzienników diagnostycznych:</span><span class="sxs-lookup"><span data-stu-id="4b670-110">Here are a few tips for getting set up with diagnostic logs:</span></span>
  
  * <span data-ttu-id="4b670-111">Centrum zdarzeń dla kategorii dzienników diagnostycznych jest tworzona automatycznie podczas sprawdzania hello opcji w portalu hello lub włączyć za pomocą programu PowerShell, więc chcesz Centrum zdarzeń hello tooselect w hello nazw o nazwie hello rozpoczyna się od **insights**.</span><span class="sxs-lookup"><span data-stu-id="4b670-111">An event hub for a category of diagnostic logs is created automatically when you check hello option in hello portal or enable it through PowerShell, so you want tooselect hello event hub in hello namespace with hello name that starts with **insights-**.</span></span>
  * <span data-ttu-id="4b670-112">Przykładowe Stream Analytics jest Hello następującego kodu SQL kwerendy, której można tooparse wszystkie dane dziennika hello tabeli tooa usługi Power BI:</span><span class="sxs-lookup"><span data-stu-id="4b670-112">hello following SQL code is a sample Stream Analytics query that you can use tooparse all hello log data in tooa PowerBI table:</span></span>

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* <span data-ttu-id="4b670-113">**Tworzenie niestandardowych telemetrii i rejestrowanie platformy** — Jeśli masz już platformy telemetrii niestandardowej lub są po prostu pomyśleć o budynku jedną hello skalowalnej publikowania / subskrypcji rodzaj usługi Event Hubs umożliwia tooflexibly pozyskiwania diagnostycznych dzienniki.</span><span class="sxs-lookup"><span data-stu-id="4b670-113">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest diagnostic logs.</span></span> <span data-ttu-id="4b670-114">[Zobacz Dan Rosanova przewodnik toousing centra zdarzeń w skali globalnej platformy telemetrii tutaj](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="4b670-114">[See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="enable-streaming-of-diagnostic-logs"></a><span data-ttu-id="4b670-115">Przesyłania strumieniowego dzienników diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="4b670-115">Enable streaming of diagnostic logs</span></span>
<span data-ttu-id="4b670-116">Można włączyć przesyłania strumieniowego dzienników diagnostycznych programowo, za pośrednictwem portalu hello, lub za pomocą hello [interfejsów API REST Monitor Azure](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span><span class="sxs-lookup"><span data-stu-id="4b670-116">You can enable streaming of diagnostic logs programmatically, via hello portal, or using hello [Azure Monitor REST APIs](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span></span> <span data-ttu-id="4b670-117">W obu przypadkach należy utworzyć ustawienie diagnostyczne z określonymi przestrzeni nazw usługi Event Hubs i hello dziennika kategorii i metryki ma toosend w toohello przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="4b670-117">Either way, you create a diagnostic setting in which you specify an Event Hubs namespace and hello log categories and metrics you want toosend in toohello namespace.</span></span> <span data-ttu-id="4b670-118">Centrum zdarzeń jest tworzony w przestrzeni nazw powitania dla każdej kategorii dziennika, który zostanie włączone.</span><span class="sxs-lookup"><span data-stu-id="4b670-118">An event hub is created in hello namespace for each log category you enable.</span></span> <span data-ttu-id="4b670-119">Diagnostyka **kategorii dziennika** jest typem dziennika, który może zbierać zasobu.</span><span class="sxs-lookup"><span data-stu-id="4b670-119">A diagnostic **log category** is a type of log that a resource may collect.</span></span>

> [!WARNING]
> <span data-ttu-id="4b670-120">Włączanie i przesyłania strumieniowego dzienników diagnostycznych z zasobów obliczeniowych (na przykład maszyny wirtualne lub sieci szkieletowej usług) [wymaga innego zestawu kroków](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span><span class="sxs-lookup"><span data-stu-id="4b670-120">Enabling and streaming diagnostic logs from Compute resources (for example, VMs or Service Fabric) [requires a different set of steps](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span></span>
> 
> 

<span data-ttu-id="4b670-121">Hello usługi Service Bus lub Event Hubs w przestrzeni nazw nie ma toobe hello tej samej subskrypcji co zasób hello emitowanie dzienniki tak długo, jak hello użytkownik, który konfiguruje ustawienia hello ma odpowiednie RBAC dostępu tooboth subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4b670-121">hello Service Bus or Event Hubs namespace does not have toobe in hello same subscription as hello resource emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="stream-diagnostic-logs-using-hello-portal"></a><span data-ttu-id="4b670-122">Strumieniowe przesyłanie dzienników diagnostycznych za pomocą portalu hello</span><span class="sxs-lookup"><span data-stu-id="4b670-122">Stream diagnostic logs using hello portal</span></span>
1. <span data-ttu-id="4b670-123">W portalu hello Przejdź tooAzure monitora, a następnie kliknij **ustawień diagnostycznych**</span><span class="sxs-lookup"><span data-stu-id="4b670-123">In hello portal, navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Monitorowanie sekcji Azure Monitor](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. <span data-ttu-id="4b670-125">Opcjonalnie Filtruj listę hello według grupy zasobów lub typ zasobu, a następnie kliknij na powitania zasobu, dla którego chcesz tooset ustawienie diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="4b670-125">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="4b670-126">Jeśli nie istnieją żadne ustawienia na powitania zasobów, wybrana przez Ciebie, jesteś toocreate zostanie wyświetlony monit o ustawienie.</span><span class="sxs-lookup"><span data-stu-id="4b670-126">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="4b670-127">Kliknij pozycję "Włącz diagnostykę."</span><span class="sxs-lookup"><span data-stu-id="4b670-127">Click "Turn on diagnostics."</span></span>

   ![Dodaj ustawienie diagnostyczne - żadnych istniejących ustawień](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   <span data-ttu-id="4b670-129">W przypadku ustawienia istniejące na powitania zasobów, zostanie wyświetlona lista ustawień już skonfigurowana dla tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="4b670-129">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="4b670-130">Kliknij przycisk "Dodaj ustawienie diagnostyczne".</span><span class="sxs-lookup"><span data-stu-id="4b670-130">Click "Add diagnostic setting."</span></span>

   ![Dodaj ustawienie diagnostyczne — istniejące ustawienia](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="4b670-132">Nadaj nazwę ustawienia i sprawdź pole hello **Centrum zdarzeń tooan strumienia**, następnie wybierz obszar nazw usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="4b670-132">Give your setting a name and check hello box for **Stream tooan event hub**, then select an Event Hubs namespace.</span></span>
   
   ![Dodaj ustawienie diagnostyczne — istniejące ustawienia](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   <span data-ttu-id="4b670-134">Hello wybrane przestrzeni nazw będzie gdzie (jeżeli jest to pierwsza przesyłania strumieniowego dzienników diagnostycznych) lub zbyt strumieniowo hello Centrum zdarzeń (jeśli istnieje już zasobów, które są przesyłania strumieniowego tej przestrzeni nazw toothis kategorii dziennika), i hello zasady określają hello uprawnienia, które ma hello mechanizm przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="4b670-134">hello namespace selected will be where hello event hub is created (if this is your first time streaming diagnostic logs) or streamed too(if there are already resources that are streaming that log category toothis namespace), and hello policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="4b670-135">Obecnie przesyłania strumieniowego tooan Centrum zdarzeń wymaga uprawnienia Zarządzanie, wysyłania i nasłuchiwania.</span><span class="sxs-lookup"><span data-stu-id="4b670-135">Today, streaming tooan event hub requires Manage, Send, and Listen permissions.</span></span> <span data-ttu-id="4b670-136">Można utworzyć lub zmodyfikować zasady dostępu przestrzeń nazw udostępnionych centra zdarzeń w portalu hello karcie Konfigurowanie hello przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="4b670-136">You can create or modify Event Hubs namespace shared access policies in hello portal under hello Configure tab for your namespace.</span></span> <span data-ttu-id="4b670-137">tooupdate, jeden z tych ustawień diagnostycznych powitania klienta musi mieć uprawnienie ListKey hello na reguły autoryzacji hello usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="4b670-137">tooupdate one of these diagnostic settings, hello client must have hello ListKey permission on hello Event Hubs authorization rule.</span></span>

4. <span data-ttu-id="4b670-138">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4b670-138">Click **Save**.</span></span>

<span data-ttu-id="4b670-139">Po kilku chwilach hello nowe ustawienie jest wyświetlane na liście ustawień dla tego zasobu, a dzienników diagnostycznych są przesyłane strumieniowo toothat konta magazynu, natychmiast po wygenerowaniu nowych danych zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="4b670-139">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are streamed toothat storage account as soon as new event data is generated.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="4b670-140">Za pomocą poleceń cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b670-140">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="4b670-141">tooenable przesyłania strumieniowego za pośrednictwem hello [polecenia cmdlet programu PowerShell usługi Azure](insights-powershell-samples.md), można użyć hello `Set-AzureRmDiagnosticSetting` polecenia cmdlet z następującymi parametrami:</span><span class="sxs-lookup"><span data-stu-id="4b670-141">tooenable streaming via hello [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use hello `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

<span data-ttu-id="4b670-142">Hello identyfikator reguły magistrali usług to ciąg w formacie: `{Service Bus resource ID}/authorizationrules/{key name}`, na przykład `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="4b670-142">hello Service Bus Rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`, for example, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span></span>

### <a name="via-azure-cli"></a><span data-ttu-id="4b670-143">Za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4b670-143">Via Azure CLI</span></span>
<span data-ttu-id="4b670-144">tooenable przesyłania strumieniowego za pośrednictwem hello [interfejsu wiersza polecenia Azure](insights-cli-samples.md), można użyć hello `insights diagnostic set` polecenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4b670-144">tooenable streaming via hello [Azure CLI](insights-cli-samples.md), you can use hello `insights diagnostic set` command like this:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

<span data-ttu-id="4b670-145">Użyj hello sam format identyfikator reguły magistrali usługi zgodnie z objaśnieniem dla hello polecenia Cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b670-145">Use hello same format for Service Bus Rule ID as explained for hello PowerShell Cmdlet.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="4b670-146">Jak korzystać z hello danych dziennika z usługi Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="4b670-146">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="4b670-147">Oto przykładowe dane wyjściowe dane z centrów zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="4b670-147">Here is sample output data from Event Hubs:</span></span>

```json
{
    "records": [
        {
            "time": "2016-07-15T18:00:22.6235064Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330013509921957/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Error",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T17:58:55.048482Z",
                "endTime": "2016-07-15T18:00:22.4109204Z",
                "status": "Failed",
                "code": "BadGateway",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330013509921957",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "29a9862f-969b-4c70-90c4-dfbdc814e413",
                    "clientTrackingId": "08587330013509921958"
                }
            }
        },
        {
            "time": "2016-07-15T18:01:15.7532989Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330012106702630/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionStarted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T18:01:15.5828115Z",
                "status": "Running",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330012106702630",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "042fb72c-7bd4-439e-89eb-3cf4409d429e",
                    "clientTrackingId": "08587330012106702632"
                }
            }
        }
    ]
}
```

| <span data-ttu-id="4b670-148">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="4b670-148">Element Name</span></span> | <span data-ttu-id="4b670-149">Opis</span><span class="sxs-lookup"><span data-stu-id="4b670-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b670-150">rekordy</span><span class="sxs-lookup"><span data-stu-id="4b670-150">records</span></span> |<span data-ttu-id="4b670-151">Tablica wszystkie zdarzenia dziennika, w tym ładunku.</span><span class="sxs-lookup"><span data-stu-id="4b670-151">An array of all log events in this payload.</span></span> |
| <span data-ttu-id="4b670-152">time</span><span class="sxs-lookup"><span data-stu-id="4b670-152">time</span></span> |<span data-ttu-id="4b670-153">Czas, jaką hello wystąpiło zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="4b670-153">Time at which hello event occurred.</span></span> |
| <span data-ttu-id="4b670-154">category</span><span class="sxs-lookup"><span data-stu-id="4b670-154">category</span></span> |<span data-ttu-id="4b670-155">Kategoria dziennika dla tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="4b670-155">Log category for this event.</span></span> |
| <span data-ttu-id="4b670-156">resourceId</span><span class="sxs-lookup"><span data-stu-id="4b670-156">resourceId</span></span> |<span data-ttu-id="4b670-157">Identyfikator zasobu hello zasobu, który wygenerował zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="4b670-157">Resource ID of hello resource that generated this event.</span></span> |
| <span data-ttu-id="4b670-158">operationName</span><span class="sxs-lookup"><span data-stu-id="4b670-158">operationName</span></span> |<span data-ttu-id="4b670-159">Nazwa operacji hello.</span><span class="sxs-lookup"><span data-stu-id="4b670-159">Name of hello operation.</span></span> |
| <span data-ttu-id="4b670-160">poziom</span><span class="sxs-lookup"><span data-stu-id="4b670-160">level</span></span> |<span data-ttu-id="4b670-161">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="4b670-161">Optional.</span></span> <span data-ttu-id="4b670-162">Wskazuje poziom zdarzenia dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="4b670-162">Indicates hello log event level.</span></span> |
| <span data-ttu-id="4b670-163">properties</span><span class="sxs-lookup"><span data-stu-id="4b670-163">properties</span></span> |<span data-ttu-id="4b670-164">Właściwości zdarzenia hello.</span><span class="sxs-lookup"><span data-stu-id="4b670-164">Properties of hello event.</span></span> |

<span data-ttu-id="4b670-165">Można wyświetlić listę wszystkich dostawców zasobów obsługujących przesyłania strumieniowego koncentratory tooEvent [tutaj](monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="4b670-165">You can view a list of all resource providers that support streaming tooEvent Hubs [here](monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="stream-data-from-compute-resources"></a><span data-ttu-id="4b670-166">Strumień danych z zasoby obliczeniowe</span><span class="sxs-lookup"><span data-stu-id="4b670-166">Stream data from Compute resources</span></span>
<span data-ttu-id="4b670-167">Można również przesyłania strumieniowego dzienników diagnostycznych z zasobów obliczeniowych, przy użyciu agenta Windows Azure Diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="4b670-167">You can also stream diagnostic logs from Compute resources using hello Windows Azure Diagnostics agent.</span></span> <span data-ttu-id="4b670-168">[Znajduje się w artykule](../event-hubs/event-hubs-streaming-azure-diags-data.md) jak tooset tego w górę.</span><span class="sxs-lookup"><span data-stu-id="4b670-168">[See this article](../event-hubs/event-hubs-streaming-azure-diags-data.md) for how tooset that up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b670-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4b670-169">Next steps</span></span>
* [<span data-ttu-id="4b670-170">Więcej informacji na temat dzienników diagnostycznych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4b670-170">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="4b670-171">Rozpoczynanie pracy z usługą Event Hubs</span><span class="sxs-lookup"><span data-stu-id="4b670-171">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

