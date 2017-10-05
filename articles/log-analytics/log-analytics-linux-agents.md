---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: TRUE
ROBOTS: NOINDEX
ms.openlocfilehash: 8332bdd39effab8c2ac9a75ca9a1e2510c940719
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-linux-computers-to-log-analytics"></a>Łączenie komputerów Linux do analizy dzienników
Za pomocą analizy dzienników, można zbierać i działają na danych generowanych przez komputery z systemem Linux. Dodawanie danych zbieranych z systemem Linux z usługą OMS umożliwia zarządzanie systemów Linux i kontener rozwiązań, takich jak Docker, niezależnie od tego, w którym znajdują się komputery — niemal dowolnego miejsca. Źródła danych mogą znajdować się w lokalnym centrum danych jako serwerów fizycznych komputerów wirtualnych w usług hostowanych w chmurze, takich jak Amazon Web Services (AWS) lub Microsoft Azure lub nawet laptopów na biurku. Ponadto OMS również zbiera dane z komputerów z systemem Windows podobnie, obsługuje on naprawdę hybrydowe środowiska IT.

Można wyświetlić i zarządzać danych ze wszystkich tych źródeł z analizy dzienników w OMS za pomocą portalu zarządzania pojedynczego. Zmniejsza to potrzebę monitorowania przy użyciu wielu różnych systemów, sprawia, że ułatwiają korzystanie, na które można wyeksportować danych, które chcesz niezależnie od rozwiązania analizy biznesowej lub system, który już istnieje.

W tym artykule jest szybki start przewodnik, które zawierają informacje pomocne podczas zbierania danych i zarządzać nimi komputerów systemu Linux przy użyciu agenta pakietu OMS dla systemu Linux. Aby uzyskać więcej szczegółowych informacji technicznych, takich jak konfiguracja serwera proxy, informacje o CollectD metryki i niestandardowych źródeł danych JSON, znajdziesz te informacje w [Agent pakietu OMS dla systemu Linux — omówienie](https://github.com/Microsoft/OMS-Agent-for-Linux) i [Agent pakietu OMS dla systemu Linux Pełna dokumentacja](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) w witrynie GitHub.

Obecnie można zebrać następujące typy danych z komputerów z systemem Linux:

* Metryki wydajności
* Zdarzenia dziennika systemowego
* Alerty z Nagios i Zabbix
* Metryki wydajności kontenera docker, spisu i dzienniki

## <a name="supported-linux-versions"></a>Obsługiwane wersje systemu Linux
Wersje x x86 i x64 oficjalnie są obsługiwane w różnych dystrybucje systemu Linux. Jednak Agent pakietu OMS dla systemu Linux mogą również uruchomić na innych dystrybucje nie na liście.

* Linux Amazon 2012.09 za pośrednictwem 2015.09
* CentOS Linux 5, 6 i 7
* Oracle Linux 5, 6 i 7
* Red Hat Enterprise Linux Server 5, 6 i 7
* Debian GNU/Linux 6, 7 i 8
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10
* SUSE Linux Enterprise Server 11 i 12

## <a name="oms-agent-for-linux"></a>Agent pakietu OMS dla systemu Linux
Agent programu Operations Management Suite dla systemu Linux składa się z wielu pakietów. Plik wersji zawiera następujących pakietów, dostępne za pomocą powłoki pakietu z `--extract`.

| **Pakiet** | **Wersja** | **Opis** |
| --- | --- | --- |
| omsagent |1.1.0 |Agent programu Operations Management Suite dla systemu Linux |
| omsconfig |1.1.1 |Agent konfiguracji dla agenta pakietu OMS |
| OMI |1.0.8.3 |Open Management Infrastructure (OMI)--lekkie serwera modelu wspólnych informacji |
| scx |1.6.2 |OMI CIM dostawców dla metryki wydajności systemu operacyjnego |
| Apache cimprov |1.0.0 |Monitorowanie dostawcę dla OMI wydajności Apache HTTP Server. Zainstalować tylko w przypadku wykrycia Apache HTTP Server. |
| MySQL cimprov |1.0.0 |Monitorowanie dostawcę dla OMI wydajności serwera MySQL. Zainstalować tylko w przypadku wykrycia MySQL/MariaDB serwera. |
| docker cimprov |0.1.0 |Dostawca docker OMI. Zainstalować tylko w przypadku wykrycia Docker. |

### <a name="additional-installation-artifacts"></a>Artefakty dodatkowych instalacji
Po zainstalowaniu agenta pakietu OMS pakietów systemu Linux, są stosowane następujące zmiany w dodatkowych konfiguracji całego systemu. Te artefakty muszą zostać usunięte po odinstalowaniu pakietu omsagent.

* Użytkownik bez uprawnień o nazwie: `omsagent` jest tworzony. Jest to konto, które demona omsagent działa jako
* Plik "Dołącz" sudoers jest tworzony w /etc/sudoers.d/omsagent to autoryzuje omsagent ponowne uruchomienie demonów syslog i omsagent. Jeśli dyrektywy "Dołącz" sudo nie są obsługiwane w zainstalowanej wersji programu sudo, te wpisy będą zapisywane /etc/sudoers.
* Zmodyfikowaniu konfiguracji syslog do przekazywania podzbiór zdarzeń na agencie. Aby uzyskać więcej informacji, zobacz **Konfigurowanie zbierania danych** poniższej sekcji

### <a name="linux-data-collection-details"></a>Szczegóły pobierania danych systemu Linux
W poniższej tabeli przedstawiono metody zbierania danych i inne szczegółowe informacje o jak zbierane są dane.

| Źródło | Bezpośrednie agenta | Agenta programu SCOM | Azure Storage | SCOM wymagane? | Dane agenta programu SCOM wysyłane za pośrednictwem grupy zarządzania | Częstotliwość kolekcji |
| --- | --- | --- | --- | --- | --- | --- |
| Zabbix |![Tak](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |1 minuta |
| Nagios |![Tak](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |po przybyciu |
| syslog |![Tak](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |z usługi Azure storage: 10 minut; od agenta: Przy nadejściu |
| Liczniki wydajności systemu Linux |![Tak](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |jako zaplanowane, co najmniej 10 sekund |
| Śledzenie zmian |![Tak](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |co godzinę |

### <a name="package-requirements"></a>Wymagania pakietu
| **Wymagany pakiet** | **Opis** | **Minimalna wersja** |
| --- | --- | --- |
| Glibc |Biblioteka GNU C |2.5-12 |
| Biblioteki Openssl |Biblioteki OpenSSL |0.9.8e lub 1.0 |
| Narzędzie curl |cURL klienta sieci web |7.15.5 |
| Ctypes języka Python |Funkcja biblioteki |Nie dotyczy |
| PAM |Uwierzytelnianie podłączane moduły |Nie dotyczy |

> [!NOTE]
> Rsyslog lub syslog ng są wymagane do zbierania komunikaty dziennika systemowego. Demon syslog domyślne w wersji 5 (sysklog) w wersji Red Hat Enterprise Linux, CentOS i Oracle Linux nie jest obsługiwana dla zbierania zdarzeń usługi syslog. Aby zbierać dane syslog z tej wersji tych dystrybucji, demona rsyslog powinna być zainstalowana i skonfigurowana zastąpić sysklog.
>
>

## <a name="quick-install"></a>Szybkiej instalacji
Uruchom następujące polecenia, aby pobrać omsagent, weryfikacja sumy kontrolnej, a następnie zainstalować i dołączyć agenta. Polecenia są dla 64-bitowej. Identyfikator i klucz podstawowy znajdują się w portalu OMS w obszarze **ustawienia** na **połączonych źródeł** kartę.

![szczegóły obszaru roboczego](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

Istnieje wiele innych metod, aby zainstalować agenta i ją uaktualnić. Więcej o nich na [kroki, aby zainstalować agenta pakietu OMS Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).

Można również wyświetlić [Azure przewodnik wideo](https://www.youtube.com/watch?v=mF1wtHPEzT0).

## <a name="choose-your-linux-data-collection-method"></a>Wybierz metodę zbierania danych systemu Linux
Jak zależy typy danych, które chcesz zebrać czy chcesz korzystać z portalu OMS lub jeśli chcesz edytować różne pliki konfiguracji bezpośrednio na klientach systemu Linux. Jeśli chcesz korzystać z portalu konfigurację są automatycznie wysyłane do wszystkich klientów systemu Linux. Jeśli potrzebujesz różnych konfiguracji dla różnych klientów systemu Linux, należy edytować pliki klienta indywidualnie — lub użyj innego jak PowerShell DSC, Chef lub Puppet.

Można określić zdarzenia dziennika systemowego i liczniki wydajności, które mają być zbierane za pomocą plików konfiguracji na komputerach z systemem Linux. *Jeśli zdecydujesz się na Konfigurowanie zbierania danych przez edycję plików konfiguracyjnych agenta, należy wyłączyć scentralizowane konfiguracji.*  Instrukcje znajdują się poniżej do skonfigurowania zbierania danych w plikach konfiguracji agenta, a także aby wyłączyć konfigurację centralnej wszystkich agentów OMS dla systemu Linux lub pojedynczych komputerów.

### <a name="disable-oms-management-for-an-individual-linux-computer"></a>Wyłącz zarządzanie OMS dla danego komputera systemu Linux
Scentralizowane zbieranie danych dla danych konfiguracji jest wyłączona dla pojedynczego komputera systemu Linux przy użyciu skryptu OMS_MetaConfigHelper.py. Może to być przydatne, jeśli podzbiorowi komputerów należy specjalne konfiguracji.

Aby wyłączyć scentralizowane konfiguracji:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

Aby ponownie włączyć scentralizowane konfiguracji:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a>Liczniki wydajności systemu Linux
Liczniki wydajności systemu Linux są podobne do liczników wydajności systemu Windows — zarówno działają podobnie. Aby dodać i skonfigurować je, można użyć poniższych procedur. Po dodaniu ich do OMS, dane są zbierane dla nich co 30 sekund.

### <a name="to-add-a-linux-performance-counter-in-oms"></a>Aby dodać licznika wydajności systemu Linux w OMS
1. Aby skonfigurować agentów OMS dla systemu Linux przy użyciu portalu OMS, Dodaj liczniki wydajności systemu Linux na stronie Ustawienia, kliknij przycisk **danych**.  
2. Na **ustawienia** w obszarze **danych** , kliknij przycisk **liczników wydajności systemu Linux** , a następnie wybierz lub wpisz nazwę licznika, które chcesz dodać.  
    ![dane](./media/log-analytics-linux-agents/oms-settings-data01.png)
3. Jeśli nie znasz pełną nazwę licznika, możesz wpisać nazwę częściowe i zostanie wyświetlona lista dostępnych liczników. Po znalezieniu licznik, który chcesz dodać, kliknij nazwę na liście, a następnie kliknij ikonę znaku plus, można dodać licznika.
4. Po dodaniu licznik, zostanie wyświetlona lista liczników wyróżnione z paskiem kolorowe.
5. Domyślnie **Zastosuj poniższą konfigurację do moich maszyn** opcja jest zaznaczona. Jeśli chcesz wyłączyć przesłania danych konfiguracji, wyczyść zaznaczenie.
6. Po zakończeniu modyfikowania liczniki wydajności, w dolnej części strony kliknij **zapisać** aby zakończyć wprowadzanie zmian. Wprowadzone zmiany konfiguracji są następnie wysyłane do wszystkich agentów OMS dla systemu Linux, które są zarejestrowane w usłudze OMS, zazwyczaj w ciągu 5 minut.

### <a name="configure-linux-performance-counters-in-oms"></a>Konfigurowanie liczników wydajności systemu Linux w OMS
Do liczników wydajności systemu Windows można wybrać określonego wystąpienia dla każdego licznika wydajności. Do liczników wydajności systemu Linux, niezależnie od wystąpienia wybranego licznika ma zastosowanie do wszystkich liczników podrzędnych licznika nadrzędnej. W poniższej tabeli przedstawiono typowe wystąpienia dostępne do liczników wydajności zarówno systemu Linux i Windows.

| **Nazwa wystąpienia** | **Znaczenie** |
| --- | --- |
| \_Całkowita liczba |Całkowita liczba wszystkich wystąpień |
| \* |Wszystkie wystąpienia |
| (/ & #124; / var) |Dopasowuje wystąpienia o nazwie: / lub /var |

Podobnie, wybrane interwału próbkowania licznika nadrzędny ma zastosowanie do wszystkich liczników podrzędnych. Innymi słowy interwałów próbkowania licznika podrzędnych i wystąpienia są również powiązane ze sobą.

### <a name="add-and-configure-performance-metrics-with-linux"></a>Dodawanie i Konfigurowanie metryki wydajności z systemem Linux
Metryki wydajności do zbierania są kontrolowane przez konfigurację w/etc/opt/microsoft/omsagent/&lt;identyfikator obszaru roboczego&gt;/conf/omsagent.conf. Zobacz [metryki wydajności dostępne](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) dostępnych klas i metryki dla agenta pakietu OMS dla systemu Linux.

Każdy obiekt lub kategorii, metryki wydajności do zbierania powinien być zdefiniowany w pliku konfiguracyjnym jako pojedynczy `<source>` elementu. Składnia jest zgodny ze wzorcem poniżej.

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

Można konfigurować parametry tego elementu są:

* **Obiekt\_nazwa**: Nazwa obiektu dla kolekcji.
* **Wystąpienie\_regex**: *wyrażenia regularnego* Definiowanie które wystąpienia zbierania. Wartość: `.*` określa wszystkich wystąpień. Aby zbierać metryki procesora tylko \_całkowita liczba wystąpień, można określić `_Total`. Aby zbierać metryki procesu tylko wystąpienia crond lub sshd, można określić: `(crond|sshd)`.
* **Licznik\_nazwa\_regex**: *wyrażenia regularnego* definiujący, które liczniki (dla obiekt) do zbierania. Aby zbierać wszystkie liczniki dla obiekt, podaj: `.*`. Aby zbierać tylko wymiany miejsca liczniki dla obiekt pamięć, można określić:`.+Swap.+`
* **Interwał:**: częstotliwość pobierane liczniki obiektu.

Konfigurację domyślną dla metryki wydajności jest:

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a>Włącz MySQL liczniki wydajności za pomocą poleceń systemu Linux
Jeśli serwer MySQL lub MariaDB serwer zostanie wykryta na komputerze po zainstalowaniu pakietu omsagent, jest automatycznie instalowany dostawcy dla serwera MySQL monitorowania wydajności. Ten dostawca nawiązuje połączenie z lokalnym serwerem MySQL/MariaDB do udostępnienia statystyki. Musisz skonfigurować poświadczenia użytkownika MySQL, tak aby dostawca dostęp do serwera MySQL.

Aby zdefiniować domyślne konto użytkownika serwera MySQL na hoście lokalnym, skorzystaj z następującego przykładu polecenia.

> [!NOTE]
> Musi być do odczytu przez konto omsagent pliku poświadczeń. Zalecane jest uruchomienie polecenia mycimprovauth jako omsgent.
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


Alternatywnie można określić wymaganych poświadczeń MySQL w pliku, tworząc plik: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Aby uzyskać więcej informacji o zarządzaniu MySQL poświadczeń do monitorowania za pomocą pliku mysql uwierzytelniania, zobacz [MySQL zarządzania, monitorowania poświadczenia w pliku authentication](#manage-mysql-monitoring-credentials-in-the-authentication-file).

Zobacz [bazy danych uprawnienia wymagane do liczników wydajności MySQL](#database-permissions-required-for-mysql-performance-counters) szczegółowe informacje na temat obiektu uprawnienia wymagane przez użytkownika MySQL, aby zbierać dane dotyczące wydajności serwera MySQL.

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a>Włącz Apache HTTP Server liczniki wydajności za pomocą poleceń systemu Linux
W przypadku wykrycia Apache HTTP Server na komputerze jest zainstalowany pakiet omsagent, jest automatycznie instalowany dostawcy dla Apache HTTP Server monitorowania wydajności. Ten dostawca zależy od Apache "module", który musi zostać załadowane do Apache HTTP Server w celu uzyskania dostępu do danych dotyczących wydajności.

Można załadować modułu przy użyciu następującego polecenia:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

Aby zwolnić modułu monitorowania Apache, uruchom następujące polecenie:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="to-view-performance-data-with-log-analytics"></a>Aby wyświetlić dane wydajności z analizy dzienników
1. W portalu usługi Operations Management Suite kliknij Kafelek wyszukiwania dziennika.
2. Na pasku wyszukiwania wpisz `* (Type=Perf)` Aby wyświetlić wszystkie liczniki wydajności.

Ponieważ OMS również zbieranie danych licznika wydajności systemu Windows, użytkownik powinien zakresu rozwijanej Wyszukaj, aby dane specyficzne dla systemu Linux. Tak poniższy przykład czy przedstawiono dane wydajności specyficzne dla systemu Linux przykładowego serwera o nazwie Chorizo21.

```
Type=Perf Computer=chorizo*
```

![przykład serwera wyświetlane w wynikach wyszukiwania](./media/log-analytics-linux-agents/oms-perfsearch01.png)

W wynikach, kliknij **metryki** Aby wyświetlić liczniki, które zebrano dane. Dane w czasie rzeczywistym jest wyświetlany na wykresach dla każdego licznika.

![metrics](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a>Dziennik systemu
SYSLOG jest protokół rejestrowania zdarzeń podobnych do dzienników zdarzeń systemu Windows — zarówno działają podobnie, podczas wyświetlania w OMS.

### <a name="to-add-a-new-linux-syslog-facility-in-oms"></a>Aby dodać nowy funkcję dziennika systemowego systemu Linux w OMS
1. Na **ustawienia** w obszarze **danych** , kliknij przycisk **Syslog** , a następnie po lewej stronie ikonę znaku plus, wpisz nazwę obiektu syslog, które chcesz dodać.
    ![Systemu Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)
2. Jeśli nie znasz pełną nazwę funkcji, możesz wpisać nazwę częściowe i zostanie wyświetlona lista dostępnych syslog urządzeń. Po znalezieniu funkcję dziennika systemowego, który chcesz dodać, kliknij nazwę na liście, a następnie kliknij ikonę znaku plus, aby dodać funkcję dziennika systemowego.
3. Po dodaniu funkcji wydaje się na liście wyróżnione z paskiem kolorowe. Następnie wybierz ważności (kategorie informacji zakładzie syslog), które mają być zbierane.
4. W dolnej części strony kliknij **zapisać** aby zakończyć wprowadzanie zmian. Wprowadzone zmiany konfiguracji są następnie wysyłane do wszystkich agentów OMS dla systemu Linux, które są zarejestrowane w usłudze OMS, zazwyczaj w ciągu 5 minut.

### <a name="configure-linux-syslog-facilities-in-linux"></a>Konfigurowanie urządzeń dziennika systemu Linux w systemie Linux
Zdarzenia dziennika systemowego są wysyłane z demona syslog, na przykład rsyslog lub syslog ng, do lokalnego portu, na którym nasłuchuje agent. Domyślnie port 25224. Agent jest zainstalowany, jest stosowany domyślnej konfiguracji programu syslog. Znaleziono w lokalizacji:

Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf

SYSLOG ng: /etc/syslog-ng/syslog-ng.conf

Domyślna konfiguracja syslog agent pakietu OMS przekazuje zdarzenia dziennika systemowego z wszystkich urządzeń z ważnością, ostrzeżenie lub nowszej.

> [!NOTE]
> Po zmodyfikowaniu konfiguracji programu syslog, należy ponownie uruchomić demona syslog, aby zmiany zaczęły obowiązywać.
>
>

Syslog konfigurację domyślną dla agenta pakietu OMS dla systemu Linux dla OMS jest:

#### <a name="rsyslog"></a>rsyslog
```
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
```

#### <a name="syslog-ng"></a>SYSLOG ng
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="to-view-all-syslog-events-with-log-analytics"></a>Aby wyświetlić wszystkie zdarzenia dziennika systemowego z analizy dzienników
1. W portalu usługi Operations Management Suite kliknij **wyszukiwania dziennika** kafelka.
2. W **zarządzanie dziennikiem** grupowania, wybierz wyszukiwania wstępnie zdefiniowanych syslog, a następnie wybierz jedno go uruchomić.

Ten przykład przedstawia wszystkie zdarzenia dziennika systemowego.

![Zdarzenia dziennika systemowego pokazano wyszukiwania dziennika](./media/log-analytics-linux-agents/oms-linux-syslog.png)

Teraz możesz przejść do szczegółów wyników wyszukiwania.

## <a name="linux-alerts"></a>Alerty systemu Linux
Jeśli używasz Nagios lub Zabbix do zarządzania maszyn z systemem Linux OMS może otrzymywać alerty generowane na podstawie tych narzędzi. Jednak nie jest obecnie żadna metoda, aby skonfigurować przychodzących danych alertów za pomocą portalu OMS. Zamiast tego należy edytować plik konfiguracji rozpoczął wysyłania alertów z usługą OMS.

### <a name="collect-alerts-from-nagios"></a>Zbieraj alerty z Nagios
Aby zbierać alerty z serwera Nagios, musisz wprowadzić następujące zmiany konfiguracji.

1. Przyznaj użytkownikowi **omsagent** dostęp do odczytu do pliku dziennika Nagios (tj. /var/log/nagios/nagios.log). Zakładając, że plik nagios.log jest właścicielem grupy **nagios** , można dodać użytkownika **omsagent** do **nagios** grupy.

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. Zmodyfikuj plik omsagent.confconfiguration (/ etc/opt/microsoft/omsagent/&lt;identyfikator obszaru roboczego&gt;/conf/omsagent.conf). Upewnij się, że następujące wpisy są obecne i nie komentarze wychodzących:

    ```
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
    ```
3. Uruchom ponownie demona omsagent:

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a>Zbieraj alerty z Zabbix
Aby zbierać alerty z serwera Zabbix, będziesz wykonywać podobne kroki w celu dla Nagios powyżej, z wyjątkiem należy określić użytkownika i hasło w *zwykły tekst*. To nie jest idealnym rozwiązaniem, ale prawdopodobnie zmienią się wkrótce. Aby rozwiązać ten problem, zaleca się utworzyć użytkownika, a następnie udzielić jej uprawnienia do monitorowania tylko.

Przykład sekcji pliku konfiguracji omsagent.conf (/ etc/opt/microsoft/omsagent/&lt;identyfikator obszaru roboczego&gt;/conf/omsagent.conf) dla Zabbix powinien przypominać następujący:

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a>Wyświetlanie alertów w wyszukiwaniu analizy dzienników
Po skonfigurowaniu komputerach systemu Linux w celu wysyłania alertów z usługą OMS, można użyć kilka zapytań wyszukiwania prostego dziennika do wyświetlania alertów. W poniższym przykładzie zapytanie wyszukiwania zwraca wszystkie zarejestrowane alertów, które zostały wygenerowane. Na przykład jeśli jakieś problem występuje w infrastrukturze IT, następnie wyniki następujące przykładowe zapytanie może wskazywać którego pochodzą może ten problem. I mogą łatwo przechodzenia alertom przez system źródła, aby zawęzić badaniu. Korzyścią jest to, że zawsze nie musi przechodzić do różnych systemów zarządzania od początku, pod warunkiem, że alerty są wysyłane do OMS, można uruchomić istnieje.

```
Type=Alert
```

#### <a name="to-view-all-nagios-alerts-with-log-analytics"></a>Aby wyświetlić wszystkie alerty Nagios z analizy dzienników
1. W portalu usługi Operations Management Suite kliknij **wyszukiwania dziennika** kafelka.
2. Na pasku zapytania wpisz następujące zapytanie wyszukiwania

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Nagios alertów przedstawianych w dzienniku wyszukiwania](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

Po wyniki wyszukiwania, możesz przejść do szczegółów dodatkowych szczegółów takich jak *stan alertu*.

### <a name="to-view-all-zabbix-alerts-with-log-analytics"></a>Aby wyświetlić wszystkie alerty Zabbix z analizy dzienników
1. W portalu usługi Operations Management Suite kliknij **wyszukiwania dziennika** kafelka.
2. Na pasku zapytania wpisz następujące zapytanie wyszukiwania

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Zabbix alertów przedstawianych w dzienniku wyszukiwania](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

Po wyniki wyszukiwania, możesz przejść do szczegółów dodatkowych szczegółów takich jak *AlertName*.

## <a name="compatibility-with-system-center-operations-manager"></a>Zgodność z programem System Center Operations Manager
Agent pakietu OMS dla systemu Linux udostępnia pliki binarne agenta agenta programu System Center Operations Manager. Instalowanie agenta pakietu OMS dla systemu Linux w systemie, w obecnie zarządzany przez program Operations Manager uaktualnia OMI i SCX pakietów na komputerze do nowszej wersji. Agent pakietu OMS dla systemów Linux i System Center 2012 R2 są zgodne. Jednak **System Center 2012 SP1 i wcześniejsze wersje nie są obecnie zgodne lub nie jest obsługiwany z agentem pakietu OMS dla systemu Linux.**

> [!NOTE]
> Jeśli Agent pakietu OMS dla systemu Linux jest zainstalowana na komputerze, który nie jest obecnie zarządzany przez program Operations Manager, a później chcesz zarządzać komputerem z programem Operations Manager, należy zmodyfikować konfigurację OMI przed wykryje komputer. **Ten krok jest zbędny, jeśli agent programu Operations Manager została zainstalowana przed Agent pakietu OMS dla systemu Linux.**
>
>

### <a name="to-enable-the-oms-agent-for-linux-to-communicate-with-operations-manager"></a>Aby włączyć agenta pakietu OMS dla systemu Linux do komunikowania się z programem Operations Manager
1. Edytuj plik /etc/opt/omi/conf/omiserver.conf
2. Upewnij się, że zaczyna się od wiersza **httpsport =** definiuje portu 1270. Takie jak`httpsport=1270`
3. Uruchom ponownie serwer OMI:

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a>Uprawnienia bazy danych wymagane dla liczników wydajności MySQL
Aby udzielić uprawnień użytkownikowi monitorowania, MySQL, udzielającym użytkownik musi mieć uprawnienie "GRANT option", a także udzielenia uprawnienia.

Aby użytkownikowi MySQL zwrócone dane dotyczące wydajności, które użytkownik wymaga dostępu do następujące zapytania:

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

Oprócz tych zapytań MySQL użytkownika wymaga wybierz dostęp do poniższych tabelach domyślne:

* INFORMATION_SCHEMA
* MySQL

Te uprawnienia można otrzymać, uruchamiając następujące polecenia grant.

```
GRANT SELECT ON information_schema.* TO ‘monuser’@’localhost’;
GRANT SELECT ON mysql.* TO ‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-the-authentication-file"></a>Zarządzanie MySQL monitorowania poświadczenia w pliku uwierzytelniania
Poniższe sekcje zawierają informacje pomocne w zarządzaniu poświadczenia MySQL.

### <a name="configure-the-mysql-omi-provider"></a>Konfigurowanie dostawcy MySQL OMI
Dostawca MySQL OMI wymaga wstępnie skonfigurowane użytkownika MySQL i zainstalowania bibliotek klienta MySQL zapytania o informacje o kondycji wydajności z wystąpienia MySQL.

### <a name="mysql-omi-authentication-file"></a>Plik authentication MySQL OMI
Dostawcy MySQL OMI używany jest plik authentication ustalić bind adres i port MySQL nasłuchuje wystąpienie i jakie poświadczenia, które będzie używane do zbierania metryk. Podczas instalacji MySQL OMI dostawca skanowania MySQL my.cnf pliki konfiguracji (lokalizacje domyślne) dla wiązania adres i port i plik authentication częściowo zestawu MySQL OMI.

Aby ukończyć, monitorowanie wystąpienia serwera MySQL, należy dodać wstępnie wygenerowany plik authentication MySQL OMI w poprawnym katalogu.

### <a name="authentication-file-format"></a>Format pliku uwierzytelniania
Plik authentication MySQL OMI jest plik tekstowy, który zawiera informacje o:

* Port
* Adres BIND
* Nazwa_użytkownika MySQL
* Kodowanie Base64 hasła

Plik authentication MySQL OMI tylko przyznaje uprawnienia do odczytu i zapisu do użytkownika w systemie Linux, która go wygenerowała.

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

Domyślny plik authentication MySQL OMI zawiera domyślne wystąpienie i numer portu, w zależności od tego, jakie informacje są dostępne i przeanalizowany z pliku konfiguracji znaleziono MySQL.

Wystąpienie domyślne umożliwiają zarządzanie wielu wystąpień MySQL na jednym hoście Linux łatwiejsze i jest wskazywane przez wystąpienie o portu 0. Wszystkie wystąpienia dodano będzie dziedziczyć właściwości z wystąpienia domyślnego. Na przykład jeśli wystąpienie MySQL nasłuchiwanie na porcie "3308" zostanie dodany, adres powiązania domyślnego wystąpienia, username i password kodowany w standardzie Base64 będzie służyć monitorowanie wystąpienia nasłuchiwanie 3308 i spróbuj. Jeśli wystąpienie na 3308 jest powiązany z innym adresem i korzysta z tej samej pary nazwa użytkownika i hasło MySQL wymagane jest tylko respecification powiązanego adresu i dziedziczone przez inne właściwości.

Przykłady plik authentication wyglądać w następujący sposób.

Domyślne wystąpienie i wystąpienia z portem 3308:

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

Domyślne wystąpienie i wystąpienia z portu 3308 + różnych Base 64 zakodowane hasło:

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| **Właściwość** | **Opis** |
| --- | --- |
| Port |Port reprezentuje bieżącego portu wystąpienia MySQL nasłuchuje na.  Port 0 oznacza, że następujące właściwości są używane dla domyślnego wystąpienia. |
| Adres BIND |Adres powiązania jest bieżącego powiązania MySQL — adresu |
| nazwa użytkownika |Ta nazwa użytkownika MySQL mają być używane do monitorowania MySQL wystąpienie serwera. |
| Hasło kodowane w formacie Base64 |Jest to hasło użytkownika monitorowania MySQL zakodowane w formacie Base64. |
| Aktualizacje automatyczne |Po uaktualnieniu dostawcy OMI MySQL dostawcy Skanuj ponownie zmiany w pliku my.cnf i zastąpić plik MySQL OMI Authentication. Ta flaga ustawioną wartość PRAWDA lub FAŁSZ w zależności od wymaganych aktualizacji do pliku uwierzytelniania MySQL OMI. |

#### <a name="authentication-file-location"></a>Lokalizacja pliku uwierzytelniania
Plik Authentication OMI MySQL powinien znajduje się w następującej lokalizacji i o nazwie "mysql uwierzytelniania":

/var/OPT/Microsoft/MySQL-cimprov/auth/omsagent/MySQL-auth

Plik (i katalog auth/omsagent) powinien należeć do użytkownika omsagent.

## <a name="agent-logs"></a>Dzienniki agentów
W dziennikach Agent pakietu OMS dla systemu Linux jest na:

/ var/opt/microsoft/omsagent/&lt;identyfikator obszaru roboczego&gt;/log/

W dziennikach Agent pakietu OMS dla systemu Linux dla programu omsconfig (konfiguracja agenta) znajduje się na:

/ var/opt/microsoft/omsconfig/log /

Dzienniki dla składników OMI i SCX (udostępniających dane metryk wydajności) znajduje się na:

/ var/opt/omi/log/i /var/opt/microsoft/scx/log

## <a name="troubleshooting-the-oms-agent-for-linux"></a>Rozwiązywanie problemów z agentem pakietu OMS dla systemu Linux
Skorzystaj z poniższych informacji do diagnozowania i rozwiązywania typowych problemów.

Jeśli żaden z informacje dotyczące rozwiązywania problemów w tej sekcji pomaga, umożliwia także następujące zasoby w celu rozwiązania problemu.

* Klienci z Premier pomocy technicznej można rejestrować sprawy pomocy technicznej za pośrednictwem [Premier](https://premier.microsoft.com/)
* Klienci z umowami pomocy technicznej platformy Azure może zalogować się dziale obsługi [portalu Azure](https://manage.windowsazure.com/?getsupport=true)
* Plik [problem GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)
* Forum opinii pomysłów i utworzyć raport o usterce [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)

### <a name="important-log-locations"></a>Lokalizacje ważne dziennika
| Plik | Ścieżka |
| --- | --- |
| Agent pakietu OMS dla pliku dziennika systemu Linux |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| Plik dziennika konfiguracji agenta pakietu OMS |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a>Pliki konfiguracji ważne
| Catergory | Lokalizacja pliku |
| --- | --- |
| Dziennik systemu |`/etc/syslog-ng/syslog-ng.conf`lub `/etc/rsyslog.conf` lub`/etc/rsyslog.d/95-omsagent.conf` |
| Wydajność, Nagios, Zabbix, OMS wyjściowego i agenta ogólne |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| Dodatkowe konfiguracje |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> Edycji plików konfiguracyjnych dla liczników wydajności i syslog zostaną zastąpione, jeśli jest włączona konfiguracja portalu OMS. Możesz wyłączyć konfiguracją w portalu OMS (dla wszystkich węzłów) lub pojedynczych węzłów, wykonując następujące czynności:
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a>Włączenie rejestrowania debugowania
Aby włączenie rejestrowania debugowania, można użyć dodatek typu plug-in OMS danych wyjściowych i pełne dane wyjściowe.

#### <a name="oms-output-plugin"></a>Dodatek dane wyjściowe OMS
FluentD umożliwia dodatek plug-in, aby określić poziomy rejestrowania dziennika różnych poziomów dla danych wejściowych i wyjściowych. Aby określić poziom dziennika różnych dla danych wyjściowych OMS, zmień konfigurację agenta ogólne w `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` pliku.

W dolnej części pliku konfiguracji, należy zmienić `log_level` właściwość z `info` do `debug`.

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

Rejestrowania debugowania umożliwia Zobacz wsadowej operacji przekazywania z usługą OMS oddzielone typ, liczba elementów danych, a czas potrzebny do wysłania.

*Przykładowy dziennik debugowania włączone:*

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a>Pełne dane wyjściowe
Zamiast używać wtyczki dane wyjściowe OMS, można również wyprowadzać elementów danych bezpośrednio do `stdout`, która jest widoczna w pliku dziennika systemu Linux Agent pakietu OMS.

W pliku konfiguracyjnym ogólne agent pakietu OMS na `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, komentarz OMS output wtyczki, dodając `#` przed każdym wierszu.

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

Poniżej wtyczki dane wyjściowe, Usuń komentarz poniższej sekcji przez usunięcie `#` symbol na początku każdego wiersza.

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-the-log"></a>Przekazany dalej komunikaty dziennika systemowego nie pojawiają się w Dzienniku
#### <a name="probable-causes"></a>Prawdopodobne przyczyny
* Konfiguracja stosowane do serwerów systemu Linux nie zezwala na zbiór urządzeń wysłanych i/lub poziomy dziennika
* SYSLOG nie są poprawnie przekazywane na serwer z systemem Linux
* Liczba komunikatów przesyłanych na sekundę jest zbyt duży dla agenta pakietu OMS dla systemu Linux do obsługi konfiguracji podstawowej

#### <a name="resolutions"></a>Rozwiązania
* Sprawdź, czy konfiguracja w portalu OMS Syslog ma wszystkie urządzenia i poziomy dziennika poprawne
  * **Portalu OMS > Ustawienia > danych > Syslog**
* Sprawdź tego macierzystego syslog wiadomości demonów (`rsyslog`, `syslog-ng`) mogą odbierać wiadomości przesyłane dalej
* Sprawdzanie ustawień zapory na serwerze Syslog, aby upewnić się, że komunikaty nie są blokowane
* Symulowanie komunikatu dziennika systemu, aby przy użyciu pakietu OMS `logger` polecenia — na przykład:
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-to-oms-when-using-a-proxy"></a>Problemy z połączeniem z usługą OMS przy użyciu serwera proxy
#### <a name="probable-causes"></a>Prawdopodobne przyczyny
* Określony serwer proxy podczas instalowania i konfigurowania agenta jest niepoprawny
* Usługę punktów końcowych, które nie są whitelistested w centrum danych.

#### <a name="resolutions"></a>Rozwiązania
* Zainstaluj ponownie agenta pakietu OMS dla systemu Linux przy użyciu następującego polecenia z opcją `-v` włączone. Dzięki temu pełne dane wyjściowe agenta łączących się za pośrednictwem serwera proxy z usługą OMS.
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * Zapoznaj się z dokumentacją serwera proxy OMS na [Konfigurowanie agenta do użycia przy użyciu serwera proxy HTTP](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)
* Sprawdź, czy następujące punkty końcowe usługę białej

| Zasób agenta | Porty |
| --- | --- |
| & #42;. ods.opinsights.Azure.com |Port 443 |
| & #42;. OMS.opinsights.Azure.com |Port 443 |
| ods.systemcenteradvisor.com |Port 443 |
| & #42;.blob.core.windows.net/ |Port 443 |

### <a name="a-403-error-is-displayed-when-onboarding"></a>Zostanie wyświetlony błąd 403 podczas dołączania
#### <a name="probable-causes"></a>Prawdopodobne przyczyny
* Data i godzina są niepoprawne na serwerze z systemem Linux
* Identyfikator i klucz obszaru roboczego, używane są nieprawidłowe

#### <a name="resolution"></a>Rozwiązanie
* Sprawdź czas na serwerze z systemem Linux `date` polecenia. Jeśli danych jest większa lub mniejsza niż 15 minut od bieżącego czasu, dołączania kończy się niepowodzeniem. Aby rozwiązać ten problem, zaktualizuj datę i/lub strefy czasowej serwera z systemem Linux.
* Najnowszą wersję agenta pakietu OMS Linux powiadamia użytkownika, jeśli różnica czasu powoduje błąd dołączania
* Ponowna dołączyć przy użyciu poprawny identyfikator i klucz obszaru roboczego. Zobacz [dołączania przy użyciu wiersza polecenia](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) Aby uzyskać więcej informacji.

### <a name="a-500-error-or-404-error-appears-in-the-log-file-after-onboarding"></a>500 Błąd lub błąd 404 pojawia się w pliku dziennika po dołączania
Jest to znany problem występujący podczas pierwszego przekazywania danych Linux pod obszarem roboczym pakietu OMS. Nie dotyczy to danych wysyłanych lub innych problemów. Możesz zignorować błędy podczas początkowego procesu dołączania.

### <a name="nagios-data-does-not-appear-in-the-oms-portal"></a>Nagios dane wyświetlane w portalu OMS
#### <a name="probable-causes"></a>Prawdopodobne przyczyny
* Użytkownik omsagent nie ma uprawnienia do odczytu z pliku dziennika Nagios
* Sekcje źródłowy oraz filtr Nagios nadal są ujęte w pliku omsagent.conf

#### <a name="resolutions"></a>Rozwiązania
* Dodaj użytkownika omsagent, aby można było odczytać z pliku Nagios. Zobacz [alerty Nagios](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) Aby uzyskać więcej informacji.
* W agencie OMS pliku ogólnych konfiguracji systemu Linux na `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, upewnij się, że **zarówno** sekcji Nagios źródła i filtr ma komentarzy usunięty, podobny do poniższego przykładu.

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-the-oms-portal"></a>Dane systemu Linux nie jest wyświetlane w portalu OMS
#### <a name="probable-causes"></a>Prawdopodobne przyczyny
* Dołączenie do usługi OMS nie powiodło się
* Połączenie z usługą OMS jest zablokowane
* Agent pakietu OMS danych Linux jest kopii zapasowej

#### <a name="resolutions"></a>Rozwiązania
* Sprawdź, że dołączania z usługą OMS zakończyła się pomyślnie, sprawdzenia, czy `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` istnieje.
* Ponowna dołączyć omsadmin.sh wiersza polecenia. Zobacz [dołączania przy użyciu wiersza polecenia](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) Aby uzyskać więcej informacji.
* Jeśli używasz serwera proxy, Użyj serwera proxy powyższe kroki rozwiązywania problemów
* W niektórych przypadkach gdy Agent pakietu OMS dla systemu Linux nie mogą komunikować się z usługą OMS danych na agencie jest kopii zapasowej do pełnego rozmiaru 50 MB. Uruchom ponownie agenta pakietu OMS dla systemu Linux, uruchamiając `/opt/microsoft/omsagent/bin/service_control restart` polecenia.
  >[AZURE.NOTE] Tego problemu w 1.1.0-28 wersję agenta i nowszych.

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-the-oms-portal"></a>Nie zastosowano konfigurację liczników wydajności systemu SYSLOG Linux w portalu OMS
#### <a name="probable-causes"></a>Prawdopodobne przyczyny
* Agent konfiguracji agenta pakietu OMS dla systemu Linux nie odebrał najnowszą konfiguracją w portalu OMS.
* Poprawione ustawień w portalu nie zostały zastosowane.

#### <a name="resolutions"></a>Rozwiązania
`omsconfig`jest agentem konfiguracji w Agent pakietu OMS dla systemu Linux, które pobierają zmiany konfiguracji portalu OMS co 5 minut. Ta konfiguracja jest następnie stosowany do Agent pakietu OMS dla plików konfiguracyjnych Linux pod adresem `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.

* W niektórych przypadkach Agent pakietu OMS dla systemu Linux konfiguracji agenta nie można skomunikować się z usługą Konfiguracja portalu, co powoduje najnowszej konfiguracji nie są stosowane.
* Sprawdź, czy `omsconfig` agent został zainstalowany z następującymi:

  * `dpkg --list omsconfig` lub `rpm -qi omsconfig`
  * Jeśli nie jest zainstalowany, zainstaluj ponownie najnowszą wersję agenta pakietu OMS dla systemu Linux
* Sprawdź, czy `omsconfig` agenta może komunikować się z usługą OMS

  * Uruchom `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` polecenia
    * Polecenie powyżej zwraca konfigurację agenta pobiera z portalu, w tym ustawienia Syslog, liczniki wydajności systemu Linux i dzienników niestandardowych
    * W przypadku niepowodzenia powyższego polecenia Uruchom `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` polecenia. To polecenie wymusza agenta omsconfig do komunikowania się z usługą OMS w celu pobrania najnowszej konfiguracji.

### <a name="custom-linux-log-data-does-not-appear-in-the-oms-portal"></a>Niestandardowe dane dziennika systemu Linux nie są wyświetlane w portalu OMS
#### <a name="probable-causes"></a>Prawdopodobne przyczyny
* Dołączenie do usługi OMS nie powiodło się
* **Dotyczy następującej konfiguracji serwerów z systemem Linux** ustawienia nie zostały wybrane.
* omsconfig nie została pobrana najnowsze dziennik niestandardowy z portalu
* `omsagent` Użycie nie jest w stanie dziennik niestandardowy z powodu problemu z uprawnieniami dostępu do lub `omsagent` nie został znaleziony. W takim przypadku zostanie wyświetlony następujący komunikat:
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* Jest to znany problem dotyczący sytuacji wyścigu, który został rozwiązany w Agent pakietu OMS dla 1.1.0-217 wersji systemu Linux

#### <a name="resolutions"></a>Rozwiązania
* Sprawdź, czy udało Ci się pomyślnie został załadowany, określając czy `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` plik istnieje.
  * Jeśli potrzebne, dodać ponownie przy użyciu wiersza polecenia omsadmin.sh. Zobacz [dołączania przy użyciu wiersza polecenia](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) Aby uzyskać więcej informacji.
* W portalu OMS w obszarze **ustawienia** na **danych** karcie, upewnij się, że **dotyczy następującej konfiguracji serwerów z systemem Linux** wybrane ustawienie  
  ![Zastosuj konfigurację](./media/log-analytics-linux-agents/customloglinuxenabled.png)
* Sprawdź, czy `omsconfig` agenta może komunikować się z usługą OMS

  * Uruchom `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` polecenia
  * Polecenie powyżej zwraca konfigurację agenta pobiera z portalu, w tym ustawienia Syslog, liczniki wydajności systemu Linux i dzienników niestandardowych
  * W przypadku niepowodzenia powyższego polecenia Uruchom `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` polecenia. To polecenie wymusza agenta omsconfig do komunikowania się z usługą OMS i pobrania najnowszej konfiguracji.

Zamiast Agent pakietu OMS dla użytkownika w systemie Linux uruchomiony jako użytkownik uprzywilejowanych `root`, Agent pakietu OMS dla systemu Linux jest uruchamiany jako `omsagent` użytkownika. W większości przypadków jawne uprawnienia muszą mieć uprawnienie do użytkownika w celu odczytu niektórych plików.

Aby przyznać uprawnienia do `omsagent` użytkownika, uruchom następujące polecenia:

1. Dodaj `omsagent` użytkownika do określonej grupy z`sudo usermod -a -G <GROUPNAME> <USERNAME>`
2. Uniwersalny dostęp do wymaganego pliku z`sudo chmod -R ugo+rw <FILE DIRECTORY>`

Istnieje znany problem dotyczący sytuacji wyścigu, który został rozwiązany w Agent pakietu OMS dla 1.1.0-217 wersji systemu Linux. Po zaktualizowaniu do najnowsza wersja agenta, uruchom następujące polecenie, aby pobrać najnowszą wersję dodatku danych wyjściowych:

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a>Znane ograniczenia
Przejrzyj poniższe sekcje, aby dowiedzieć się więcej o ograniczeniach bieżącego agenta pakietu OMS dla systemu Linux.

### <a name="azure-diagnostics"></a>Diagnostyka Azure
Dla maszyn wirtualnych systemu Linux działających na platformie Azure może być wymagane dodatkowe kroki umożliwiają zbieranie danych diagnostyki Azure i usługi Operations Management Suite. **W wersji 2.2** rozszerzenia diagnostyki dla systemu Linux jest wymagany dla zgodności z agentem pakietu OMS dla systemu Linux.

Aby uzyskać więcej informacji o instalowaniu i konfigurowaniu rozszerzenia diagnostycznych dla systemu Linux, zobacz [za pomocą polecenia wiersza polecenia platformy Azure można włączyć rozszerzenia diagnostycznych Linux](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).

**Uaktualnianie rozszerzenia diagnostyki Linux z 2.0 do 2,2 ASM interfejsu wiersza polecenia platformy Azure:**

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

**ARM**

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

Plik o nazwie PrivateConfig.json odwoływać się do tych przykładach poleceń. Format tego pliku powinno przypominać następujące przykładowe.

```
    {
    "storageAccountName":"the storage account to receive data",
    "storageAccountKey":"the key of the account"
    }
```

### <a name="sysklog-is-not-supported"></a>Sysklog nie jest obsługiwane.
Rsyslog lub syslog ng są wymagane do zbierania komunikaty dziennika systemowego. Demon syslog domyślne w wersji 5 (sysklog) w wersji Red Hat Enterprise Linux, CentOS i Oracle Linux nie jest obsługiwana dla zbierania zdarzeń usługi syslog. Aby zbierać dane syslog z tej wersji tych dystrybucji, demona rsyslog powinna być zainstalowana i skonfigurowana zastąpić sysklog. Aby uzyskać więcej informacji o zamianę sysklog rsyslog, zobacz [zainstalować nowo zbudowany rsyslog obr. / min](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).

## <a name="next-steps"></a>Następne kroki
* [Dodaj rozwiązania Log Analytics z galerii rozwiązań](log-analytics-add-solutions.md), aby dodać funkcje i zebrać dane.
* Zapoznaj się z [wyszukiwaniem w dziennikach](log-analytics-log-searches.md), aby wyświetlić szczegółowe informacje zebrane przez rozwiązania.
* Użyj [pulpitów nawigacyjnych](log-analytics-dashboards.md), aby zapisywać i wyświetlać własne, niestandardowe wyszukiwania.
