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
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a>Zbieranie danych z CollectD na agentach systemu Linux w analizy dzienników
[CollectD](https://collectd.org/) jest demonów systemu Linux typu open source, która okresowo gromadzi metryki wydajności z aplikacji i informacji o poziomie systemu. Przykładowe aplikacje obejmują hello maszyny wirtualnej Java (JVM), serwer MySQL i Nginx. Ten artykuł zawiera informacje dotyczące zbierania danych wydajności z CollectD w analizy dzienników.

Pełną listę dostępnych wtyczek można znaleźć w folderze [tabeli wtyczek](https://collectd.org/wiki/index.php/Table_of_Plugins).

![Omówienie CollectD](media/log-analytics-data-sources-collectd/overview.png)

Witaj następującej konfiguracji CollectD znajduje się w hello Agent pakietu OMS dla systemu Linux tooroute CollectD danych toohello Agent pakietu OMS dla systemu Linux.

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

Ponadto jeśli używane wersje collectD przed powitania po konfiguracji zamiast tego użyj 5.5.

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

Konfiguracja CollectD Hello korzysta z domyślnego hello`write_http` danych metryki wydajności toosend wtyczki za pośrednictwem portu 26000 tooOMS agenta dla systemu Linux. 

> [!NOTE]
> Ten port może być skonfigurowany tooa niestandardowy port, w razie potrzeby.

Witaj Agent pakietu OMS dla systemu Linux również nasłuchuje na porcie 26000 dla metryki CollectD, a następnie konwertuje je tooOMS schematu metryki. Witaj Oto hello Agent pakietu OMS dla konfiguracji systemu Linux `collectd.conf`.

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a>Obsługiwane wersje
- Analiza dzienników obsługuje obecnie CollectD wersji 4.8 i powyżej.
- Dla kolekcji metryki CollectD wymagany jest Agent pakietu OMS dla systemu Linux v1.1.0-217 lub nowszym.


## <a name="configuration"></a>Konfiguracja
Witaj poniżej przedstawiono podstawowe czynności tooconfigure zbierania danych CollectD w analizy dzienników.

1. Skonfiguruj CollectD toosend danych toohello Agent pakietu OMS dla systemu Linux przy użyciu wtyczki write_http hello.  
2. Skonfiguruj hello Agent pakietu OMS dla systemu Linux toolisten dla hello CollectD danych na powitania odpowiedni port.
3. Uruchom ponownie CollectD i Agent pakietu OMS dla systemu Linux.

### <a name="configure-collectd-tooforward-data"></a>Konfigurowanie CollectD tooforward danych 

1. tooroute CollectD danych toohello Agent pakietu OMS dla systemu Linux `oms.conf` toobe potrzeb dodane przez tooCollectD katalogu konfiguracji. docelowy Hello tego pliku zależy od hello Linux distro komputera.

    Jeśli w katalogu config CollectD znajduje się w /etc/collectd.d/:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    Jeśli w katalogu config CollectD znajduje się w /etc/collectd/collectd.conf.d/:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    >Dla wersji CollectD przed 5.5 będzie mieć tagi hello toomodify `oms.conf` zgodnie z powyższym.
    >

2. Skopiuj katalog konfiguracji omsagent collectd.conf toohello potrzeby roboczym.

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. Uruchom ponownie CollectD i Agent pakietu OMS dla systemu Linux z hello następujące polecenia.

    ponowne uruchomienie sudo usługi collectd ponownego uruchomienia operacji sudo /opt/microsoft/omsagent/bin/service_control

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a>CollectD metryki tooLog konwersja schematu analityka
toomaintain znanego modelu między metryki infrastruktury już zebrane przez agenta pakietu OMS dla systemów Linux i hello nowe metryki zebrane przez CollectD następującego mapowania schematu hello jest używany:

| Metryka CollectD pola | Pole analizy dzienników |
|:--|:--|
| Host | Computer (Komputer) |
| Wtyczki | Brak |
| plugin_instance | Nazwa wystąpienia<br>Jeśli **plugin_instance** jest *null* następnie InstanceName = "*_Total*" |
| type | Nazwa obiektu |
| type_instance | CounterName<br>Jeśli **type_instance** jest *null* następnie CounterName =**puste** |
| [dsnames] | CounterName |
| dstypes | Brak |
| wartości] | Równowartości |

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) tooanalyze hello dane zebrane ze źródeł danych i rozwiązań. 
* Użyj [pola niestandardowe](log-analytics-custom-fields.md) tooparse danych z rekordów dziennika systemowego do poszczególnych pól.

