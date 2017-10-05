---
title: "Strumieniowe przesyłanie danych diagnostycznych platformy Azure w ścieżce aktywnej za pomocą usługi Event Hubs | Dokumentacja firmy Microsoft"
description: "Konfigurowanie diagnostyki Azure za pomocą usługi Event Hubs kompleksowe, w tym wskazówki dotyczące typowych scenariuszy."
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
ms.openlocfilehash: 1c05bd6dc4c4d394aa043b9995de9c184e4f14c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="streaming-azure-diagnostics-data-in-the-hot-path-by-using-event-hubs"></a><span data-ttu-id="16435-103">Strumieniowe przesyłanie danych diagnostycznych platformy Azure w ścieżce aktywnej za pomocą usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="16435-103">Streaming Azure Diagnostics data in the hot path by using Event Hubs</span></span>
<span data-ttu-id="16435-104">Diagnostyka Azure oferuje elastyczne metod zbierać metryki i dzienniki z maszyn wirtualnych usługi w chmurze (VM) i przenieść wyniki do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="16435-104">Azure Diagnostics provides flexible ways to collect metrics and logs from cloud services virtual machines (VMs) and transfer results to Azure Storage.</span></span> <span data-ttu-id="16435-105">Uruchamianie w ramach czasowych marca 2016 (zestaw SDK 2.9), można wysyłanie danych diagnostycznych do źródeł danych niestandardowych i transferu danych ścieżkę aktywną w ciągu sekund za pomocą [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="16435-105">Starting in the March 2016 (SDK 2.9) time frame, you can send Diagnostics to custom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="16435-106">Obsługiwane typy danych obejmują:</span><span class="sxs-lookup"><span data-stu-id="16435-106">Supported data types include:</span></span>

* <span data-ttu-id="16435-107">Zdarzenia funkcji Śledzenie zdarzeń systemu Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="16435-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="16435-108">Liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="16435-108">Performance counters</span></span>
* <span data-ttu-id="16435-109">Dzienniki zdarzeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="16435-109">Windows event logs</span></span>
* <span data-ttu-id="16435-110">Dzienniki aplikacji</span><span class="sxs-lookup"><span data-stu-id="16435-110">Application logs</span></span>
* <span data-ttu-id="16435-111">Dzienników infrastruktury Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="16435-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="16435-112">W tym artykule przedstawiono sposób konfigurowania diagnostyki Azure z usługą Event Hubs od końca do końca.</span><span class="sxs-lookup"><span data-stu-id="16435-112">This article shows you how to configure Azure Diagnostics with Event Hubs from end to end.</span></span> <span data-ttu-id="16435-113">Także wskazówki dotyczące następujących scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="16435-113">Guidance is also provided for the following common scenarios:</span></span>

* <span data-ttu-id="16435-114">Dostosowywanie dzienniki i metryki, która jest wysyłana do usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="16435-114">How to customize the logs and metrics that get sent to Event Hubs</span></span>
* <span data-ttu-id="16435-115">Jak zmienić konfiguracje w każdym środowisku.</span><span class="sxs-lookup"><span data-stu-id="16435-115">How to change configurations in each environment</span></span>
* <span data-ttu-id="16435-116">Jak wyświetlać dane strumienia centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="16435-116">How to view Event Hubs stream data</span></span>
* <span data-ttu-id="16435-117">Jak rozwiązywać problemy z połączenia</span><span class="sxs-lookup"><span data-stu-id="16435-117">How to troubleshoot the connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="16435-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="16435-118">Prerequisites</span></span>
<span data-ttu-id="16435-119">Dane receieving centra zdarzeń z diagnostyki Azure jest obsługiwana w usługi w chmurze, maszyn wirtualnych, zestawy skalowania maszyny wirtualnej i sieci szkieletowej usług, począwszy od programu Azure SDK 2.9 i odpowiednie narzędzia Azure dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="16435-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in the Azure SDK 2.9 and the corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="16435-120">Rozszerzenie diagnostyki Azure 1.6 ([zestawu Azure SDK dla programu .NET 2.9 lub nowszego](https://azure.microsoft.com/downloads/) dotyczy to domyślnie)</span><span class="sxs-lookup"><span data-stu-id="16435-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="16435-121">Visual Studio 2013 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="16435-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="16435-122">Istniejące konfiguracje diagnostyki Azure w aplikacji przy użyciu *.wadcfgx* plików i jedną z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="16435-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of the following methods:</span></span>
  * <span data-ttu-id="16435-123">Visual Studio: [Konfigurowanie diagnostyki dla usług w chmurze Azure i maszyny wirtualne](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="16435-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="16435-124">Program Windows PowerShell: [Włącz diagnostykę w usług Azure Cloud Services przy użyciu programu PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="16435-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="16435-125">Udostępniane na artykuł, centra zdarzeń w przestrzeni nazw [Rozpoczynanie pracy z usługą Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="16435-125">Event Hubs namespace provisioned per the article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-to-event-hubs-sink"></a><span data-ttu-id="16435-126">Połącz diagnostyki Azure do ujścia centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="16435-126">Connect Azure Diagnostics to Event Hubs sink</span></span>
<span data-ttu-id="16435-127">Domyślnie diagnostyki Azure zawsze wysyła dzienniki i metryk do konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="16435-127">By default, Azure Diagnostics always sends logs and metrics to an Azure Storage account.</span></span> <span data-ttu-id="16435-128">Aplikacja może również wysyłać dane do usługi Event Hubs, dodając nową **wychwytywanie** w obszarze **PublicConfig** / **WadCfg** elementu *.wadcfgx* pliku.</span><span class="sxs-lookup"><span data-stu-id="16435-128">An application may also send data to Event Hubs by adding a new **Sinks** section under the **PublicConfig** / **WadCfg** element of the *.wadcfgx* file.</span></span> <span data-ttu-id="16435-129">W programie Visual Studio *.wadcfgx* plik znajduje się w następującej ścieżce: **projekt usługi w chmurze** > **ról** > **(RoleName)** > **diagnostics.wadcfgx** pliku.</span><span class="sxs-lookup"><span data-stu-id="16435-129">In Visual Studio, the *.wadcfgx* file is stored in the following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

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

<span data-ttu-id="16435-130">W tym przykładzie adres URL Centrum zdarzeń jest równa nazw FQDN Centrum zdarzeń: przestrzeń nazw usługi Event Hubs + "/" + Nazwa Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="16435-130">In this example, the event hub URL is set to the fully qualified namespace of the event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="16435-131">Adres URL jest wyświetlany w Centrum zdarzeń [portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885) na pulpicie nawigacyjnym usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="16435-131">The event hub URL is displayed in the [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on the Event Hubs dashboard.</span></span>  

<span data-ttu-id="16435-132">**Sink** może mieć ustawionej nazwy dowolny prawidłowy ciąg tak długo, jak taką samą wartość jest używana przez całą pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="16435-132">The **Sink** name can be set to any valid string as long as the same value is used consistently throughout the config file.</span></span>

> [!NOTE]
> <span data-ttu-id="16435-133">Mogą istnieć dodatkowe wychwytywanie, takich jak *applicationInsights* skonfigurowane w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="16435-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="16435-134">Diagnostyka Azure umożliwia wychwytywanie co najmniej jeden do zdefiniowania, jeśli każdy obiekt sink jest również zadeklarowany w **PrivateConfig** sekcji.</span><span class="sxs-lookup"><span data-stu-id="16435-134">Azure Diagnostics allows one or more sinks to be defined if each sink is also declared in the **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="16435-135">Zbiornik usługi Event Hubs również musi być zadeklarowana i zdefiniowane w **PrivateConfig** sekcji *.wadcfgx* pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="16435-135">The Event Hubs sink must also be declared and defined in the **PrivateConfig** section of the *.wadcfgx* config file.</span></span>

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

<span data-ttu-id="16435-136">`SharedAccessKeyName` Wartości muszą być zgodne, klucz dostępu sygnatury dostępu Współdzielonego i zasad, który został zdefiniowany w **usługi Event Hubs** przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="16435-136">The `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in the **Event Hubs** namespace.</span></span> <span data-ttu-id="16435-137">Przejdź do pulpitu nawigacyjnego usługi Event Hubs w [portalu Azure](https://manage.windowsazure.com), kliknij przycisk **Konfiguruj** , a następnie skonfigurować zasadę nazwanych (na przykład "SendRule"), która ma *wysyłania* uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="16435-137">Browse to the Event Hubs dashboard in the [Azure portal](https://manage.windowsazure.com), click the **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="16435-138">**StorageAccount** jest również zadeklarowany w **PrivateConfig**.</span><span class="sxs-lookup"><span data-stu-id="16435-138">The **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="16435-139">Nie istnieje potrzeba umożliwia zmianę wartości w tym miejscu pracy.</span><span class="sxs-lookup"><span data-stu-id="16435-139">There is no need to change values here if they are working.</span></span> <span data-ttu-id="16435-140">W tym przykładzie firma Microsoft może pozostać wartości puste, która jest znak, że zasób podrzędne spowoduje ustawienie wartości.</span><span class="sxs-lookup"><span data-stu-id="16435-140">In this example, we leave the values empty, which is a sign that a downstream asset will set the values.</span></span> <span data-ttu-id="16435-141">Na przykład *ServiceConfiguration.Cloud.cscfg* pliku konfiguracji środowiska ustawia odpowiednie środowisko nazwy i kluczy.</span><span class="sxs-lookup"><span data-stu-id="16435-141">For example, the *ServiceConfiguration.Cloud.cscfg* environment configuration file sets the environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="16435-142">Klucz sygnatury dostępu Współdzielonego Event Hubs jest przechowywany w postaci zwykłego tekstu w *.wadcfgx* pliku.</span><span class="sxs-lookup"><span data-stu-id="16435-142">The Event Hubs SAS key is stored in plain text in the *.wadcfgx* file.</span></span> <span data-ttu-id="16435-143">Często ten klucz jest zaewidencjonowany do kontroli kodu źródłowego lub jest dostępna jako zasób w serwerze kompilacji, więc należy je chronić, zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="16435-143">Often, this key is checked in to source code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="16435-144">Zalecane jest użycie klucza sygnatury dostępu Współdzielonego tutaj z *wysłać tylko* uprawnienia tak, aby złośliwy użytkownik może zapisać do Centrum zdarzeń, ale nie nasłuchiwania do niego lub możesz nim zarządzać.</span><span class="sxs-lookup"><span data-stu-id="16435-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write to the event hub, but not listen to it or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-to-send-logs-and-metrics-to-event-hubs"></a><span data-ttu-id="16435-145">Skonfiguruj diagnostyki Azure, aby wysłać dzienniki i metryk do usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="16435-145">Configure Azure Diagnostics to send logs and metrics to Event Hubs</span></span>
<span data-ttu-id="16435-146">Zgodnie z opisem wcześniej, wszystkie domyślne i dane diagnostyki niestandardowej, oznacza to, metryki i dzienników, jest automatycznie przesyłany do usługi Azure Storage w skonfigurowanych interwałów.</span><span class="sxs-lookup"><span data-stu-id="16435-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent to Azure Storage in the configured intervals.</span></span> <span data-ttu-id="16435-147">Centra zdarzeń i wszelkie dodatkowe zbiornika można określić dowolnego węzła głównego lub liścia w hierarchii, które mają być wysyłane do Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="16435-147">With Event Hubs and any additional sink, you can specify any root or leaf node in the hierarchy to be sent to the event hub.</span></span> <span data-ttu-id="16435-148">W tym zdarzenia ETW, liczniki wydajności, dzienniki zdarzeń systemu Windows i dzienników aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16435-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="16435-149">Należy wziąć pod uwagę liczbę punktów danych faktycznie mają zostać przeniesione do usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="16435-149">It is important to consider how many data points should actually be transferred to Event Hubs.</span></span> <span data-ttu-id="16435-150">Zwykle deweloperzy transferu danych hot ścieżki małe opóźnienia, który musi być używane i szybko interpretowane.</span><span class="sxs-lookup"><span data-stu-id="16435-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="16435-151">Przykłady są systemy monitorowania, alertów lub reguły automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="16435-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="16435-152">Deweloper może również skonfigurować Magazyn alternatywnego analizy lub Wyszukaj magazynu — na przykład usługi Azure Stream Analytics, Elasticsearch, system monitorowania niestandardowe lub Ulubione system monitorowania od innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="16435-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="16435-153">Poniżej przedstawiono niektóre przykładowe konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="16435-153">The following are some example configurations.</span></span>

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

<span data-ttu-id="16435-154">W powyższym przykładzie sink są stosowane do nadrzędnego **liczniki wydajności** węzeł w hierarchii, co oznacza, że wszystkie podrzędne **liczniki wydajności** będą wysyłane do usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="16435-154">In the above example, the sink is applied to the parent **PerformanceCounters** node in the hierarchy, which means all child **PerformanceCounters** will be sent to Event Hubs.</span></span>  

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

<span data-ttu-id="16435-155">W poprzednim przykładzie obiekt sink zostanie zastosowana tylko trzy liczniki: **żądania w kolejce**, **odrzucenia żądania**, i **% czasu procesora**.</span><span class="sxs-lookup"><span data-stu-id="16435-155">In the previous example, the sink is applied to only three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="16435-156">W poniższym przykładzie pokazano, jak deweloper może ograniczyć ilość danych wysłanych krytyczne metryki, które są używane dla tej usługi kondycji.</span><span class="sxs-lookup"><span data-stu-id="16435-156">The following example shows how a developer can limit the amount of sent data to be the critical metrics that are used for this service’s health.</span></span>  

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

<span data-ttu-id="16435-157">W tym przykładzie obiekt sink jest stosowany do dzienników i jest filtrowana tylko dla błędów poziomu śledzenia.</span><span class="sxs-lookup"><span data-stu-id="16435-157">In this example, the sink is applied to logs and is filtered only to error level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="16435-158">Wdrażanie i aktualizacji aplikacji i informacji diagnostycznych konfiguracji usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="16435-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="16435-159">Program Visual Studio udostępnia najłatwiejszą do wdrażania aplikacji i usługi Event Hubs zbiornika konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="16435-159">Visual Studio provides the easiest path to deploy the application and Event Hubs sink configuration.</span></span> <span data-ttu-id="16435-160">Aby wyświetlić i edytować plik, otwórz *.wadcfgx* plików w programie Visual Studio, go edytować i zapisać go.</span><span class="sxs-lookup"><span data-stu-id="16435-160">To view and edit the file, open the *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="16435-161">Ścieżka jest **projekt usługi w chmurze** > **ról** > **(RoleName)** > **diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="16435-161">The path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="16435-162">W tym momencie wszystkie wdrożenia i wdrożenia aktualizacji w Visual Studio, Visual Studio Team System i wszystkie polecenia lub skryptów, które są oparte na MSBuild i użyj akcje **/t: publikowanie** docelowy obejmują *.wadcfgx* w procesie tworzenia pakietów.</span><span class="sxs-lookup"><span data-stu-id="16435-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use the **/t:publish** target include the *.wadcfgx* in the packaging process.</span></span> <span data-ttu-id="16435-163">Ponadto wdrożenia i aktualizacje wdrażanie pliku na platformie Azure przy użyciu odpowiedniego rozszerzenia agenta diagnostyki Azure na maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="16435-163">In addition, deployments and updates deploy the file to Azure by using the appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="16435-164">Po wdrożeniu aplikacji i konfiguracji diagnostyki Azure, będzie wyświetlany natychmiast działania na pulpicie nawigacyjnym Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="16435-164">After you deploy the application and Azure Diagnostics configuration, you will immediately see activity in the dashboard of the event hub.</span></span> <span data-ttu-id="16435-165">Oznacza to, że możesz przejść do wyświetlania danych hot ścieżki w narzędziu klienta lub analizy odbiornika wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="16435-165">This indicates that you're ready to move on to viewing the hot-path data in the listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="16435-166">Na poniższej ilustracji na pulpicie nawigacyjnym usługi Event Hubs zawiera dobrej kondycji wysyłanie danych diagnostycznych do Centrum zdarzeń uruchamianie pewnego czasu po 23: 00.</span><span class="sxs-lookup"><span data-stu-id="16435-166">In the following figure, the Event Hubs dashboard shows healthy sending of diagnostics data to the event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="16435-167">Gdy to aplikacja została wdrożona z zaktualizowaną *.wadcfgx* pliku, a obiekt sink zostało skonfigurowane prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="16435-167">That's when the application was deployed with an updated *.wadcfgx* file, and the sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="16435-168">Po wprowadzeniu aktualizacji do pliku konfiguracji diagnostyki Azure (.wadcfgx), zaleca się wypychania aktualizacji do całej aplikacji, a także konfiguracji za pomocą programu Visual Studio publikowania lub skrypt programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16435-168">When you make updates to the Azure Diagnostics config file (.wadcfgx), it's recommended that you push the updates to the entire application as well as the configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="16435-169">Dane widoku dynamicznego ścieżki</span><span class="sxs-lookup"><span data-stu-id="16435-169">View hot-path data</span></span>
<span data-ttu-id="16435-170">Jak wcześniej wspomniano, istnieje wiele zastosowań do nasłuchiwania i przetwarzania danych usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="16435-170">As discussed previously, there are many use cases for listening to and processing Event Hubs data.</span></span>

<span data-ttu-id="16435-171">Jest jednym z podejść proste do tworzenia aplikacji konsoli teście małych do nasłuchiwania Centrum zdarzeń i drukowanie w strumieniu wyjściowym.</span><span class="sxs-lookup"><span data-stu-id="16435-171">One simple approach is to create a small test console application to listen to the event hub and print the output stream.</span></span> <span data-ttu-id="16435-172">Możesz umieścić następujący kod, który jest co omówiono bardziej szczegółowo w [Rozpoczynanie pracy z usługą Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), w aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="16435-172">You can place the following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="16435-173">Należy pamiętać, że aplikacja konsoli musi zawierać [pakietu NuGet hosta procesora zdarzeń](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="16435-173">Note that the console application must include the [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="16435-174">Pamiętaj, aby zastąpić wartości w nawiasy w **Main** funkcji z wartościami dla zasobów.</span><span class="sxs-lookup"><span data-stu-id="16435-174">Remember to replace the values in angle brackets in the **Main** function with values for your resources.</span></span>   

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

            Console.WriteLine("Receiving. Press enter key to stop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="16435-175">Rozwiązywanie problemów z wychwytywanie centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="16435-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="16435-176">Centrum zdarzeń nie są wyświetlane zdarzenia przychodzącego lub wychodzącego działania zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="16435-176">The event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="16435-177">Sprawdź, czy Centrum zdarzeń jest pomyślnie zainicjowano obsługę administracyjną.</span><span class="sxs-lookup"><span data-stu-id="16435-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="16435-178">Wszystkie informacje o połączeniu w **PrivateConfig** sekcji *.wadcfgx* musi odpowiadać wartości zasobu, jak pokazano w portalu.</span><span class="sxs-lookup"><span data-stu-id="16435-178">All connection info in the **PrivateConfig** section of *.wadcfgx* must match the values of your resource as seen in the portal.</span></span> <span data-ttu-id="16435-179">Upewnij się, że masz SAS zasady zdefiniowane ("SendRule" w przykładzie) w portalu, który *wysyłania* uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="16435-179">Make sure that you have a SAS policy defined ("SendRule" in the example) in the portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="16435-180">Po zaktualizowaniu Centrum zdarzeń nie jest już wyświetlana działania zdarzenia przychodzącego lub wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="16435-180">After an update, the event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="16435-181">Najpierw upewnij się, czy informacje o Centrum i konfiguracji zdarzeń jest poprawna, jak opisano wcześniej.</span><span class="sxs-lookup"><span data-stu-id="16435-181">First, make sure that the event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="16435-182">Czasami **PrivateConfig** jest resetowany w aktualizacji wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="16435-182">Sometimes the **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="16435-183">Zalecane rozwiązanie polega na wszystkie zmiany do *.wadcfgx* w projekcie, a następnie wypychania aktualizacji kompletna aplikacja.</span><span class="sxs-lookup"><span data-stu-id="16435-183">The recommended fix is to make all changes to *.wadcfgx* in the project and then push a complete application update.</span></span> <span data-ttu-id="16435-184">Jeśli nie jest to możliwe, upewnij się, że aktualizacji diagnostyki wypchnięcia pełnego **PrivateConfig** zawierającej klucz sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="16435-184">If this is not possible, make sure that the diagnostics update pushes a complete **PrivateConfig** that includes the SAS key.</span></span>  
* <span data-ttu-id="16435-185">Próbuję sugestie i Centrum zdarzeń nadal nie działa.</span><span class="sxs-lookup"><span data-stu-id="16435-185">I tried the suggestions, and the event hub is still not working.</span></span>

    <span data-ttu-id="16435-186">Należy przejrzeć tabeli magazynu Azure, która zawiera dzienniki i błędy diagnostyki Azure, sama: **WADDiagnosticInfrastructureLogsTable**.</span><span class="sxs-lookup"><span data-stu-id="16435-186">Try looking in the Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="16435-187">Jedną z opcji się za pomocą narzędzia, takie jak [Eksploratora usługi Storage Azure](http://www.storageexplorer.com) nawiązać tego konta magazynu, wyświetlić tej tabeli i Dodaj zapytanie dla sygnatury czasowej w ostatnich 24 godzin.</span><span class="sxs-lookup"><span data-stu-id="16435-187">One option is to use a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) to connect to this storage account, view this table, and add a query for TimeStamp in the last 24 hours.</span></span> <span data-ttu-id="16435-188">Można użyć narzędzia, aby wyeksportować plik CSV i otwórz go w aplikacji, takich jak program Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="16435-188">You can use the tool to export a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="16435-189">Excel ułatwia wyszukiwanie ciągów karty telefonicznej, takich jak **EventHubs**, aby zobaczyć, jakie błąd jest zgłaszany.</span><span class="sxs-lookup"><span data-stu-id="16435-189">Excel makes it easy to search for calling-card strings, such as **EventHubs**, to see what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="16435-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16435-190">Next steps</span></span>
<span data-ttu-id="16435-191">• [Dowiedz się więcej o usłudze Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="16435-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="16435-192">Dodatek: Ukończyć przykład pliku (.wadcfgx) konfiguracji diagnostyki Azure</span><span class="sxs-lookup"><span data-stu-id="16435-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
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

<span data-ttu-id="16435-193">Uzupełniające *ServiceConfiguration.Cloud.cscfg* dla tego przykładu wygląda podobnie do następującej.</span><span class="sxs-lookup"><span data-stu-id="16435-193">The complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like the following.</span></span>

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

<span data-ttu-id="16435-194">Odpowiednik Json na podstawie ustawień maszyny wirtualnej jest następujący:</span><span class="sxs-lookup"><span data-stu-id="16435-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="16435-195">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16435-195">Next steps</span></span>
<span data-ttu-id="16435-196">Następujące linki pozwalają dowiedzieć się więcej na temat usługi Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="16435-196">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="16435-197">Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="16435-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="16435-198">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="16435-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="16435-199">Event Hubs — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="16435-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
