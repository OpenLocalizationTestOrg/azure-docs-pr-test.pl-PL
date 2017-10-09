---
title: "aaaVMware rozwiązania monitorowanie Log Analytics | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat jak hello rozwiązanie monitorowanie VMware może pomóc zarządzania dziennikami i monitorować hostach ESXi."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 16516639-cc1e-465c-a22f-022f3be297f1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: 959d5c2201fc5c7947f8b8870d055cdf9eea8e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="vmware-monitoring-preview-solution-in-log-analytics"></a>VMware monitorowania (wersja zapoznawcza) rozwiązania analizy dzienników

![VMware symbol](./media/log-analytics-vmware/vmware-symbol.png)

Witaj monitorowania VMware rozwiązania analizy dzienników jest rozwiązaniem, które pomaga w utworzeniu centralnego rejestrowania i monitorowania podejście do dużych dzienników VMware. W tym artykule opisano, jak można rozwiązać, przechwytywania i zarządzać hostach ESXi hello w jednej lokalizacji za pomocą rozwiązania hello. Dzięki rozwiązaniu hello widać szczegółowe dane na wszystkich hostach ESXi w jednym miejscu. Widać liczby zdarzeń top, stanu i trendów hostów maszyny Wirtualnej i ESXi realizowane za pośrednictwem dzienniki hosta ESXi hello. Można rozwiązać, wyświetlając i wyszukiwanie scentralizowane dzienniki hosta ESXi. I można tworzyć alerty na podstawie kwerend wyszukiwania dziennika.

rozwiązanie Hello używa funkcji natywnego syslog hello ESXi hosta toopush tooa miejsce docelowe danych maszyny Wirtualnej, którego Agent pakietu OMS. Jednak rozwiązanie hello nie zapisywać pliki na syslog w hello docelowej maszyny Wirtualnej. agent pakietu OMS Hello otwiera port 1514 i nasłuchuje toothis. Po odebraniu danych hello agent pakietu OMS hello wypycha dane hello do OMS.

## <a name="installing-and-configuring-hello-solution"></a>Instalowanie i konfigurowanie hello rozwiązania
Użyj powitania po tooinstall informacji i skonfiguruj hello rozwiązania.

* Dodaj hello monitorowania VMware rozwiązania tooyour obszarem roboczym pakietu OMS za pomocą hello procesu opisanego w [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).

#### <a name="supported-vmware-esxi-hosts"></a>Hosty VMware ESXi obsługiwane
vSphere ESXi 5.5 hosta i 6.0

#### <a name="prepare-a-linux-server"></a>Przygotuj serwer systemu Linux
Utwórz wszystkie dane syslog tooreceive maszyny Wirtualnej systemu Linux na podstawie hostach ESXi hello. Witaj [agenta systemu Linux OMS](log-analytics-linux-agents.md) jest hello kolekcji punktów dla wszystkich danych syslog hosta ESXi. Można użyć wielu ESXi hostów tooforward dzienniki tooa pojedynczego Linux serwera, jak hello poniższy przykład.  

   ![Przepływ usługi SYSLOG](./media/log-analytics-vmware/diagram.png)

### <a name="configure-syslog-collection"></a>Konfigurowanie zbierania syslog
1. Skonfiguruj funkcję przesyłania syslog VSphere. Aby skonfigurować przekazywanie syslog toohelp szczegółowe informacje, zobacz [Konfigurowanie syslog na ESXi 5.x i 6.0 (2003322)](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2003322). Przejdź za**Konfiguracja hosta ESXi** > **oprogramowania** > **Zaawansowane ustawienia** > **Syslog**.
   ![vsphereconfig](./media/log-analytics-vmware/vsphere1.png)  
2. W hello *Syslog.global.logHost* pól, Dodaj swój numer portu systemu Linux, jak serwer i hello *1514*. Na przykład `tcp://hostname:1514` lub`tcp://123.456.789.101:1514`
3. Otwórz zaporę hosta ESXi powitania dla syslog. **Konfiguracja hosta ESXi** > **oprogramowania** > **profil zabezpieczeń** > **zapory** , a następnie otwórz **właściwości**.  

    ![vspherefw](./media/log-analytics-vmware/vsphere2.png)  

    ![vspherefwproperties](./media/log-analytics-vmware/vsphere3.png)  
4. Sprawdź hello vSphere konsoli tooverify, który tego syslog jest poprawnie skonfigurowana. Potwierdzaj hello ten port hosta ESXI **1514** jest skonfigurowany.
5. Pobierz i zainstaluj hello Agent pakietu OMS dla systemu Linux na serwerze Linux hello. Aby uzyskać więcej informacji, zobacz hello [dokumentacji Agent pakietu OMS Linux](https://github.com/Microsoft/OMS-Agent-for-Linux).
6. Po zainstalowaniu hello Agent pakietu OMS dla systemu Linux, przejdź do katalogu /etc/opt/microsoft/omsagent/sysconf/omsagent.d toohello i kopiowania hello vmware_esxi.conf pliku toohello /etc/opt/microsoft/omsagent/conf/omsagent.d katalogu i hello grupy właściciel hello zmiany uprawnienia pliku hello i. Na przykład:

    ```
    sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/vmware_esxi.conf /etc/opt/microsoft/omsagent/conf/omsagent.d
   sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf
    ```
7. Uruchom ponownie hello Agent pakietu OMS dla systemu Linux, uruchamiając `sudo /opt/microsoft/omsagent/bin/service_control restart`.
8. Test hello łączność między serwerem systemu Linux hello i hosta ESXi hello przy użyciu hello `nc` na powitania hosta ESXi. Na przykład:

    ```
    [root@ESXiHost:~] nc -z 123.456.789.101 1514
    Connection too123.456.789.101 1514 port [tcp/*] succeeded!
    ```

9. W portalu OMS hello, wyszukaj dziennika `Type=VMware_CL`. OMS służy do zbierania danych z serwera syslog hello, zachowuje hello formatu syslog. W portalu hello niektórych określonych pól są przechwytywane, takich jak *Hostname* i *ProcessName*.  

    ![type](./media/log-analytics-vmware/type.png)  

    Jeśli wyświetlanie wyników wyszukiwania dziennika są podobne powyższy obraz toohello, gotowe pulpitu nawigacyjnego programu toouse hello monitorowania VMware OMS rozwiązania.  

## <a name="vmware-data-collection-details"></a>Szczegóły pobierania danych VMware
Hello rozwiązanie monitorowanie VMware zbiera różne metryki i dziennika dane dotyczące wydajności z hostach ESXi przy użyciu hello OMS agentów dla systemu Linux, które mają włączone.

Witaj poniższej tabeli przedstawiono metody zbierania danych i inne szczegółowe informacje o jak zbierane są dane.

| Platformy | Agent pakietu OMS dla systemu Linux | Agenta programu SCOM | Azure Storage | SCOM wymagane? | Dane agenta programu SCOM wysyłane za pośrednictwem grupy zarządzania | Częstotliwość kolekcji |
| --- | --- | --- | --- | --- | --- | --- |
| Linux |&#8226; |  |  |  |  |co 3 minuty |

Witaj w poniższej tabeli przedstawiono przykłady pól danych zbieranych przez rozwiązanie monitorowanie VMware hello:

| Nazwa pola | description |
| --- | --- |
| Device_s |Urządzenia magazynujące VMware |
| ESXIFailure_s |typy niepowodzenia |
| EventTime_t |Godzina wystąpienia zdarzenia |
| HostName_s |Nazwa hosta ESXi |
| Operation_s |Tworzenie maszyny Wirtualnej lub usuwanie maszyny Wirtualnej |
| ProcessName_s |Nazwa zdarzenia |
| ResourceId_s |Nazwa hosta VMware hello |
| ResourceLocation_s |VMware |
| ResourceName_s |VMware |
| ResourceType_s |Funkcja Hyper-V |
| SCSIStatus_s |Stan VMware SCSI |
| SyslogMessage_s |Dane dziennika systemowego |
| UserName_s |Użytkownik, który utworzeniu lub usunięciu maszyny Wirtualnej |
| VMName_s |Nazwa maszyny wirtualnej |
| Computer (Komputer) |komputer-host |
| TimeGenerated |dane o czasie hello został wygenerowany. |
| DataCenter_s |Centrum danych VMware |
| StorageLatency_s |Magazyn czas oczekiwania (ms) |

## <a name="vmware-monitoring-solution-overview"></a>Monitorowanie VMware Omówienie rozwiązania
w portalu OMS hello pojawi się Kafelek VMware Hello. Zapewnia widok wysokiego poziomu zakończą się niepowodzeniem. Po kliknięciu kafelka hello, przejdź do widoku pulpitu nawigacyjnego.

![Kafelek](./media/log-analytics-vmware/tile.png)

#### <a name="navigate-hello-dashboard-view"></a>Przejdź do widoku pulpitu nawigacyjnego hello
W hello **VMware** widoku pulpitu nawigacyjnego bloki są zorganizowane według:

* Licznik stan awarii
* Zlicza hosta najwyższego przez zdarzenie
* Liczba zdarzeń TOP
* Działania maszyny wirtualnej
* Zdarzenia dysku hosta ESXi

![solution1](./media/log-analytics-vmware/solutionview1-1.png)

![solution2](./media/log-analytics-vmware/solutionview1-2.png)

Kliknij pozycję Wszystkie tooopen bloku okienko wyszukiwania analizy dzienników, która zawiera szczegółowe informacje specyficzne dla bloku hello.

W tym miejscu można edytować toomodify zapytania wyszukiwania hello go dla określonego elementu. Samouczek dotyczący hello podstawy wyszukiwania OMS, zapoznaj się z hello [OMS dziennik wyszukiwania samouczka.](log-analytics-log-searches.md)

#### <a name="find-esxi-host-events"></a>Znajdź zdarzenia hosta ESXi
Na jednym hoście ESXi generuje wiele dzienników, opartych na ich procesów. Witaj rozwiązanie monitorowanie VMware centralizuje je i zawiera podsumowanie liczby zdarzeń hello. Ten widok scentralizowane pomaga w zrozumieniu którym hoście ESXi ma dużą liczbę zdarzeń i jakie zdarzenia występują najczęściej w danym środowisku.

![Zdarzenia](./media/log-analytics-vmware/events.png)

Można przejść do szczegółów przez kliknięcie przycisku hosta ESXi lub typ zdarzenia.

Po kliknięciu nazwy hosta ESXi, możesz przeglądać informacje z tego hosta ESXi. Wyniki toonarrow z typem zdarzenia hello, należy dodać `“ProcessName_s=EVENT TYPE”` w kwerendzie wyszukiwania. Możesz wybrać **ProcessName** hello filtru wyszukiwania. Który zawęża hello informacje dla Ciebie.

![Przechodzenie do szczegółów](./media/log-analytics-vmware/eventhostdrilldown.png)

#### <a name="find-high-vm-activities"></a>Znajdź dużej aktywności maszyny Wirtualnej
Można tworzyć i usunąć na żadnym hoście ESXi maszyny wirtualnej. Jest przydatne w przypadku tooidentify administratora liczbę maszyn wirtualnych, które tworzy hosta ESXi. Który w Włącz, toounderstand wydajności i planowania pojemności. Rejestrowanie informacji o zdarzenia działania maszyny Wirtualnej jest niezwykle istotne w przypadku, gdy zarządzanie środowiskiem.

![Przechodzenie do szczegółów](./media/log-analytics-vmware/vmactivities1.png)

Kliknij nazwę hosta ESXi, toosee hosta ESXi dodatkowe dane dotyczące tworzenia maszyny Wirtualnej.

![Przechodzenie do szczegółów](./media/log-analytics-vmware/createvm.png)

#### <a name="common-search-queries"></a>Typowe zapytania wyszukiwania
rozwiązanie Hello zawiera inne przydatne zapytań, które ułatwiają zarządzanie hostach ESXi, takich jak miejsca do magazynowania wysoka, opóźnienie magazynu ścieżka błędu.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![— zapytania](./media/log-analytics-vmware/queries.png)


#### <a name="save-queries"></a>Zapisywanie zapytań
Zapisywanie zapytań wyszukiwania jest standardowa funkcja OMS i mogą pomóc żadnych zapytań, które zostały znalezione przydatne. Po utworzeniu kwerendę, która jest użyteczna, zapisz go, klikając hello **ulubione**. Zapisane zapytanie pozwala łatwo użyć go ponownie później z hello [Mój pulpit nawigacyjny](log-analytics-dashboards.md) strony, w którym można tworzyć niestandardowe pulpity.

![DockerDashboardView](./media/log-analytics-vmware/dockerdashboardview.png)

#### <a name="create-alerts-from-queries"></a>Utwórz alerty na podstawie zapytania
Po utworzeniu zapytań może być toouse hello zapytania tooalert w przypadku wystąpienia określonych zdarzeń. Zobacz [alertów w analizy dzienników](log-analytics-alerts.md) informacje na temat toocreate alertów. Przykłady alerty zapytania i inne przykłady zapytania, zobacz hello [VMware monitora przy użyciu analizy dzienników OMS](https://blogs.technet.microsoft.com/msoms/2016/06/15/monitor-vmware-using-oms-log-analytics) wpis w blogu.

## <a name="frequently-asked-questions"></a>Często zadawane pytania
### <a name="what-do-i-need-toodo-on-hello-esxi-host-setting-what-impact-will-it-have-on-my-current-environment"></a>Co należy toodo na hoście ESXi hello ustawienie? Jaki wpływ mają go na mój bieżącego środowiska?
rozwiązanie Hello używa hello macierzysty mechanizm przekazywania Syslog hosta ESXi. Nie potrzebujesz dodatkowego oprogramowania Microsoft hello hosta ESXi toocapture hello dzienników. Powinien on tooyour niski wpływ istniejącego środowiska. Należy jednak tooset syslog przekazywania, czyli ESXI funkcji.

### <a name="do-i-need-toorestart-my-esxi-host"></a>Należy toorestart Moje hosta ESXi?
Nie. Ten proces nie wymaga ponownego uruchomienia komputera. Czasami prawidłowo vSphere nie aktualizuje hello syslog. W takim przypadku Zaloguj się na hoście ESXi toohello i załaduj ponownie hello syslog. Ponownie nie masz toorestart hello hosta, więc ten proces nie jest destrukcyjne tooyour środowiska.

### <a name="can-i-increase-or-decrease-hello-volume-of-log-data-sent-toooms"></a>Można można zwiększyć lub zmniejszyć wolumin hello wysyłane tooOMS danych dziennika?
Tak, można. Można użyć ustawień poziomu dziennika hosta ESXi hello w vSphere. Zbieranie dzienników jest oparta na powitania *informacji* poziom. Tak, jeśli chcesz tooaudit tworzenia maszyny Wirtualnej lub usunięciu konieczne tookeep hello *informacji* poziomu na Hostd. Aby uzyskać więcej informacji, zobacz hello [wiedzy VMware](https://kb.vmware.com/selfservice/microsites/search.do?&cmd=displayKC&externalId=1017658).

### <a name="why-is-hostd-not-providing-data-toooms-my-log-setting-is-set-tooinfo"></a>Dlaczego Hostd nie dostarcza tooOMS danych? Mój dzienniku ustawioną tooinfo.
Wystąpił błąd hosta ESXi sygnatura czasowa syslog hello. Aby uzyskać więcej informacji, zobacz hello [wiedzy VMware](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2111202). Po zastosowaniu obejścia hello Hostd powinny działać normalnie.

### <a name="can-i-have-multiple-esxi-hosts-forwarding-syslog-data-tooa-single-vm-with-omsagent"></a>Może mieć wiele ESXi hostów przekazywania syslog tooa danych maszyny Wirtualnej z jednym z omsagent?
Tak. Może mieć wiele ESXi przekazywania tooa hosty maszyny Wirtualnej z jednym z omsagent.

### <a name="why-dont-i-see-data-flowing-into-oms"></a>Dlaczego nie widzę danych otrzymywanych przez OMS
Może istnieć wiele przyczyn:

* Hello ESXi hosta nie jest poprawnie wypychanie omsagent uruchomionej maszyny Wirtualnej toohello danych. tootest, wykonaj następujące kroki hello:

  1. tooconfirm, zaloguj się na hoście ESXi toohello przy użyciu ssh i uruchom następujące polecenie hello:`nc -z ipaddressofVM 1514`

      Jeśli to się nie powiedzie, ustawienia vSphere w hello Advanced Configuration są prawdopodobnie nie rozwiązać. Zobacz [Konfigurowanie zbierania syslog](#configure-syslog-collection) informacji o jak tooset się hello ESXi hosta przekazywania dziennika systemowego.
  2. Jeśli łączności port syslog zakończy się pomyślnie, ale nadal nie widzisz żadnych danych, należy ponownie załadować syslog hello na hoście ESXi hello przy użyciu ssh hello toorun następujące polecenie:` esxcli system syslog reload`
* Nie ustawiono poprawnie Hello maszyny Wirtualnej z agentem pakietu OMS. tootest, wykonaj następujące kroki hello:

  1. OMS nasłuchuje portu toohello 1514 i wypycha dane do OMS. tooverify jest otwarty, uruchom następujące polecenie hello:`netstat -a | grep 1514`
  2. Powinny pojawić się portu `1514/tcp` otworzyć. Jeśli nie chcesz, sprawdź, czy ten omsagent hello jest poprawnie zainstalowany. Jeśli nie ma informacji o porcie hello, hello syslog port nie jest otwarty na powitania maszyny Wirtualnej.

     1. Sprawdź, że hello OMS Agent jest uruchomiony przy użyciu `ps -ef | grep oms`. Jeśli nie jest uruchomiona, uruchom proces hello, uruchamiając polecenie hello` sudo /opt/microsoft/omsagent/bin/service_control start`
     2. Otwórz hello `/etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf` pliku.

         Sprawdź, czy hello odpowiednich użytkowników i ustawienia grupy jest prawidłowy, podobnie jak:`-rw-r--r-- 1 omsagent omiusers 677 Sep 20 16:46 vmware_esxi.conf`

         Jeśli hello plik nie istnieje lub nie hello użytkownika i ustawienia grupy jest nieprawidłowy, należy podjąć działania naprawcze przez [przygotowania serwera Linux](#prepare-a-linux-server).

## <a name="next-steps"></a>Następne kroki
* Użyj [dziennik wyszukiwania](log-analytics-log-searches.md) w analizy dzienników tooview szczegółowe dane hosta VMware.
* [Tworzenie własnych pulpity nawigacyjne](log-analytics-dashboards.md) przedstawiający danych hosta VMware.
* [Tworzenie alertów](log-analytics-alerts.md) po wystąpieniu określonych zdarzeń hosta VMware.
