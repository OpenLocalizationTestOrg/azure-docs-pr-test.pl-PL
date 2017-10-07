---
title: dane aaaCollect z CollectD w OMS Log Analytics | Dokumentacja firmy Microsoft
description: "CollectD jest demonów systemu Linux typu open source, który okresowo zbiera dane z aplikacji oraz informacje o poziomie systemu.  Ten artykuł zawiera informacje dotyczące zbierania danych z CollectD w analizy dzienników."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: magoedte
ms.openlocfilehash: 7ad82c9c67a664aabd44f08bef2253d84cd2dfba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="34334-104">Zbieranie danych z CollectD na agentach systemu Linux w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="34334-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="34334-105">[CollectD](https://collectd.org/) jest demonów systemu Linux typu open source, która okresowo gromadzi metryki wydajności z aplikacji i informacji o poziomie systemu.</span><span class="sxs-lookup"><span data-stu-id="34334-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="34334-106">Przykładowe aplikacje obejmują hello maszyny wirtualnej Java (JVM), serwer MySQL i Nginx.</span><span class="sxs-lookup"><span data-stu-id="34334-106">Example applications include hello Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="34334-107">Ten artykuł zawiera informacje dotyczące zbierania danych wydajności z CollectD w analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="34334-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="34334-108">Pełną listę dostępnych wtyczek można znaleźć w folderze [tabeli wtyczek](https://collectd.org/wiki/index.php/Table_of_Plugins).</span><span class="sxs-lookup"><span data-stu-id="34334-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![Omówienie CollectD](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="34334-110">Witaj następującej konfiguracji CollectD znajduje się w hello Agent pakietu OMS dla systemu Linux tooroute CollectD danych toohello Agent pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="34334-110">hello following CollectD configuration is included in hello OMS Agent for Linux tooroute  CollectD data toohello OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="34334-111">Ponadto jeśli używane wersje collectD przed powitania po konfiguracji zamiast tego użyj 5.5.</span><span class="sxs-lookup"><span data-stu-id="34334-111">Additionally, if using an versions of collectD before 5.5 use hello following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="34334-112">Konfiguracja CollectD Hello korzysta z domyślnego hello`write_http` danych metryki wydajności toosend wtyczki za pośrednictwem portu 26000 tooOMS agenta dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="34334-112">hello CollectD configuration uses hello default`write_http` plugin toosend performance metric data over port 26000 tooOMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="34334-113">Ten port może być skonfigurowany tooa niestandardowy port, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="34334-113">This port can be configured tooa custom-defined port if needed.</span></span>

<span data-ttu-id="34334-114">Witaj Agent pakietu OMS dla systemu Linux również nasłuchuje na porcie 26000 dla metryki CollectD, a następnie konwertuje je tooOMS schematu metryki.</span><span class="sxs-lookup"><span data-stu-id="34334-114">hello OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them tooOMS schema metrics.</span></span> <span data-ttu-id="34334-115">Witaj Oto hello Agent pakietu OMS dla konfiguracji systemu Linux `collectd.conf`.</span><span class="sxs-lookup"><span data-stu-id="34334-115">hello following is hello OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="34334-116">Obsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="34334-116">Versions supported</span></span>
- <span data-ttu-id="34334-117">Analiza dzienników obsługuje obecnie CollectD wersji 4.8 i powyżej.</span><span class="sxs-lookup"><span data-stu-id="34334-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="34334-118">Dla kolekcji metryki CollectD wymagany jest Agent pakietu OMS dla systemu Linux v1.1.0-217 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="34334-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="34334-119">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="34334-119">Configuration</span></span>
<span data-ttu-id="34334-120">Witaj poniżej przedstawiono podstawowe czynności tooconfigure zbierania danych CollectD w analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="34334-120">hello following are basic steps tooconfigure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="34334-121">Skonfiguruj CollectD toosend danych toohello Agent pakietu OMS dla systemu Linux przy użyciu wtyczki write_http hello.</span><span class="sxs-lookup"><span data-stu-id="34334-121">Configure CollectD toosend data toohello OMS Agent for Linux using hello write_http plugin.</span></span>  
2. <span data-ttu-id="34334-122">Skonfiguruj hello Agent pakietu OMS dla systemu Linux toolisten dla hello CollectD danych na powitania odpowiedni port.</span><span class="sxs-lookup"><span data-stu-id="34334-122">Configure hello OMS Agent for Linux toolisten for hello CollectD data on hello appropriate port.</span></span>
3. <span data-ttu-id="34334-123">Uruchom ponownie CollectD i Agent pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="34334-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-tooforward-data"></a><span data-ttu-id="34334-124">Konfigurowanie CollectD tooforward danych</span><span class="sxs-lookup"><span data-stu-id="34334-124">Configure CollectD tooforward data</span></span> 

1. <span data-ttu-id="34334-125">tooroute CollectD danych toohello Agent pakietu OMS dla systemu Linux `oms.conf` toobe potrzeb dodane przez tooCollectD katalogu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="34334-125">tooroute CollectD data toohello OMS Agent for Linux, `oms.conf` needs toobe added tooCollectD's configuration directory.</span></span> <span data-ttu-id="34334-126">docelowy Hello tego pliku zależy od hello Linux distro komputera.</span><span class="sxs-lookup"><span data-stu-id="34334-126">hello destination of this file depends on hello Linux  distro of your machine.</span></span>

    <span data-ttu-id="34334-127">Jeśli w katalogu config CollectD znajduje się w /etc/collectd.d/:</span><span class="sxs-lookup"><span data-stu-id="34334-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="34334-128">Jeśli w katalogu config CollectD znajduje się w /etc/collectd/collectd.conf.d/:</span><span class="sxs-lookup"><span data-stu-id="34334-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="34334-129">Dla wersji CollectD przed 5.5 będzie mieć tagi hello toomodify `oms.conf` zgodnie z powyższym.</span><span class="sxs-lookup"><span data-stu-id="34334-129">For CollectD versions before 5.5 you will have toomodify hello tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="34334-130">Skopiuj katalog konfiguracji omsagent collectd.conf toohello potrzeby roboczym.</span><span class="sxs-lookup"><span data-stu-id="34334-130">Copy collectd.conf toohello desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="34334-131">Uruchom ponownie CollectD i Agent pakietu OMS dla systemu Linux z hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="34334-131">Restart CollectD and OMS Agent for Linux with hello following commands.</span></span>

    <span data-ttu-id="34334-132">ponowne uruchomienie sudo usługi collectd ponownego uruchomienia operacji sudo /opt/microsoft/omsagent/bin/service_control</span><span class="sxs-lookup"><span data-stu-id="34334-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a><span data-ttu-id="34334-133">CollectD metryki tooLog konwersja schematu analityka</span><span class="sxs-lookup"><span data-stu-id="34334-133">CollectD metrics tooLog Analytics schema conversion</span></span>
<span data-ttu-id="34334-134">toomaintain znanego modelu między metryki infrastruktury już zebrane przez agenta pakietu OMS dla systemów Linux i hello nowe metryki zebrane przez CollectD następującego mapowania schematu hello jest używany:</span><span class="sxs-lookup"><span data-stu-id="34334-134">toomaintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and hello new metrics collected by CollectD hello following schema mapping is used:</span></span>

| <span data-ttu-id="34334-135">Metryka CollectD pola</span><span class="sxs-lookup"><span data-stu-id="34334-135">CollectD Metric field</span></span> | <span data-ttu-id="34334-136">Pole analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="34334-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="34334-137">Host</span><span class="sxs-lookup"><span data-stu-id="34334-137">host</span></span> | <span data-ttu-id="34334-138">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="34334-138">Computer</span></span> |
| <span data-ttu-id="34334-139">Wtyczki</span><span class="sxs-lookup"><span data-stu-id="34334-139">plugin</span></span> | <span data-ttu-id="34334-140">Brak</span><span class="sxs-lookup"><span data-stu-id="34334-140">None</span></span> |
| <span data-ttu-id="34334-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="34334-141">plugin_instance</span></span> | <span data-ttu-id="34334-142">Nazwa wystąpienia</span><span class="sxs-lookup"><span data-stu-id="34334-142">Instance Name</span></span><br><span data-ttu-id="34334-143">Jeśli **plugin_instance** jest *null* następnie InstanceName = "*_Total*"</span><span class="sxs-lookup"><span data-stu-id="34334-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="34334-144">type</span><span class="sxs-lookup"><span data-stu-id="34334-144">type</span></span> | <span data-ttu-id="34334-145">Nazwa obiektu</span><span class="sxs-lookup"><span data-stu-id="34334-145">ObjectName</span></span> |
| <span data-ttu-id="34334-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="34334-146">type_instance</span></span> | <span data-ttu-id="34334-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="34334-147">CounterName</span></span><br><span data-ttu-id="34334-148">Jeśli **type_instance** jest *null* następnie CounterName =**puste**</span><span class="sxs-lookup"><span data-stu-id="34334-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="34334-149">[dsnames]</span><span class="sxs-lookup"><span data-stu-id="34334-149">dsnames[]</span></span> | <span data-ttu-id="34334-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="34334-150">CounterName</span></span> |
| <span data-ttu-id="34334-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="34334-151">dstypes</span></span> | <span data-ttu-id="34334-152">Brak</span><span class="sxs-lookup"><span data-stu-id="34334-152">None</span></span> |
| <span data-ttu-id="34334-153">wartości]</span><span class="sxs-lookup"><span data-stu-id="34334-153">values[]</span></span> | <span data-ttu-id="34334-154">Równowartości</span><span class="sxs-lookup"><span data-stu-id="34334-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="34334-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="34334-155">Next steps</span></span>
* <span data-ttu-id="34334-156">Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) tooanalyze hello dane zebrane ze źródeł danych i rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="34334-156">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="34334-157">Użyj [pola niestandardowe](log-analytics-custom-fields.md) tooparse danych z rekordów dziennika systemowego do poszczególnych pól.</span><span class="sxs-lookup"><span data-stu-id="34334-157">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>

