---
title: Zbieraj alerty Nagios i Zabbix w OMS Log Analytics | Dokumentacja firmy Microsoft
description: "Nagios i Zabbix są typu open source, narzędzia do monitorowania. Alerty można zbierać z tych narzędzi do analizy dzienników w celu przeanalizowania wraz z alertów z innych źródeł.  W tym artykule opisano sposób konfigurowania agenta pakietu OMS dla systemu Linux zbierać alerty z tych systemów."
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
ms.openlocfilehash: 0b64c32e1031e704d50aab0b38eaea41e27d134b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a>Zbieraj alerty z Nagios i Zabbix w Log Analytics z usługą OMS agenta dla systemu Linux 
[Nagios](https://www.nagios.org/) i [Zabbix](http://www.zabbix.com/) są typu open source, narzędzia do monitorowania.  Można zbierać alerty z tych narzędzi do analizy dzienników w celu przeanalizowania wraz z [alertów z innych źródeł](log-analytics-alerts.md).  W tym artykule opisano sposób konfigurowania agenta pakietu OMS dla systemu Linux zbierać alerty z tych systemów.
 
## <a name="configure-alert-collection"></a>Konfigurowanie zbierania alertów

### <a name="configuring-nagios-alert-collection"></a>Konfigurowanie zbierania alertów Nagios
Wykonaj następujące czynności na serwerze Nagios do zbierania alertów.

1. Przyznaj użytkownikowi **omsagent** dostęp do odczytu do pliku dziennika Nagios (tj. `/var/log/nagios/nagios.log`). Zakładając, że plik nagios.log jest właścicielem grupy `nagios`, można dodać użytkownika **omsagent** do **nagios** grupy. 

    sudo usermod - -G nagios omsagent

2.  Modyfikowanie pliku konfiguracji na (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Upewnij się, że następujące wpisy są obecne i nie komentarze wychodzących:  

        <source>  
          type tail  
          #Update path to point to your nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. Uruchom ponownie demona omsagent

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a>Konfigurowanie zbierania alertów Zabbix
Aby zbierać alerty z serwera Zabbix, należy określić użytkownika i hasło w *zwykły tekst*. Nie jest to idealne rozwiązanie, ale zalecamy, aby utworzyć użytkownika, a następnie udzielić uprawnień, aby monitorować onlu.

Wykonaj następujące czynności na serwerze Nagios do zbierania alertów.

1. Modyfikowanie pliku konfiguracji na (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Upewnij się, że następujące wpisy są obecne i nie komentarze wychodzących.  Zmień wartości w danym środowisku Zabbix nazwy użytkownika i hasła.

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. Uruchom ponownie demona omsagent

    sudo sh /opt/microsoft/omsagent/bin/service_control ponownego uruchomienia


## <a name="alert-records"></a>Rejestruje alertu
Rejestruje alertu można pobrać z Nagios i Zabbix przy użyciu [dziennika wyszukiwania](log-analytics-log-searches.md) w analizy dzienników.

### <a name="nagios-alert-records"></a>Rejestruje Nagios Alert

Alert ma rekordy zebrane przez Nagios **typu** z **alertu** i **SourceSystem** z **Nagios**.  Mają one właściwości w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| Typ |*Alert* |
| SourceSystem |*Nagios* |
| AlertName |Nazwa alertu. |
| AlertDescription | Opis alertu. |
| Stan alertu | Stan usługi lub hosta.<br><br>OK<br>OSTRZEŻENIE<br>W GÓRĘ<br>W DÓŁ |
| Nazwa hosta | Nazwa hosta, który utworzony alert. |
| PriorityNumber | Poziom priorytetu alertu. |
| StateType | Typ stanu alertu.<br><br>SOFT - problem, który nie został zresetowany.<br>TWARDE — problem, który został zresetowany przez określoną liczbę razy.  |
| TimeGenerated |Data i godzina utworzenia alertu. |


### <a name="zabbix-alert-records"></a>Rejestruje alertu Zabbix
Alert ma rekordy zebrane przez Zabbix **typu** z **alertu** i **SourceSystem** z **Zabbix**.  Mają one właściwości w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| Typ |*Alert* |
| SourceSystem |*Zabbix* |
| AlertName | Nazwa alertu. |
| AlertPriority | Ważność alertu.<br><br>nie sklasyfikowane<br>Informacje<br>Ostrzeżenie<br>Średnia<br>Wysoka<br>po awarii  |
| Stan alertu | Stan alertu.<br><br>0 — stan jest aktualny.<br>1 — stan jest nieznany.  |
| AlertTypeNumber | Określa, czy alert może wygenerować wiele zdarzeń problem.<br><br>0 — stan jest aktualny.<br>1 — stan jest nieznany.    |
| Komentarze | Dodatkowe uwagi o alercie. |
| Nazwa hosta | Nazwa hosta, który utworzony alert. |
| PriorityNumber | Wartość wskazująca, ważność alertu.<br><br>0 — nie sklasyfikowane<br>1 — informacje<br>2 — ostrzeżenie<br>3 — średnia<br>4 - Wysoka<br>5 — po awarii |
| TimeGenerated |Data i godzina utworzenia alertu. |
| TimeLastModified |Data i godzina ostatniej zmiany stanu alertu. |


## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [alerty](log-analytics-alerts.md) w analizy dzienników.
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) analizować dane zebrane ze źródeł danych i rozwiązania. 
