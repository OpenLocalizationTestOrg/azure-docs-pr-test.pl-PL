---
title: "Skonfiguruj diagnostyki Azure w celu wysyłania danych do usługi Application Insights | Dokumentacja firmy Microsoft"
description: "Zaktualizuj konfigurację publicznego diagnostyki Azure do przesyłania danych do usługi Application Insights."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: f9e12c3e-c307-435e-a149-ef0fef20513a
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2016
ms.author: robb
ms.openlocfilehash: 67dc2d5bbfa2012e4e098616edda593d023c4c1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-to-application-insights"></a><span data-ttu-id="c3cc5-103">Wyślij dane diagnostyczne usługi w chmurze maszyny wirtualnej i sieci szkieletowej usług do usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="c3cc5-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data to Application Insights</span></span>
<span data-ttu-id="c3cc5-104">Usługi w chmurze, maszyn wirtualnych, zestawy skalowania maszyny wirtualnej i sieci szkieletowej usług wszystkie używane rozszerzenie diagnostyki Azure do zbierania danych.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use the Azure Diagnostics extension to collect data.</span></span>  <span data-ttu-id="c3cc5-105">Diagnostyka Azure wysyła dane do tabel usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-105">Azure diagnostics sends data to Azure Storage tables.</span></span>  <span data-ttu-id="c3cc5-106">Można jednak również potoku wszystkie lub podzbiór danych do innych lokalizacji przy użyciu rozszerzenia diagnostyki Azure w wersji 1.5 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-106">However, you can also pipe all or a subset of the data to other locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="c3cc5-107">W tym artykule opisano sposób wysyłania danych z rozszerzenia diagnostyki Azure do usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-107">This article describes how to send data from the Azure Diagnostics extension to Application Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="c3cc5-108">Wyjaśniono konfiguracji diagnostyki</span><span class="sxs-lookup"><span data-stu-id="c3cc5-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="c3cc5-109">Wychwytywanie rozszerzenia diagnostyki Azure w wersji 1.5 wprowadzono, które są dodatkowe lokalizacje, w którym może wysyłać dane diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-109">The Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="c3cc5-110">Przykład konfiguracji zbiorniku dla usługi Application Insights:</span><span class="sxs-lookup"><span data-stu-id="c3cc5-110">Example configuration of a sink for Application Insights:</span></span>

```XML
<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "ApplicationInsights",
            "ApplicationInsights": "{Insert InstrumentationKey}",
            "Channels": {
                "Channel": [
                    {
                        "logLevel": "Error",
                        "name": "MyTopDiagData"
                    },
                    {
                        "logLevel": "Error",
                        "name": "MyLogData"
                    }
                ]
            }
        }
    ]
}
```
- <span data-ttu-id="c3cc5-111">**Zbiornika** *nazwa* atrybut jest wartość ciągu, który unikatowo identyfikuje obiekt sink.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-111">The **Sink** *name* attribute is a string value that uniquely identifies the sink.</span></span>

- <span data-ttu-id="c3cc5-112">**ApplicationInsights** element określa klucz Instrumentacji zasobu usługi Application insights wysyłania danych diagnostycznych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-112">The **ApplicationInsights** element specifies instrumentation key of the Application insights resource where the Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="c3cc5-113">Jeśli nie masz istniejący zasób usługi Application Insights, zobacz [utworzyć nowy zasób usługi Application Insights](../application-insights/app-insights-create-new-resource.md) Aby uzyskać więcej informacji na temat tworzenia zasobu i pobierania klucza instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting the instrumentation key.</span></span>
    - <span data-ttu-id="c3cc5-114">Jeśli tworzysz usługi w chmurze z Azure SDK 2.8 i nowsze, ten klucz Instrumentacji jest wypełniane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="c3cc5-115">Wartość na podstawie **APPINSIGHTS_INSTRUMENTATIONKEY** ustawienie konfiguracyjne usługi podczas pakowania projektu usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-115">The value is based on the **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging the Cloud Service project.</span></span> <span data-ttu-id="c3cc5-116">Zobacz [użycia usługi Application Insights z diagnostyki Azure rozwiązywać problemy z usługą w chmurze](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span><span class="sxs-lookup"><span data-stu-id="c3cc5-116">See [Use Application Insights with Azure Diagnostics to troubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="c3cc5-117">**Kanałów** elementu zawiera jeden lub więcej **kanału** elementów.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-117">The **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="c3cc5-118">*Nazwa* jednoznacznie odnosi się do tego kanału.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-118">The *name* attribute uniquely refers to that channel.</span></span>
    - <span data-ttu-id="c3cc5-119">*Loglevel* atrybutu pozwala określić poziom dziennika, który umożliwia kanału.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-119">The *loglevel* attribute lets you specify the log level that the channel allows.</span></span> <span data-ttu-id="c3cc5-120">Dostępne są następujące poziomy rejestrowania dostępne w kolejności od najbardziej do najmniej informacji:</span><span class="sxs-lookup"><span data-stu-id="c3cc5-120">The available log levels in order of most to least information are:</span></span>
        - <span data-ttu-id="c3cc5-121">Pełne</span><span class="sxs-lookup"><span data-stu-id="c3cc5-121">Verbose</span></span>
        - <span data-ttu-id="c3cc5-122">Informacje</span><span class="sxs-lookup"><span data-stu-id="c3cc5-122">Information</span></span>
        - <span data-ttu-id="c3cc5-123">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="c3cc5-123">Warning</span></span>
        - <span data-ttu-id="c3cc5-124">Błąd</span><span class="sxs-lookup"><span data-stu-id="c3cc5-124">Error</span></span>
        - <span data-ttu-id="c3cc5-125">Krytyczne</span><span class="sxs-lookup"><span data-stu-id="c3cc5-125">Critical</span></span>

<span data-ttu-id="c3cc5-126">Kanał działa jak filtr i służy do wybierania określonego dziennika poziomów do wysłania do docelowej obiekt sink.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-126">A channel acts like a filter and allows you to select specific log levels to send to the target sink.</span></span> <span data-ttu-id="c3cc5-127">Na przykład można zebrać dzienniki pełne i wysyłać je do magazynu, ale tylko błędy wysyłania do ujścia.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-127">For example, you could collect verbose logs and send them to storage, but send only Errors to the sink.</span></span>

<span data-ttu-id="c3cc5-128">Opisywaną relację przedstawiono na poniższym rysunku.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-128">The following graphic shows this relationship.</span></span>

![Publiczna Konfiguracja diagnostyki](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="c3cc5-130">Na rysunku poniżej przedstawiono wartości konfiguracji i jak działają.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-130">The following graphic summarizes the configuration values and how they work.</span></span> <span data-ttu-id="c3cc5-131">Wychwytywanie wielu można uwzględnić w konfiguracji na różnych poziomach hierarchii.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-131">You can include multiple sinks in the configuration at different levels in the hierarchy.</span></span> <span data-ttu-id="c3cc5-132">Obiekt sink na najwyższym poziomie działa jako ustawienie globalne, określony w elemencie poszczególnych działa jak zastąpienie tego ustawienia globalnego.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-132">The sink at the top level acts as a global setting and the one specified at the individual element acts like an override to that global setting.</span></span>

![Diagnostyka wychwytywanie konfiguracji z usługą Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="c3cc5-134">Przykład konfiguracji zbiornika ukończone</span><span class="sxs-lookup"><span data-stu-id="c3cc5-134">Complete sink configuration example</span></span>
<span data-ttu-id="c3cc5-135">W tym miejscu jest kompletnym przykładem publicznej konfiguracji pliku</span><span class="sxs-lookup"><span data-stu-id="c3cc5-135">Here is a complete example of the public configuration file that</span></span>
1. <span data-ttu-id="c3cc5-136">wysyła wszystkie błędy do usługi Application Insights (określony w **DiagnosticMonitorConfiguration** węzła)</span><span class="sxs-lookup"><span data-stu-id="c3cc5-136">sends all errors to Application Insights (specified at the **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="c3cc5-137">wysyła również dzienniki poziomu Verbose dzienników aplikacji (określony w **dzienniki** węzła).</span><span class="sxs-lookup"><span data-stu-id="c3cc5-137">also sends Verbose level logs for the Application Logs (specified at the **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent to this channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent to this channel -->
  </DiagnosticMonitorConfiguration>

<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
  </SinksConfig>
</WadCfg>
```
```JSON
"WadCfg": {
    "DiagnosticMonitorConfiguration": {
        "overallQuotaInMB": 4096,
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent to this channel",
        "DiagnosticInfrastructureLogs": {
        },
        "PerformanceCounters": {
            "PerformanceCounterConfiguration": [
                {
                    "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                    "sampleRate": "PT3M"
                },
                {
                    "counterSpecifier": "\\Memory\\Available MBytes",
                    "sampleRate": "PT3M"
                }
            ]
        },
        "WindowsEventLog": {
            "scheduledTransferPeriod": "PT1M",
            "DataSource": [
                {
                    "name": "Application!*"
                }
            ]
        },
        "Logs": {
            "scheduledTransferPeriod": "PT1M",
            "scheduledTransferLogLevelFilter": "Verbose",
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent to this channel"
        }
    },
    "SinksConfig": {
        "Sink": [
            {
                "name": "ApplicationInsights",
                "ApplicationInsights": "{Insert InstrumentationKey}",
                "Channels": {
                    "Channel": [
                        {
                            "logLevel": "Error",
                            "name": "MyTopDiagData"
                        },
                        {
                            "logLevel": "Verbose",
                            "name": "MyLogData"
                        }
                    ]
                }
            }
        ]
    }
}
```
<span data-ttu-id="c3cc5-138">W poprzedniej konfiguracji następujące wiersze mają następujące znaczenie:</span><span class="sxs-lookup"><span data-stu-id="c3cc5-138">In the previous configuration, the following lines have the following meanings:</span></span>

### <a name="send-all-the-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="c3cc5-139">Wyślij wszystkie dane, które jest zbieranych przez Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="c3cc5-139">Send all the data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-to-the-application-insights-sink"></a><span data-ttu-id="c3cc5-140">Wyślij tylko dzienniki błędów do ujścia usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="c3cc5-140">Send only error logs to the Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-to-application-insights"></a><span data-ttu-id="c3cc5-141">Wysyłanie dzienników pełne aplikacji do usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="c3cc5-141">Send Verbose application logs to Application Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="c3cc5-142">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="c3cc5-142">Limitations</span></span>

- <span data-ttu-id="c3cc5-143">**Kanały zalogować się wyłącznie liczniki wydajności nie i typu.**</span><span class="sxs-lookup"><span data-stu-id="c3cc5-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="c3cc5-144">Jeśli określisz kanał z elementem licznika wydajności jest ignorowana.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="c3cc5-145">**Poziom dziennika dla kanału nie może przekraczać poziom dziennika co zbieranych przez diagnostycznych platformy Azure.**</span><span class="sxs-lookup"><span data-stu-id="c3cc5-145">**The log level for a channel cannot exceed the log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="c3cc5-146">Na przykład nie można gromadzić błędy w dzienniku aplikacji w elemencie dzienniki i spróbuj wysłać pełne dzienniki do ujścia szczegółowe informacje o aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-146">For example, you cannot collect Application Log errors in the Logs element and try to send Verbose logs to the Application Insight sink.</span></span> <span data-ttu-id="c3cc5-147">*ScheduledTransferLogLevelFilter* atrybutów zawsze należy zebrać takie same lub więcej dzienników niż dzienniki chcesz wysyłać do ujścia.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-147">The *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than the logs you are trying to send to a sink.</span></span>
- <span data-ttu-id="c3cc5-148">**Nie można wysłać danych obiektów blob zbierane przez rozszerzenie diagnostyki Azure do usługi Application Insights.**</span><span class="sxs-lookup"><span data-stu-id="c3cc5-148">**You cannot send blob data collected by Azure diagnostics extension to Application Insights.**</span></span> <span data-ttu-id="c3cc5-149">Na przykład niczego określone w obszarze *katalogów* węzła.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-149">For example, anything specified under the *Directories* node.</span></span> <span data-ttu-id="c3cc5-150">Dla zrzuty awaryjne zrzutu awaryjnego rzeczywiste są wysyłane do magazynu obiektów blob i tylko wygenerowano zrzutu awaryjnego powiadomienie jest wysyłane do usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-150">For Crash Dumps the actual crash dump is sent to blob storage and only a notification that the crash dump was generated is sent to Application Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3cc5-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c3cc5-151">Next Steps</span></span>
* <span data-ttu-id="c3cc5-152">Dowiedz się, jak [wyświetlania informacji diagnostycznych platformy Azure](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) w usłudze Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-152">Learn how to [view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="c3cc5-153">Użyj [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) można włączyć rozszerzenia diagnostyki Azure dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c3cc5-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) to enable the Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="c3cc5-154">Użyj [programu Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) można włączyć rozszerzenia diagnostyki Azure dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="c3cc5-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) to enable the Azure diagnostics extension for your application</span></span>
