---
title: "Zbieranie danych niestandardowych JSON w OMS analizy dzienników | Dokumentacja firmy Microsoft"
description: "Mogą być zbierane niestandardowych źródeł danych JSON do analizy dzienników dla systemu Linux przy użyciu agenta pakietu OMS.  Te źródła danych niestandardowych można proste skrypty zwracanie JSON, takie jak curl lub jednego z jego FluentD 300 + wtyczek. W tym artykule opisano konfiguracja wymagana dla tej kolekcji danych."
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
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 800ee1269556e7c2d56fbbf2b497c10509b5c78c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="collecting-custom-json-data-sources-with-the-oms-agent-for-linux-in-log-analytics"></a><span data-ttu-id="10909-105">Zbieranie niestandardowych źródeł danych JSON z agentem pakietu OMS dla systemu Linux w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="10909-105">Collecting custom JSON data sources with the OMS Agent for Linux in Log Analytics</span></span>
<span data-ttu-id="10909-106">Mogą być zbierane niestandardowych źródeł danych JSON do analizy dzienników dla systemu Linux przy użyciu agenta pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="10909-106">Custom JSON data sources can be collected into Log Analytics using the OMS Agent for Linux.</span></span>  <span data-ttu-id="10909-107">Te źródła danych niestandardowych mogą być proste skrypty, takie jak zwracanie JSON [curl](https://curl.haxx.se/) lub jednego z [w FluentD 300 + wtyczek](http://www.fluentd.org/plugins/all).</span><span class="sxs-lookup"><span data-stu-id="10909-107">These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all).</span></span> <span data-ttu-id="10909-108">W tym artykule opisano konfiguracja wymagana dla tej kolekcji danych.</span><span class="sxs-lookup"><span data-stu-id="10909-108">This article describes the configuration required for this data collection.</span></span>

> [!NOTE]
> <span data-ttu-id="10909-109">Agent pakietu OMS dla systemu Linux v1.1.0-217 + jest wymagana dla danych JSON niestandardowe</span><span class="sxs-lookup"><span data-stu-id="10909-109">OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data</span></span>

## <a name="configuration"></a><span data-ttu-id="10909-110">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="10909-110">Configuration</span></span>

### <a name="configure-input-plugin"></a><span data-ttu-id="10909-111">Skonfiguruj wtyczkę wejściowych</span><span class="sxs-lookup"><span data-stu-id="10909-111">Configure input plugin</span></span>

<span data-ttu-id="10909-112">Aby zbierać dane JSON w analizy dzienników, Dodaj `oms.api.` na początku tag FluentD w wejściowych wtyczki.</span><span class="sxs-lookup"><span data-stu-id="10909-112">To collect JSON data in Log Analytics, add `oms.api.` to the start of a FluentD tag in an input plugin.</span></span>

<span data-ttu-id="10909-113">Na przykład poniżej przedstawiono plik konfiguracji oddzielnych `exec-json.conf` w `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span><span class="sxs-lookup"><span data-stu-id="10909-113">For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span></span>  <span data-ttu-id="10909-114">Używa wtyczki FluentD `exec` do uruchamiania polecenia curl co 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="10909-114">This uses the FluentD plugin `exec` to run a curl command every 30 seconds.</span></span>  <span data-ttu-id="10909-115">Dane wyjściowe tego polecenia są zbierane przez wtyczkę dane wyjściowe JSON.</span><span class="sxs-lookup"><span data-stu-id="10909-115">The output from this command is collected by the JSON output plugin.</span></span>

```
<source>
  type exec
  command 'curl localhost/json.output'
  format json
  tag oms.api.httpresponse
  run_interval 30s
</source>

<match oms.api.httpresponse>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api_httpresponse*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```
<span data-ttu-id="10909-116">Plik konfiguracji dodany w obszarze `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` trzeba mieć własność zmienić przy użyciu następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="10909-116">The configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require to have its ownership changed with the following command.</span></span>

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a><span data-ttu-id="10909-117">Skonfiguruj wtyczkę danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="10909-117">Configure output plugin</span></span> 
<span data-ttu-id="10909-118">Dodaj następującą konfigurację wtyczki dane wyjściowe do konfiguracji głównego w `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` lub plik konfiguracji oddzielne wprowadzanych w`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span><span class="sxs-lookup"><span data-stu-id="10909-118">Add the following output plugin configuration to the main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span></span>

```
<match oms.api.**>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```

### <a name="restart-oms-agent-for-linux"></a><span data-ttu-id="10909-119">Uruchom ponownie agenta pakietu OMS dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="10909-119">Restart OMS Agent for Linux</span></span>
<span data-ttu-id="10909-120">Uruchom ponownie agenta pakietu OMS usługi systemu Linux przy użyciu następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="10909-120">Restart the OMS Agent for Linux service with the following command.</span></span>

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a><span data-ttu-id="10909-121">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="10909-121">Output</span></span>
<span data-ttu-id="10909-122">Dane zostaną zebrane w analizy dzienników z typem rekordu `<FLUENTD_TAG>_CL`.</span><span class="sxs-lookup"><span data-stu-id="10909-122">The data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.</span></span>

<span data-ttu-id="10909-123">Na przykład niestandardowe tag `tag oms.api.tomcat` w analizy dzienników z typem rekordu `tomcat_CL`.</span><span class="sxs-lookup"><span data-stu-id="10909-123">For example, the custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.</span></span>  <span data-ttu-id="10909-124">Można pobrać wszystkie rekordy tego typu z następujących wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="10909-124">You could retrieve all records of this type with the following log search.</span></span>

    Type=tomcat_CL

<span data-ttu-id="10909-125">Zagnieżdżone dane JSON źródeł, są obsługiwane, ale są indeksowane na podstawie pola nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="10909-125">Nested JSON data sources are supported, but are indexed based off of parent field.</span></span> <span data-ttu-id="10909-126">Na przykład następujące dane JSON jest zwracana z analizy dzienników wyszukiwanie jako `tag_s : "[{ "a":"1", "b":"2" }]`.</span><span class="sxs-lookup"><span data-stu-id="10909-126">For example, the following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.</span></span>

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a><span data-ttu-id="10909-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="10909-127">Next steps</span></span>
* <span data-ttu-id="10909-128">Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) analizować dane zebrane ze źródeł danych i rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="10909-128">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
 