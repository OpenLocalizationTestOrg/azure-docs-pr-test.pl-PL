---
title: "aaaCollect i analizować komunikaty dziennika systemowego w OMS Log Analytics | Dokumentacja firmy Microsoft"
description: "SYSLOG jest protokół rejestrowania zdarzeń, który jest tooLinux wspólnej. W tym artykule opisano, jak tooconfigure kolekcję komunikatów Syslog w analizy dzienników i szczegóły rekordów hello tworzą w repozytorium OMS hello."
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
ms.date: 07/12/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 8bfa0bca3f2f18287d1352c98bbaa2a70e41e276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a>SYSLOG źródeł danych w analizy dzienników
SYSLOG jest protokół rejestrowania zdarzeń, który jest tooLinux wspólnej.  Aplikacje będą wysyłać wiadomości, które mogą być przechowywane na komputerze lokalnym hello lub dostarczony moduł zbierający Syslog tooa.  Po zainstalowaniu hello Agent pakietu OMS dla systemu Linux, konfiguruje hello Syslog demon tooforward wiadomości toohello agent lokalny.  Witaj agent wysyła następnie tooLog wiadomość hello Analytics której zostaje utworzony rekord odpowiedniego hello OMS repozytorium.  

> [!NOTE]
> Analiza dzienników obsługuje kolekcji komunikatów wysłanych przez rsyslog lub syslog ng, gdzie rsyslog jest hello demon domyślne. demon syslog domyślne Hello w wersji 5 (sysklog) w wersji Red Hat Enterprise Linux, CentOS i Oracle Linux nie jest obsługiwana dla zbierania zdarzeń usługi syslog. Witaj toocollect syslog danych z tej wersji tych dystrybucji [demon rsyslog](http://rsyslog.com) powinien być zainstalowany i skonfigurowany tooreplace sysklog.
>
>

![Kolekcja SYSLOG](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a>Konfigurowanie usługi Syslog
Hello Agent pakietu OMS dla systemu Linux są zbierane zdarzenia za pomocą urządzeń hello i ważności, które są określone w konfiguracji.  Syslog można skonfigurować za pośrednictwem portalu OMS hello lub przez zarządzanie plikami konfiguracji na agentów systemu Linux.

### <a name="configure-syslog-in-hello-oms-portal"></a>Konfigurowanie w portalu OMS hello Syslog
Konfigurowanie Syslog z hello [danych menu Ustawienia usługi Analiza dzienników](log-analytics-data-sources.md#configuring-data-sources).  Ta konfiguracja jest dostarczana toohello pliku konfiguracji na każdym agenta systemu Linux.

Można dodać nowego zakładu, wpisując jej nazwę, a następnie klikając polecenie  **+** .  Dla każdego obiektu zostaną zebrane tylko wiadomości powitania wybrane ważności.  Sprawdź hello wag dla obiektu określonego hello, które mają toocollect.  Nie można podać wszelkie dodatkowe kryteria toofilter wiadomości.

![Konfigurowanie usługi Syslog](media/log-analytics-data-sources-syslog/configure.png)

Domyślnie wszystkie zmiany konfiguracji są automatycznie wypychana agentów tooall.  Jeśli chcesz tooconfigure Syslog ręcznie na każdym agenta systemu Linux, usuń zaznaczenie pola hello *Zastosuj poniżej maszyny z systemem Linux toomy konfiguracji*.

### <a name="configure-syslog-on-linux-agent"></a>Skonfiguruj Syslog na agenta systemu Linux
Gdy hello [OMS agent jest zainstalowany na komputerze klienckim Linux](log-analytics-linux-agents.md), instaluje domyślny plik konfiguracji programu syslog definiujący funkcje hello i ważność hello wiadomości, które są zbierane.  Można zmodyfikować tę konfigurację hello toochange pliku.  plik konfiguracji Hello jest różne w zależności od hello Syslog demon, który hello klienta został zainstalowany.

> [!NOTE]
> Edytuj hello syslog konfiguracji, należy ponownie uruchomić demon syslog hello hello zmiany tootake efektu.
>
>

#### <a name="rsyslog"></a>rsyslog
Witaj pliku konfiguracyjnego rsyslog znajduje się w **/etc/rsyslog.d/95-omsagent.conf**.  Poniżej przedstawiono domyślną zawartość.  Umożliwia zbieranie informacji wysyłanych z agenta lokalne powitania dla wszystkich obiektów o poziomie ostrzeżenia lub komunikaty dziennika systemowego.

    kern.warning       @127.0.0.1:25224
    user.warning       @127.0.0.1:25224
    daemon.warning     @127.0.0.1:25224
    auth.warning       @127.0.0.1:25224
    syslog.warning     @127.0.0.1:25224
    uucp.warning       @127.0.0.1:25224
    authpriv.warning   @127.0.0.1:25224
    ftp.warning        @127.0.0.1:25224
    cron.warning       @127.0.0.1:25224
    local0.warning     @127.0.0.1:25224
    local1.warning     @127.0.0.1:25224
    local2.warning     @127.0.0.1:25224
    local3.warning     @127.0.0.1:25224
    local4.warning     @127.0.0.1:25224
    local5.warning     @127.0.0.1:25224
    local6.warning     @127.0.0.1:25224
    local7.warning     @127.0.0.1:25224

Należy usunąć obiekt przez usunięcie jego sekcji hello pliku konfiguracji.  Można ograniczyć hello wag, które są zbierane dla konkretnego obiektu przez zmodyfikowanie wpisu tego obiektu.  Na przykład toolimit hello użytkownika zakładzie toomessages z ważność błędu lub wyższy jaki modyfikuje się tego wiersza toohello pliku konfiguracji hello następujące:

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a>SYSLOG ng
plik konfiguracji Hello syslog ng jest lokalizacji **/etc/syslog-ng/syslog-ng.conf**.  Poniżej przedstawiono domyślną zawartość.  Umożliwia zbieranie informacji wysyłanych z agenta lokalne powitania dla wszystkich urządzeń i wszystkich wag komunikaty dziennika systemowego.   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

Należy usunąć obiekt przez usunięcie jego sekcji hello pliku konfiguracji.  Można ograniczyć hello wag, które są zbierane dla konkretnego obiektu, usuwając je z listy.  Na przykład toolimit hello użytkownika zakładzie toojust komunikaty alertów i krytycznego, jaki modyfikuje tej sekcji toohello pliku konfiguracji hello następujące:

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a>Zbieranie danych z dodatkowych portów usługi Syslog
agent pakietu OMS Hello odbiera komunikaty dziennika systemowego na powitania klienta lokalnego na porcie 25224.  Po zainstalowaniu agenta hello domyślnej konfiguracji programu syslog jest stosowane i znaleźć w następującej lokalizacji hello:

* Rsyslog:`/etc/rsyslog.d/95-omsagent.conf`
* SYSLOG ng:`/etc/syslog-ng/syslog-ng.conf`

Można zmienić numer portu hello przez utworzenie dwóch plików konfiguracyjnych: FluentD pliku konfiguracji i pliku ng rsyslog lub syslog, w zależności od demon Syslog hello został zainstalowany.  

* plik konfiguracji FluentD Hello powinien być nowy plik znajduje się w: `/etc/opt/microsoft/omsagent/conf/omsagent.d` i zastąp wartość hello w hello **portu** wpis o numer portu niestandardowego.

        <source>
          type syslog
          port %SYSLOG_PORT%
          bind 127.0.0.1
          protocol_type udp
          tag oms.syslog
        </source>
        <filter oms.syslog.**>
          type filter_syslog
        </filter>

* Rsyslog, należy utworzyć plik konfiguracji znajduje się w: `/etc/rsyslog.d/` i Zastąp hello wartość % SYSLOG_PORT numer portu niestandardowego.  

    > [!NOTE]
    > Jeśli zmodyfikujesz tę wartość w pliku konfiguracyjnym hello `95-omsagent.conf`, zostaną zastąpione, gdy hello agent dotyczy konfiguracji domyślnej.
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* Hello config syslog ng powinno zostać zmodyfikowane przez skopiowanie hello Przykładowa konfiguracja pokazano poniżej i dodawanie toohello zmodyfikowane ustawienia niestandardowe hello koniec pliku konfiguracji syslog ng.conf hello znajduje się w `/etc/syslog-ng/`.  Czy **nie** Użyj etykiety domyślnej hello **% WORKSPACE_ID % _oms** lub **% WORKSPACE_ID_OMS**, zdefiniować niestandardowe etykiety toohelp odróżnić zmiany.  

    > [!NOTE]
    > Jeśli zmodyfikujesz hello domyślne wartości w pliku konfiguracyjnym hello, zostaną one zastąpione gdy hello agent dotyczy konfiguracji domyślnej.
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

Po zakończeniu zmiany hello, hello Syslog i hello usługę agenta musi ponownie uruchomić toobe tooensure hello konfiguracji zmiany zaczęły obowiązywać.   

## <a name="syslog-record-properties"></a>Właściwości rekordu dziennika systemowego
Rekordy dziennika systemowego zawiera typu **Syslog** i mają właściwości hello w hello w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| Computer (Komputer) |Komputer, który hello zdarzeń zostały zebrane. |
| Funkcje |Definiuje hello częścią systemu hello, który wygenerował wiadomość hello. |
| HostIP |Adres IP systemu hello wysyłania wiadomości powitania. |
| Nazwa hosta |Nazwa systemu hello wysyłania wiadomości powitania. |
| Poziom ważności |Poziom ważności hello zdarzenia. |
| SyslogMessage |Tekst wiadomości powitania. |
| Identyfikator procesu |Identyfikator procesu hello, który wygenerował wiadomość hello. |
| eventTime |Data i godzina hello zdarzeń został wygenerowany. |

## <a name="log-queries-with-syslog-records"></a>Dziennik zapytań dotyczących rekordów dziennika systemowego
Witaj poniższej tabeli przedstawiono różne przykłady dziennika zapytań, które pobierają rekordy dziennika systemowego.

| Zapytanie | Opis |
|:--- |:--- |
| Typ = Syslog |Wszystkie audyt dzienników systemowych. |
| Typ = poziom ważności Syslog = błąd |Wszystkie rekordy dziennika systemowego o ważności błędu. |
| Typ = Syslog &#124; count() miary w przeliczeniu na komputer |Liczba Syslog rejestruje przez komputer. |
| Typ = Syslog &#124; Miara count() przez funkcje |Liczba Syslog rejestruje przez funkcje. |

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie hello powyżej zapytania spowoduje zmianę następujących toohello.

> | Zapytanie | Opis |
|:--- |:--- |
| Dziennik systemu |Wszystkie audyt dzienników systemowych. |
| SYSLOG &#124; gdy poziom ważności == "error" |Wszystkie rekordy dziennika systemowego o ważności błędu. |
| SYSLOG &#124; Podsumuj AggregatedValue = count() przez komputer |Liczba Syslog rejestruje przez komputer. |
| SYSLOG &#124; Podsumuj AggregatedValue = count() przez funkcje |Liczba Syslog rejestruje przez funkcje. |

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) tooanalyze hello dane zebrane ze źródeł danych i rozwiązań.
* Użyj [pola niestandardowe](log-analytics-custom-fields.md) tooparse danych z rekordów dziennika systemowego do poszczególnych pól.
* [Konfigurowanie agentów systemu Linux](log-analytics-linux-agents.md) toocollect innych typów danych.
