---
title: "aaaStreaming danych diagnostycznych platformy Azure w ścieżce aktywnej hello za pomocą usługi Event Hubs | Dokumentacja firmy Microsoft"
description: "Konfigurowania diagnostyki Azure z usługą Event Hubs końcowy tooend, w tym wskazówki dotyczące typowych scenariuszy."
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: 
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: robb
ms.openlocfilehash: a2528ddd0688d1c23a8631e769ca016dd79e4159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a><span data-ttu-id="3ba3b-103">Strumieniowe przesyłanie danych diagnostycznych platformy Azure w ścieżce aktywnej hello za pomocą usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3ba3b-103">Streaming Azure Diagnostics data in hello hot path by using Event Hubs</span></span>
<span data-ttu-id="3ba3b-104">Diagnostyka Azure oferuje elastyczne metody toocollect metryki i loguje się z usługi w maszynach wirtualnych (VM) w chmurze i przenieść tooAzure wyniki magazynu.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-104">Azure Diagnostics provides flexible ways toocollect metrics and logs from cloud services virtual machines (VMs) and transfer results tooAzure Storage.</span></span> <span data-ttu-id="3ba3b-105">Począwszy od przedział czasu hello marca 2016 (zestaw SDK 2.9) można wysyłać toocustom diagnostyki źródeł danych i transferu danych ścieżkę aktywną w ciągu sekund za pomocą [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="3ba3b-105">Starting in hello March 2016 (SDK 2.9) time frame, you can send Diagnostics toocustom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="3ba3b-106">Obsługiwane typy danych obejmują:</span><span class="sxs-lookup"><span data-stu-id="3ba3b-106">Supported data types include:</span></span>

* <span data-ttu-id="3ba3b-107">Zdarzenia funkcji Śledzenie zdarzeń systemu Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="3ba3b-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="3ba3b-108">Liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="3ba3b-108">Performance counters</span></span>
* <span data-ttu-id="3ba3b-109">Dzienniki zdarzeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="3ba3b-109">Windows event logs</span></span>
* <span data-ttu-id="3ba3b-110">Dzienniki aplikacji</span><span class="sxs-lookup"><span data-stu-id="3ba3b-110">Application logs</span></span>
* <span data-ttu-id="3ba3b-111">Dzienników infrastruktury Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="3ba3b-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="3ba3b-112">W tym artykule opisano, jak tooconfigure diagnostyki Azure z usługą Event Hubs od zakończenia tooend.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-112">This article shows you how tooconfigure Azure Diagnostics with Event Hubs from end tooend.</span></span> <span data-ttu-id="3ba3b-113">Także wskazówki dotyczące hello następujące typowe scenariusze:</span><span class="sxs-lookup"><span data-stu-id="3ba3b-113">Guidance is also provided for hello following common scenarios:</span></span>

* <span data-ttu-id="3ba3b-114">Sposób rejestrowania toocustomize hello i metryki, które jest wysyłana tooEvent koncentratory</span><span class="sxs-lookup"><span data-stu-id="3ba3b-114">How toocustomize hello logs and metrics that get sent tooEvent Hubs</span></span>
* <span data-ttu-id="3ba3b-115">Sposób konfiguracji toochange w każdym środowisku.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-115">How toochange configurations in each environment</span></span>
* <span data-ttu-id="3ba3b-116">Jak usługa Event Hubs tooview strumienia danych</span><span class="sxs-lookup"><span data-stu-id="3ba3b-116">How tooview Event Hubs stream data</span></span>
* <span data-ttu-id="3ba3b-117">Jak tootroubleshoot hello połączenia</span><span class="sxs-lookup"><span data-stu-id="3ba3b-117">How tootroubleshoot hello connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="3ba3b-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3ba3b-118">Prerequisites</span></span>
<span data-ttu-id="3ba3b-119">Dane receieving centra zdarzeń z diagnostyki Azure jest obsługiwana w usługi w chmurze, maszyn wirtualnych, zestawy skalowania maszyny wirtualnej i sieci szkieletowej usług w programie hello Azure SDK 2.9 i hello odpowiadającego Azure Tools dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in hello Azure SDK 2.9 and hello corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="3ba3b-120">Rozszerzenie diagnostyki Azure 1.6 ([zestawu Azure SDK dla programu .NET 2.9 lub nowszego](https://azure.microsoft.com/downloads/) dotyczy to domyślnie)</span><span class="sxs-lookup"><span data-stu-id="3ba3b-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="3ba3b-121">Visual Studio 2013 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="3ba3b-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="3ba3b-122">Istniejące konfiguracje diagnostyki Azure w aplikacji przy użyciu *.wadcfgx* pliku i jedną z następujących metod hello:</span><span class="sxs-lookup"><span data-stu-id="3ba3b-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of hello following methods:</span></span>
  * <span data-ttu-id="3ba3b-123">Visual Studio: [Konfigurowanie diagnostyki dla usług w chmurze Azure i maszyny wirtualne](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="3ba3b-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="3ba3b-124">Program Windows PowerShell: [Włącz diagnostykę w usług Azure Cloud Services przy użyciu programu PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="3ba3b-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="3ba3b-125">Przestrzeń nazw centra zdarzeń udostępniane na artykuł hello [Rozpoczynanie pracy z usługą Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="3ba3b-125">Event Hubs namespace provisioned per hello article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a><span data-ttu-id="3ba3b-126">Połącz zbiornika koncentratory tooEvent diagnostyki Azure</span><span class="sxs-lookup"><span data-stu-id="3ba3b-126">Connect Azure Diagnostics tooEvent Hubs sink</span></span>
<span data-ttu-id="3ba3b-127">Domyślnie diagnostyki Azure zawsze wysyła dzienniki i metryki tooan konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-127">By default, Azure Diagnostics always sends logs and metrics tooan Azure Storage account.</span></span> <span data-ttu-id="3ba3b-128">Aplikacja może również wysłać tooEvent danych koncentratory, dodając nową **wychwytywanie** w sekcji hello **PublicConfig** / **WadCfg** element hello *.wadcfgx* pliku.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-128">An application may also send data tooEvent Hubs by adding a new **Sinks** section under hello **PublicConfig** / **WadCfg** element of hello *.wadcfgx* file.</span></span> <span data-ttu-id="3ba3b-129">W programie Visual Studio hello *.wadcfgx* plik jest przechowywany w hello następującej ścieżki: **projekt usługi w chmurze** > **ról** > **() RoleName)** > **diagnostics.wadcfgx** pliku.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-129">In Visual Studio, hello *.wadcfgx* file is stored in hello following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "HotPath",
            "EventHub": {
                "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
                "SharedAccessKeyName": "SendRule"
            }
        }
    ]
}
```

<span data-ttu-id="3ba3b-130">W tym przykładzie hello Centrum zdarzeń jest ustawiony adres URL toohello pełni kwalifikowanych nazw Centrum zdarzeń hello: przestrzeń nazw usługi Event Hubs + "/" + Nazwa Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-130">In this example, hello event hub URL is set toohello fully qualified namespace of hello event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="3ba3b-131">adres URL jest wyświetlany w hello Centrum zdarzeń Hello [portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885) na pulpicie nawigacyjnym usługi Event Hubs hello.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-131">hello event hub URL is displayed in hello [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on hello Event Hubs dashboard.</span></span>  

<span data-ttu-id="3ba3b-132">Witaj **Sink** nazwa może być ustawiona prawidłowy ciąg tooany tak długo, jak hello tę samą wartość jest używana przez całą hello pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-132">hello **Sink** name can be set tooany valid string as long as hello same value is used consistently throughout hello config file.</span></span>

> [!NOTE]
> <span data-ttu-id="3ba3b-133">Mogą istnieć dodatkowe wychwytywanie, takich jak *applicationInsights* skonfigurowane w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="3ba3b-134">Diagnostyka Azure umożliwia jeden lub więcej wychwytywanie toobe zdefiniowana, jeśli każdy obiekt sink jest również zadeklarowany w hello **PrivateConfig** sekcji.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-134">Azure Diagnostics allows one or more sinks toobe defined if each sink is also declared in hello **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="3ba3b-135">Hello zbiornika centra zdarzeń należy również zadeklarowana i zdefiniowanych w hello **PrivateConfig** sekcji hello *.wadcfgx* pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-135">hello Event Hubs sink must also be declared and defined in hello **PrivateConfig** section of hello *.wadcfgx* config file.</span></span>

```XML
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="{account name}" key="{account key}" endpoint="{optional storage endpoint}" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
</PrivateConfig>
```
```JSON
{
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{optional storage endpoint}",
    "EventHub": {
        "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    }
}
```

<span data-ttu-id="3ba3b-136">Witaj `SharedAccessKeyName` wartości muszą być zgodne, klucz dostępu sygnatury dostępu Współdzielonego i zasad, który został zdefiniowany w hello **centra zdarzeń** przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-136">hello `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in hello **Event Hubs** namespace.</span></span> <span data-ttu-id="3ba3b-137">Przeglądaj pulpitu nawigacyjnego usługi Event Hubs toohello w hello [portalu Azure](https://manage.windowsazure.com), kliknij przycisk hello **Konfiguruj** , a następnie skonfigurować zasadę nazwanych (na przykład "SendRule"), która ma *wysyłania* uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-137">Browse toohello Event Hubs dashboard in hello [Azure portal](https://manage.windowsazure.com), click hello **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="3ba3b-138">Witaj **StorageAccount** jest również zadeklarowany w **PrivateConfig**.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-138">hello **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="3ba3b-139">Nie jest konieczne tutaj wartości toochange jeśli działają.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-139">There is no need toochange values here if they are working.</span></span> <span data-ttu-id="3ba3b-140">W tym przykładzie firma Microsoft może pozostać hello wartości puste, co jest znak czy podrzędne zasobów spowoduje ustawienie wartości hello.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-140">In this example, we leave hello values empty, which is a sign that a downstream asset will set hello values.</span></span> <span data-ttu-id="3ba3b-141">Na przykład Witaj *ServiceConfiguration.Cloud.cscfg* pliku konfiguracji środowiska ustawia hello odpowiednie środowisko nazwy i kluczy.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-141">For example, hello *ServiceConfiguration.Cloud.cscfg* environment configuration file sets hello environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="3ba3b-142">klucz sygnatury dostępu Współdzielonego centra zdarzeń Hello jest przechowywany w postaci zwykłego tekstu w hello *.wadcfgx* pliku.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-142">hello Event Hubs SAS key is stored in plain text in hello *.wadcfgx* file.</span></span> <span data-ttu-id="3ba3b-143">Często ten klucz jest zaewidencjonowany toosource kontroli kodu lub jest dostępna jako zasób w serwerze kompilacji, więc należy je chronić, zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-143">Often, this key is checked in toosource code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="3ba3b-144">Zalecane jest użycie klucza sygnatury dostępu Współdzielonego tutaj z *wysłać tylko* uprawnienia tak, aby złośliwy użytkownik można zapisać toohello Centrum zdarzeń, ale nie nasłuchiwania tooit lub zarządzać nim.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write toohello event hub, but not listen tooit or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a><span data-ttu-id="3ba3b-145">Skonfiguruj diagnostyki Azure toosend dzienniki i metryki tooEvent koncentratory</span><span class="sxs-lookup"><span data-stu-id="3ba3b-145">Configure Azure Diagnostics toosend logs and metrics tooEvent Hubs</span></span>
<span data-ttu-id="3ba3b-146">Zgodnie z opisem wcześniej, wszystkie domyślne i dane diagnostyki niestandardowej, oznacza to, metryki i dzienniki, są wysyłane automatycznie tooAzure magazynu z interwałem hello skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent tooAzure Storage in hello configured intervals.</span></span> <span data-ttu-id="3ba3b-147">Centra zdarzeń i wszelkie dodatkowe zbiornika w toobe hierarchii hello wysyłane toohello Centrum zdarzeń można określić dowolnego węzła głównego lub typu liść.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-147">With Event Hubs and any additional sink, you can specify any root or leaf node in hello hierarchy toobe sent toohello event hub.</span></span> <span data-ttu-id="3ba3b-148">W tym zdarzenia ETW, liczniki wydajności, dzienniki zdarzeń systemu Windows i dzienników aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="3ba3b-149">Koniecznie tooconsider liczbę punktów danych faktycznie powinna być przetransferowane tooEvent koncentratorów.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-149">It is important tooconsider how many data points should actually be transferred tooEvent Hubs.</span></span> <span data-ttu-id="3ba3b-150">Zwykle deweloperzy transferu danych hot ścieżki małe opóźnienia, który musi być używane i szybko interpretowane.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="3ba3b-151">Przykłady są systemy monitorowania, alertów lub reguły automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="3ba3b-152">Deweloper może również skonfigurować Magazyn alternatywnego analizy lub Wyszukaj magazynu — na przykład usługi Azure Stream Analytics, Elasticsearch, system monitorowania niestandardowe lub Ulubione system monitorowania od innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="3ba3b-153">Witaj poniżej przedstawiono niektóre przykładowe konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-153">hello following are some example configurations.</span></span>

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "sinks": "HotPath",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        }
    ]
}
```

<span data-ttu-id="3ba3b-154">W hello powyżej przykładzie, zbiornika hello jest nadrzędny zastosowane toohello **liczniki wydajności** węzeł w hierarchii hello, co oznacza, że wszystkie podrzędne **liczniki wydajności** będą wysyłane tooEvent koncentratorów.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-154">In hello above example, hello sink is applied toohello parent **PerformanceCounters** node in hello hierarchy, which means all child **PerformanceCounters** will be sent tooEvent Hubs.</span></span>  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Rejected",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Queued",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        }
    ]
}
```

<span data-ttu-id="3ba3b-155">W poprzednim przykładzie hello zbiornika hello jest zastosowane tooonly trzy liczniki: **żądania w kolejce**, **odrzucenia żądania**, i **% czasu procesora**.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-155">In hello previous example, hello sink is applied tooonly three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="3ba3b-156">Witaj poniższy przykład przedstawia sposób deweloper może ograniczyć hello ilość danych wysłanych toobe hello krytyczne metryki, które są używane dla tej usługi kondycji.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-156">hello following example shows how a developer can limit hello amount of sent data toobe hello critical metrics that are used for this service’s health.</span></span>  

```XML
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```
```JSON
"Logs": {
    "scheduledTransferPeriod": "PT1M",
    "scheduledTransferLogLevelFilter": "Error",
    "sinks": "HotPath"
}
```

<span data-ttu-id="3ba3b-157">W tym przykładzie zbiornika hello jest stosowane toologs i filtrowane tylko tooerror śledzenia poziomu.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-157">In this example, hello sink is applied toologs and is filtered only tooerror level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="3ba3b-158">Wdrażanie i aktualizacji aplikacji i informacji diagnostycznych konfiguracji usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="3ba3b-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="3ba3b-159">Visual Studio udostępnia hello najprostszym ścieżki toodeploy hello aplikacji i konfigurowanie zbiornika usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-159">Visual Studio provides hello easiest path toodeploy hello application and Event Hubs sink configuration.</span></span> <span data-ttu-id="3ba3b-160">Plik hello tooview i edytowanie, otwórz hello *.wadcfgx* plików w programie Visual Studio, go edytować i zapisać go.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-160">tooview and edit hello file, open hello *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="3ba3b-161">Ścieżka Hello jest **projekt usługi w chmurze** > **ról** > **(RoleName)** > **diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-161">hello path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="3ba3b-162">W tym momencie wszystkie wdrożenia i wdrożenia aktualizacji w Visual Studio, Visual Studio Team System i wszystkie polecenia lub skryptów, które są oparte na MSBuild i użyj hello akcje **/t: publikowanie** docelowy obejmują hello *.wadcfgx*  w procesie tworzenia pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use hello **/t:publish** target include hello *.wadcfgx* in hello packaging process.</span></span> <span data-ttu-id="3ba3b-163">Ponadto wdrożenia i aktualizacje wdrożyć hello tooAzure pliku przy użyciu hello odpowiednie rozszerzenie agenta diagnostyki Azure na maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-163">In addition, deployments and updates deploy hello file tooAzure by using hello appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="3ba3b-164">Po wdrożeniu aplikacji hello i konfiguracji diagnostyki Azure, będzie wyświetlany natychmiast działania na pulpicie nawigacyjnym hello hello Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-164">After you deploy hello application and Azure Diagnostics configuration, you will immediately see activity in hello dashboard of hello event hub.</span></span> <span data-ttu-id="3ba3b-165">Oznacza to, że wszystko jest gotowe toomove na tooviewing hello hot ścieżki danych hello odbiornika klienta lub analizy dowolnego narzędzia.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-165">This indicates that you're ready toomove on tooviewing hello hot-path data in hello listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="3ba3b-166">W następującej ilustracji hello pulpit nawigacyjny usługi Event Hubs hello pokazuje, dobrej kondycji wysyłania diagnostyki danych toohello zdarzenia koncentratora początkowych pewnego czasu po 23: 00.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-166">In hello following figure, hello Event Hubs dashboard shows healthy sending of diagnostics data toohello event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="3ba3b-167">Kiedy jest hello aplikacja została wdrożona z zaktualizowaną *.wadcfgx* plików i hello zbiornika zostało skonfigurowane prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-167">That's when hello application was deployed with an updated *.wadcfgx* file, and hello sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="3ba3b-168">Po wprowadzeniu pliku konfiguracji diagnostyki Azure toohello aktualizacji (.wadcfgx), zaleca się push hello aktualizacje toohello całej aplikacji, a także hello konfiguracji za pomocą programu Visual Studio publikowania lub skrypt programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-168">When you make updates toohello Azure Diagnostics config file (.wadcfgx), it's recommended that you push hello updates toohello entire application as well as hello configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="3ba3b-169">Dane widoku dynamicznego ścieżki</span><span class="sxs-lookup"><span data-stu-id="3ba3b-169">View hot-path data</span></span>
<span data-ttu-id="3ba3b-170">Jak wcześniej wspomniano, istnieje wiele przypadki użycia nasłuchiwania tooand przetwarzania danych usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-170">As discussed previously, there are many use cases for listening tooand processing Event Hubs data.</span></span>

<span data-ttu-id="3ba3b-171">Jednym z podejść proste jest toocreate z Centrum testów małych konsoli aplikacji toolisten toohello zdarzeń i drukowania hello strumienia wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-171">One simple approach is toocreate a small test console application toolisten toohello event hub and print hello output stream.</span></span> <span data-ttu-id="3ba3b-172">Możesz umieścić hello następującego kodu, który jest co omówiono bardziej szczegółowo w [Rozpoczynanie pracy z usługą Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), w aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-172">You can place hello following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="3ba3b-173">Należy pamiętać, że aplikacja konsolowa hello musi zawierać hello [pakietu NuGet hosta procesora zdarzeń](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="3ba3b-173">Note that hello console application must include hello [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="3ba3b-174">Pamiętaj tooreplace hello wartości w nawiasy w hello **Main** funkcji z wartościami dla zasobów.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-174">Remember tooreplace hello values in angle brackets in hello **Main** function with values for your resources.</span></span>   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key toostop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="3ba3b-175">Rozwiązywanie problemów z wychwytywanie centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="3ba3b-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="3ba3b-176">Centrum zdarzeń Hello nie są wyświetlane zdarzenia przychodzącego lub wychodzącego działania zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-176">hello event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="3ba3b-177">Sprawdź, czy Centrum zdarzeń jest pomyślnie zainicjowano obsługę administracyjną.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="3ba3b-178">Wszystkie informacje o połączeniu w hello **PrivateConfig** sekcji *.wadcfgx* musi odpowiadać wartości hello zasobu w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-178">All connection info in hello **PrivateConfig** section of *.wadcfgx* must match hello values of your resource as seen in hello portal.</span></span> <span data-ttu-id="3ba3b-179">Upewnij się, że masz SAS zasady zdefiniowane ("SendRule" w przykładzie hello) w portalu hello, który *wysyłania* uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-179">Make sure that you have a SAS policy defined ("SendRule" in hello example) in hello portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="3ba3b-180">Po zaktualizowaniu Centrum zdarzeń hello nie jest już wyświetlana działania zdarzenia przychodzącego lub wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-180">After an update, hello event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="3ba3b-181">Najpierw upewnij się, że hello Centrum zdarzeń i informacje o konfiguracji są poprawne, jak opisano wcześniej.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-181">First, make sure that hello event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="3ba3b-182">Czasami hello **PrivateConfig** jest resetowany w aktualizacji wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-182">Sometimes hello **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="3ba3b-183">Witaj zalecane jest poprawka toomake wszystkie zmiany zbyt*.wadcfgx* w hello projektu, a następnie Wypchnij aktualizacji kompletna aplikacja.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-183">hello recommended fix is toomake all changes too*.wadcfgx* in hello project and then push a complete application update.</span></span> <span data-ttu-id="3ba3b-184">Jeśli nie jest to możliwe, upewnij się, aktualizacja diagnostyki hello wypchnięcia pełnego **PrivateConfig** zawierającą hello klucza sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-184">If this is not possible, make sure that hello diagnostics update pushes a complete **PrivateConfig** that includes hello SAS key.</span></span>  
* <span data-ttu-id="3ba3b-185">Próbuję hello sugestie i Centrum zdarzeń hello nadal nie działa.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-185">I tried hello suggestions, and hello event hub is still not working.</span></span>

    <span data-ttu-id="3ba3b-186">Należy przejrzeć hello Azure Storage tabeli, która zawiera dzienniki i błędy diagnostyki Azure, sama: **WADDiagnosticInfrastructureLogsTable**.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-186">Try looking in hello Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="3ba3b-187">Jedną z opcji jest toouse narzędzia, takie jak [Eksploratora usługi Storage Azure](http://www.storageexplorer.com) tooconnect toothis konta magazynu, wyświetlić tę tabelę i Dodaj zapytanie dla sygnatury czasowej w hello ostatnich 24 godzinach.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-187">One option is toouse a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) tooconnect toothis storage account, view this table, and add a query for TimeStamp in hello last 24 hours.</span></span> <span data-ttu-id="3ba3b-188">Można użyć hello narzędzia tooexport plik CSV i otwórz go w aplikacji, takich jak program Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-188">You can use hello tool tooexport a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="3ba3b-189">Excel umożliwia łatwe toosearch ciągi karty telefonicznej, takich jak **EventHubs**, jakie błąd jest zgłaszany toosee.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-189">Excel makes it easy toosearch for calling-card strings, such as **EventHubs**, toosee what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="3ba3b-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3ba3b-190">Next steps</span></span>
<span data-ttu-id="3ba3b-191">• [Dowiedz się więcej o usłudze Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="3ba3b-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="3ba3b-192">Dodatek: Ukończyć przykład pliku (.wadcfgx) konfiguracji diagnostyki Azure</span><span class="sxs-lookup"><span data-stu-id="3ba3b-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount>ACCOUNT_NAME</StorageAccount>
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="{account name}" key="{account key}" endpoint="{storage endpoint}" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

<span data-ttu-id="3ba3b-193">uzupełniające Hello *ServiceConfiguration.Cloud.cscfg* dla tego przykładu wygląda hello.</span><span class="sxs-lookup"><span data-stu-id="3ba3b-193">hello complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like hello following.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="3ba3b-194">Odpowiednik Json na podstawie ustawień maszyny wirtualnej jest następujący:</span><span class="sxs-lookup"><span data-stu-id="3ba3b-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
```JSON
"settings": {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 4096,
            "sinks": "applicationInsights.errors",
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "Directories": {
                "scheduledTransferPeriod": "PT1M",
                "IISLogs": {
                    "containerName": "wad-iis-logfiles"
                },
                "FailedRequestLogs": {
                    "containerName": "wad-failedrequestlogs"
                }
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "sinks": "HotPath",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Memory\\Available MBytes",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\Bytes Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Requests/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Errors Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Queued",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Rejected",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
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
                "scheduledTransferLogLevelFilter": "Error",
                "sinks": "HotPath"
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "HotPath",
                    "EventHub": {
                        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
                        "SharedAccessKeyName": "SendRule"
                    }
                },
                {
                    "name": "applicationInsights",
                    "ApplicationInsights": "",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "errors"
                            }
                        ]
                    }
                }
            ]
        }
    },
    "StorageAccount": "{account name}"
}


"protectedSettings": {
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{storage endpoint}",
    "EventHub": {
        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "YOUR_KEY_HERE"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="3ba3b-195">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3ba3b-195">Next steps</span></span>
<span data-ttu-id="3ba3b-196">Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="3ba3b-196">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="3ba3b-197">Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3ba3b-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="3ba3b-198">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="3ba3b-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="3ba3b-199">Event Hubs — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="3ba3b-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
