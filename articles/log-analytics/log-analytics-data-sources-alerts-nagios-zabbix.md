---
title: alerty Nagios i Zabbix aaaCollect w OMS Log Analytics | Dokumentacja firmy Microsoft
description: "Nagios i Zabbix są typu open source, narzędzia do monitorowania. Można zebrać alertów z tych narzędzi do analizy dzienników w kolejności tooanalyze je wraz z alertów z innych źródeł.  W tym artykule opisano, jak tooconfigure hello Agent pakietu OMS dla systemu Linux toocollect alerty z tych systemów."
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
ms.openlocfilehash: 23e2252e4fed8bc87baec063694a8472ca84220d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a>Zbieraj alerty z Nagios i Zabbix w Log Analytics z usługą OMS agenta dla systemu Linux 
[Nagios](https://www.nagios.org/) i [Zabbix](http://www.zabbix.com/) są typu open source, narzędzia do monitorowania.  Można zebrać alertów z tych narzędzi do analizy dzienników w kolejności tooanalyze je wraz z [alertów z innych źródeł](log-analytics-alerts.md).  W tym artykule opisano, jak tooconfigure hello Agent pakietu OMS dla systemu Linux toocollect alerty z tych systemów.
 
## <a name="configure-alert-collection"></a>Konfigurowanie zbierania alertów

### <a name="configuring-nagios-alert-collection"></a>Konfigurowanie zbierania alertów Nagios
Wykonaj następujące kroki na alerty toocollect serwera Nagios hello hello.

1. Udziel hello użytkownika **omsagent** pliku dziennika Nagios toohello dostęp do odczytu (tj. `/var/log/nagios/nagios.log`). Zakładając, że plik nagios.log hello jest własnością grupy hello `nagios`, można dodać użytkownika hello **omsagent** toohello **nagios** grupy. 

    sudo usermod - -G nagios omsagent

2.  Modyfikowanie pliku konfiguracji hello w (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Upewnij się, że hello następujące wpisy są obecne i nie komentarze wychodzących:  

        <source>  
          type tail  
          #Update path toopoint tooyour nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. Uruchom ponownie demon omsagent hello

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a>Konfigurowanie zbierania alertów Zabbix
toocollect alertów z serwera Zabbix, należy toospecify użytkownika i hasło w *zwykły tekst*. Nie jest to idealne rozwiązanie, ale zaleca się utworzenie użytkownika hello i przyznać uprawnienia toomonitor onlu.

Wykonaj następujące kroki na alerty toocollect serwera Nagios hello hello.

1. Modyfikowanie pliku konfiguracji hello w (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Upewnij się, że hello następujące wpisy są obecne i nie komentarze wychodzących.  Zmień hello toovalues nazwę i hasło użytkownika w danym środowisku Zabbix.

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. Uruchom ponownie demon omsagent hello

    sudo sh /opt/microsoft/omsagent/bin/service_control ponownego uruchomienia


## <a name="alert-records"></a>Rejestruje alertu
Rejestruje alertu można pobrać z Nagios i Zabbix przy użyciu [dziennika wyszukiwania](log-analytics-log-searches.md) w analizy dzienników.

### <a name="nagios-alert-records"></a>Rejestruje Nagios Alert

Alert ma rekordy zebrane przez Nagios **typu** z **alertu** i **SourceSystem** z **Nagios**.  Mają one właściwości hello w hello w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| Typ |*Alert* |
| SourceSystem |*Nagios* |
| AlertName |Nazwa alertu hello. |
| AlertDescription | Opis alertu hello. |
| Stan alertu | Stan usługi hello lub hosta.<br><br>OK<br>OSTRZEŻENIE<br>W GÓRĘ<br>W DÓŁ |
| Nazwa hosta | Nazwa hosta hello, utworzony hello alert. |
| PriorityNumber | Poziom priorytetu hello alertu. |
| StateType | Typ Hello stanu hello alertu.<br><br>SOFT - problem, który nie został zresetowany.<br>TWARDE — problem, który został zresetowany przez określoną liczbę razy.  |
| TimeGenerated |Data i godzina hello alert został utworzony. |


### <a name="zabbix-alert-records"></a>Rejestruje alertu Zabbix
Alert ma rekordy zebrane przez Zabbix **typu** z **alertu** i **SourceSystem** z **Zabbix**.  Mają one właściwości hello w hello w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| Typ |*Alert* |
| SourceSystem |*Zabbix* |
| AlertName | Nazwa alertu hello. |
| AlertPriority | Ważność alertu hello.<br><br>nie sklasyfikowane<br>Informacje<br>Ostrzeżenie<br>Średnia<br>Wysoka<br>po awarii  |
| Stan alertu | Stan alertu hello.<br><br>0 — stan działa toodate.<br>1 — stan jest nieznany.  |
| AlertTypeNumber | Określa, czy alert może wygenerować wiele zdarzeń problem.<br><br>0 — stan działa toodate.<br>1 — stan jest nieznany.    |
| Komentarze | Dodatkowe uwagi o alercie. |
| Nazwa hosta | Nazwa hosta hello, utworzony hello alert. |
| PriorityNumber | Wartość wskazująca, ważność alertu hello.<br><br>0 — nie sklasyfikowane<br>1 — informacje<br>2 — ostrzeżenie<br>3 — średnia<br>4 - Wysoka<br>5 — po awarii |
| TimeGenerated |Data i godzina hello alert został utworzony. |
| TimeLastModified |Data i godzina stan hello hello alert został ostatnio zmieniony. |


## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [alerty](log-analytics-alerts.md) w analizy dzienników.
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) tooanalyze hello dane zebrane ze źródeł danych i rozwiązań. 
