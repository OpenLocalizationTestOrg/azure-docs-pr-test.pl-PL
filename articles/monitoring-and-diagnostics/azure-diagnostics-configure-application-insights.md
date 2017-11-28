---
title: aaaConfigure diagnostyki Azure toosend danych tooApplication Insights | Dokumentacja firmy Microsoft
description: "Zaktualizuj hello Azure Diagnostics publicznej konfiguracji toosend danych tooApplication szczegółowych informacji."
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
ms.openlocfilehash: 7c36f29da8fdc12fa58c17458348a311b900b0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a><span data-ttu-id="cb89c-103">Usługi w chmurze maszyny wirtualnej i sieci szkieletowej usług danych diagnostycznych tooApplication Insights wysyłania</span><span class="sxs-lookup"><span data-stu-id="cb89c-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data tooApplication Insights</span></span>
<span data-ttu-id="cb89c-104">Usługi w chmurze, maszyn wirtualnych, zestawy skalowania maszyny wirtualnej i sieci szkieletowej usług wszystkich Użyj hello Azure Diagnostics rozszerzenia toocollect danych.</span><span class="sxs-lookup"><span data-stu-id="cb89c-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use hello Azure Diagnostics extension toocollect data.</span></span>  <span data-ttu-id="cb89c-105">Diagnostyka Azure wysyła tooAzure danych magazynu tabel.</span><span class="sxs-lookup"><span data-stu-id="cb89c-105">Azure diagnostics sends data tooAzure Storage tables.</span></span>  <span data-ttu-id="cb89c-106">Można jednak również potoku wszystkie lub podzbiór lokalizacje tooother danych hello przy użyciu rozszerzenia diagnostyki Azure w wersji 1.5 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="cb89c-106">However, you can also pipe all or a subset of hello data tooother locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="cb89c-107">W tym artykule opisano, jak dane toosend z hello Azure Diagnostics rozszerzenia tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="cb89c-107">This article describes how toosend data from hello Azure Diagnostics extension tooApplication Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="cb89c-108">Wyjaśniono konfiguracji diagnostyki</span><span class="sxs-lookup"><span data-stu-id="cb89c-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="cb89c-109">wychwytywanie rozszerzenia 1.5 wprowadzone diagnostyki Azure Hello, które są dodatkowe lokalizacje, w którym może wysyłać dane diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="cb89c-109">hello Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="cb89c-110">Przykład konfiguracji zbiorniku dla usługi Application Insights:</span><span class="sxs-lookup"><span data-stu-id="cb89c-110">Example configuration of a sink for Application Insights:</span></span>

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
- <span data-ttu-id="cb89c-111">Witaj **zbiornika** *nazwa* atrybut jest wartość ciągu, który unikatowo identyfikuje zbiornika hello.</span><span class="sxs-lookup"><span data-stu-id="cb89c-111">hello **Sink** *name* attribute is a string value that uniquely identifies hello sink.</span></span>

- <span data-ttu-id="cb89c-112">Witaj **ApplicationInsights** element określa klucz Instrumentacji hello zasobu usługi Application insights wysyłania hello dane diagnostyczne platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cb89c-112">hello **ApplicationInsights** element specifies instrumentation key of hello Application insights resource where hello Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="cb89c-113">Jeśli nie masz istniejący zasób usługi Application Insights, zobacz [utworzyć nowy zasób usługi Application Insights](../application-insights/app-insights-create-new-resource.md) Aby uzyskać więcej informacji na temat tworzenia zasobu i pobierania klucza Instrumentacji hello.</span><span class="sxs-lookup"><span data-stu-id="cb89c-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting hello instrumentation key.</span></span>
    - <span data-ttu-id="cb89c-114">Jeśli tworzysz usługi w chmurze z Azure SDK 2.8 i nowsze, ten klucz Instrumentacji jest wypełniane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="cb89c-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="cb89c-115">wartość Hello jest oparta na powitania **APPINSIGHTS_INSTRUMENTATIONKEY** ustawienie konfiguracyjne usługi podczas pakowania hello projektu usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="cb89c-115">hello value is based on hello **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging hello Cloud Service project.</span></span> <span data-ttu-id="cb89c-116">Zobacz [wystawia usługi w chmurze Użyj usługi Application Insights z diagnostyki Azure tootroubleshoot](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span><span class="sxs-lookup"><span data-stu-id="cb89c-116">See [Use Application Insights with Azure Diagnostics tootroubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="cb89c-117">Witaj **kanałów** elementu zawiera jeden lub więcej **kanału** elementów.</span><span class="sxs-lookup"><span data-stu-id="cb89c-117">hello **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="cb89c-118">Witaj *nazwa* jednoznacznie odnosi się toothat kanału.</span><span class="sxs-lookup"><span data-stu-id="cb89c-118">hello *name* attribute uniquely refers toothat channel.</span></span>
    - <span data-ttu-id="cb89c-119">Witaj *loglevel* atrybutu pozwala określić umożliwia hello poziom dziennika, który hello kanału.</span><span class="sxs-lookup"><span data-stu-id="cb89c-119">hello *loglevel* attribute lets you specify hello log level that hello channel allows.</span></span> <span data-ttu-id="cb89c-120">poziomy rejestrowania dostępne Hello w kolejności większość informacji tooleast są:</span><span class="sxs-lookup"><span data-stu-id="cb89c-120">hello available log levels in order of most tooleast information are:</span></span>
        - <span data-ttu-id="cb89c-121">Pełne</span><span class="sxs-lookup"><span data-stu-id="cb89c-121">Verbose</span></span>
        - <span data-ttu-id="cb89c-122">Informacje</span><span class="sxs-lookup"><span data-stu-id="cb89c-122">Information</span></span>
        - <span data-ttu-id="cb89c-123">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="cb89c-123">Warning</span></span>
        - <span data-ttu-id="cb89c-124">Błąd</span><span class="sxs-lookup"><span data-stu-id="cb89c-124">Error</span></span>
        - <span data-ttu-id="cb89c-125">Krytyczne</span><span class="sxs-lookup"><span data-stu-id="cb89c-125">Critical</span></span>

<span data-ttu-id="cb89c-126">Kanał działa jak filtr i pozwala określonego dziennika tooselect poziomy toohello toosend docelowej obiekt sink.</span><span class="sxs-lookup"><span data-stu-id="cb89c-126">A channel acts like a filter and allows you tooselect specific log levels toosend toohello target sink.</span></span> <span data-ttu-id="cb89c-127">Można na przykład zbierania pełnych dzienników i wysyłać je toostorage, ale wysłać tylko błędy toohello ujścia.</span><span class="sxs-lookup"><span data-stu-id="cb89c-127">For example, you could collect verbose logs and send them toostorage, but send only Errors toohello sink.</span></span>

<span data-ttu-id="cb89c-128">Witaj poniższy rysunek przedstawia tę relację.</span><span class="sxs-lookup"><span data-stu-id="cb89c-128">hello following graphic shows this relationship.</span></span>

![Publiczna Konfiguracja diagnostyki](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="cb89c-130">powitania po grafiki znajduje się podsumowanie wartości konfiguracji hello i jak działają.</span><span class="sxs-lookup"><span data-stu-id="cb89c-130">hello following graphic summarizes hello configuration values and how they work.</span></span> <span data-ttu-id="cb89c-131">W konfiguracji hello na różnych poziomach hierarchii hello może zawierać wiele wychwytywanie.</span><span class="sxs-lookup"><span data-stu-id="cb89c-131">You can include multiple sinks in hello configuration at different levels in hello hierarchy.</span></span> <span data-ttu-id="cb89c-132">zbiornik Hello na najwyższym poziomie hello działa jako ustawienie globalne i hello jeden określony w poszczególnych hello element działa jak ustawienie globalne toothat do zastąpienia.</span><span class="sxs-lookup"><span data-stu-id="cb89c-132">hello sink at hello top level acts as a global setting and hello one specified at hello individual element acts like an override toothat global setting.</span></span>

![Diagnostyka wychwytywanie konfiguracji z usługą Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="cb89c-134">Przykład konfiguracji zbiornika ukończone</span><span class="sxs-lookup"><span data-stu-id="cb89c-134">Complete sink configuration example</span></span>
<span data-ttu-id="cb89c-135">W tym miejscu jest kompletnym przykładem hello publicznej konfiguracji pliku</span><span class="sxs-lookup"><span data-stu-id="cb89c-135">Here is a complete example of hello public configuration file that</span></span>
1. <span data-ttu-id="cb89c-136">wysyła wszystkie błędy tooApplication Insights (określone na powitania **DiagnosticMonitorConfiguration** węzła)</span><span class="sxs-lookup"><span data-stu-id="cb89c-136">sends all errors tooApplication Insights (specified at hello **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="cb89c-137">wysyła również pełne poziomu dzienniki hello Dzienniki aplikacji (określone na powitania **dzienniki** węzła).</span><span class="sxs-lookup"><span data-stu-id="cb89c-137">also sends Verbose level logs for hello Application Logs (specified at hello **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent toothis channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent toothis channel -->
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
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent toothis channel",
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
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent toothis channel"
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
<span data-ttu-id="cb89c-138">W poprzedniej konfiguracji hello hello następujące wiersze mają następujące znaczenie hello:</span><span class="sxs-lookup"><span data-stu-id="cb89c-138">In hello previous configuration, hello following lines have hello following meanings:</span></span>

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="cb89c-139">Wyślij wszystkie dane hello, które jest zbieranych przez Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="cb89c-139">Send all hello data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a><span data-ttu-id="cb89c-140">Wyślij tylko błąd dzienniki toohello usługi Application Insights odbioru</span><span class="sxs-lookup"><span data-stu-id="cb89c-140">Send only error logs toohello Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a><span data-ttu-id="cb89c-141">Wyślij dzienniki pełne application tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="cb89c-141">Send Verbose application logs tooApplication Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="cb89c-142">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="cb89c-142">Limitations</span></span>

- <span data-ttu-id="cb89c-143">**Kanały zalogować się wyłącznie liczniki wydajności nie i typu.**</span><span class="sxs-lookup"><span data-stu-id="cb89c-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="cb89c-144">Jeśli określisz kanał z elementem licznika wydajności jest ignorowana.</span><span class="sxs-lookup"><span data-stu-id="cb89c-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="cb89c-145">**poziom dziennika Hello kanału nie może przekraczać hello poziom dziennika co zbieranych przez diagnostycznych platformy Azure.**</span><span class="sxs-lookup"><span data-stu-id="cb89c-145">**hello log level for a channel cannot exceed hello log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="cb89c-146">Na przykład nie można gromadzić błędy w dzienniku aplikacji w elemencie dzienniki hello i spróbuj toosend pełne dzienniki toohello szczegółowe informacje o aplikacji ujścia.</span><span class="sxs-lookup"><span data-stu-id="cb89c-146">For example, you cannot collect Application Log errors in hello Logs element and try toosend Verbose logs toohello Application Insight sink.</span></span> <span data-ttu-id="cb89c-147">Witaj *scheduledTransferLogLevelFilter* atrybutów zawsze należy zebrać takie same lub więcej dzienników niż hello loguje użytkownika próbujesz toosend tooa ujścia.</span><span class="sxs-lookup"><span data-stu-id="cb89c-147">hello *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than hello logs you are trying toosend tooa sink.</span></span>
- <span data-ttu-id="cb89c-148">**Nie można wysłać obiektu blob danych zbieranych przez tooApplication rozszerzenia diagnostyki Azure szczegółowych informacji.**</span><span class="sxs-lookup"><span data-stu-id="cb89c-148">**You cannot send blob data collected by Azure diagnostics extension tooApplication Insights.**</span></span> <span data-ttu-id="cb89c-149">Na przykład niczego określone w obszarze hello *katalogów* węzła.</span><span class="sxs-lookup"><span data-stu-id="cb89c-149">For example, anything specified under hello *Directories* node.</span></span> <span data-ttu-id="cb89c-150">Zrzuty awaryjne zrzutu awaryjnego rzeczywiste hello są wysyłane tooblob magazynu i został wygenerowany tylko powiadomienie, które hello zrzutu awaryjnego są wysyłane tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="cb89c-150">For Crash Dumps hello actual crash dump is sent tooblob storage and only a notification that hello crash dump was generated is sent tooApplication Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb89c-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cb89c-151">Next Steps</span></span>
* <span data-ttu-id="cb89c-152">Dowiedz się, jak za[wyświetlania informacji diagnostycznych platformy Azure](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) w usłudze Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cb89c-152">Learn how too[view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="cb89c-153">Użyj [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello rozszerzenia diagnostyki Azure dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb89c-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="cb89c-154">Użyj [programu Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello rozszerzenia diagnostyki Azure dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="cb89c-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello Azure diagnostics extension for your application</span></span>
