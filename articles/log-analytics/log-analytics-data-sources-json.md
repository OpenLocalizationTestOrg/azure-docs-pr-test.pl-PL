---
title: niestandardowe dane JSON aaaCollecting w OMS Log Analytics | Dokumentacja firmy Microsoft
description: "Mogą być zbierane niestandardowych źródeł danych JSON do analizy dzienników dla systemu Linux przy użyciu hello Agent pakietu OMS.  Te źródła danych niestandardowych można proste skrypty zwracanie JSON, takie jak curl lub jednego z jego FluentD 300 + wtyczek. W tym artykule opisano hello konfiguracja wymagana dla tej kolekcji danych."
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
ms.openlocfilehash: 97d401408a8c206d4a9ef2ec9b13ba1ca6b5e92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a>Zbieranie niestandardowych źródeł danych JSON z hello Agent pakietu OMS dla systemu Linux w analizy dzienników
Mogą być zbierane niestandardowych źródeł danych JSON do analizy dzienników dla systemu Linux przy użyciu hello Agent pakietu OMS.  Te źródła danych niestandardowych mogą być proste skrypty, takie jak zwracanie JSON [curl](https://curl.haxx.se/) lub jednego z [w FluentD 300 + wtyczek](http://www.fluentd.org/plugins/all). W tym artykule opisano hello konfiguracja wymagana dla tej kolekcji danych.

> [!NOTE]
> Agent pakietu OMS dla systemu Linux v1.1.0-217 + jest wymagana dla danych JSON niestandardowe

## <a name="configuration"></a>Konfiguracja

### <a name="configure-input-plugin"></a>Skonfiguruj wtyczkę wejściowych

Dodaj dane JSON toocollect w analizy dzienników `oms.api.` toohello początku tag FluentD w wejściowych wtyczki.

Na przykład poniżej przedstawiono plik konfiguracji oddzielnych `exec-json.conf` w `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.  Używa wtyczki FluentD hello `exec` toorun polecenia curl co 30 sekund.  dane wyjściowe tego polecenia Hello są zbierane przez wtyczkę dane wyjściowe JSON hello.

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
dodawane w pliku konfiguracji Hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` będzie wymagać toohave zmienić własność z hello następujące polecenia.

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a>Skonfiguruj wtyczkę danych wyjściowych 
Dodaj hello następujące dane wyjściowe wtyczki toohello głównego Konfiguracja w `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` lub plik konfiguracji oddzielne wprowadzanych w`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`

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

### <a name="restart-oms-agent-for-linux"></a>Uruchom ponownie agenta pakietu OMS dla systemu Linux
Uruchom ponownie hello Agent pakietu OMS dla systemu Linux usługi z hello następujące polecenia.

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a>Dane wyjściowe
Witaj dane będą zbierane w analizy dzienników z typem rekordu `<FLUENTD_TAG>_CL`.

Na przykład Witaj niestandardowy `tag oms.api.tomcat` w analizy dzienników z typem rekordu `tomcat_CL`.  Wszystkie rekordy tego typu można pobrać z powitania po wyszukiwania dziennika.

    Type=tomcat_CL

Zagnieżdżone dane JSON źródeł, są obsługiwane, ale są indeksowane na podstawie pola nadrzędnego. Na przykład następujące dane JSON hello zostanie zwrócona przez wyszukiwanie analizy dzienników jako `tag_s : "[{ "a":"1", "b":"2" }]`.

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) tooanalyze hello dane zebrane ze źródeł danych i rozwiązań. 
 