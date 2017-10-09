---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a>Połącz z tooLog komputerów Linux Analytics
Za pomocą analizy dzienników, można zbierać i działają na danych generowanych przez komputery z systemem Linux. Dodawanie danych zbieranych z Linux tooOMS pozwala toomanage systemów Linux i kontener rozwiązań, takich jak Docker, niezależnie od tego, w którym znajdują się komputery — niemal dowolnego miejsca. Źródeł danych może znajdować się w lokalnym centrum danych jako serwerów fizycznych komputerów wirtualnych w usług hostowanych w chmurze, takich jak Amazon Web Services (AWS) lub Microsoft Azure lub nawet hello laptopów na biurku. Ponadto OMS również zbiera dane z komputerów z systemem Windows podobnie, obsługuje on naprawdę hybrydowe środowiska IT.

Można wyświetlić i zarządzać danych ze wszystkich tych źródeł z analizy dzienników w OMS za pomocą portalu zarządzania pojedynczego. Zmniejsza to potrzebę hello toomonitor przy użyciu wielu różnych systemów, umożliwia łatwe tooconsume i można wyeksportować wszystkie dane, które chcesz rozwiązania analizy biznesowej toowhatever lub systemu, która już istnieje.

W tym artykule jest Przewodnik Szybki start, które zawierają informacje pomocne podczas zbierania danych i zarządzanie nimi dla komputerów systemu Linux przy użyciu hello Agent pakietu OMS dla systemu Linux. Aby uzyskać więcej szczegółowych informacji technicznych, takich jak konfiguracja serwera proxy, informacje o CollectD metryki i niestandardowych źródeł danych JSON, znajdziesz te informacje w [Agent pakietu OMS dla systemu Linux — omówienie](https://github.com/Microsoft/OMS-Agent-for-Linux) i [Agent pakietu OMS dla systemu Linux Pełna dokumentacja](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) w witrynie GitHub.

Obecnie można zebrać hello następujące typy danych z komputerów z systemem Linux:

* Metryki wydajności
* Zdarzenia dziennika systemowego
* Alerty z Nagios i Zabbix
* Metryki wydajności kontenera docker, spisu i dzienniki

## <a name="supported-linux-versions"></a>Obsługiwane wersje systemu Linux
Wersje x x86 i x64 oficjalnie są obsługiwane w różnych dystrybucje systemu Linux. Jednak hello Agent pakietu OMS dla systemu Linux mogą również uruchomić na innych dystrybucje nie na liście.

* Linux Amazon 2012.09 za pośrednictwem 2015.09
* CentOS Linux 5, 6 i 7
* Oracle Linux 5, 6 i 7
* Red Hat Enterprise Linux Server 5, 6 i 7
* Debian GNU/Linux 6, 7 i 8
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10
* SUSE Linux Enterprise Server 11 i 12

## <a name="oms-agent-for-linux"></a>Agent pakietu OMS dla systemu Linux
Agent programu Operations Management Suite dla systemu Linux Hello składa się z wielu pakietów. Witaj wersji pliku zawiera następujące dostępnych przez uruchomione hello powłoki pakietu z pakietów hello `--extract`.

| **Pakiet** | **Wersja** | **Opis** |
| --- | --- | --- |
| omsagent |1.1.0 |Witaj Operations Management Suite agenta dla systemu Linux |
| omsconfig |1.1.1 |Konfiguracja agenta dla hello Agent pakietu OMS |
| OMI |1.0.8.3 |Open Management Infrastructure (OMI)--lekkie serwera modelu wspólnych informacji |
| scx |1.6.2 |OMI CIM dostawców dla metryki wydajności systemu operacyjnego |
| Apache cimprov |1.0.0 |Monitorowanie dostawcę dla OMI wydajności Apache HTTP Server. Zainstalować tylko w przypadku wykrycia Apache HTTP Server. |
| MySQL cimprov |1.0.0 |Monitorowanie dostawcę dla OMI wydajności serwera MySQL. Zainstalować tylko w przypadku wykrycia MySQL/MariaDB serwera. |
| docker cimprov |0.1.0 |Dostawca docker OMI. Zainstalować tylko w przypadku wykrycia Docker. |

### <a name="additional-installation-artifacts"></a>Artefakty dodatkowych instalacji
Po zainstalowaniu agenta pakietu OMS hello pakietów systemu Linux, hello następujące dodatkowe czynności konfiguracyjne systemowe zmiany zostaną zastosowane. Te artefakty muszą zostać usunięte po odinstalowaniu hello omsagent pakietu.

* Użytkownik bez uprawnień o nazwie: `omsagent` jest tworzony. To jest program hello konta hello omsagent demon działa jako
* Plik "Dołącz" sudoers jest tworzony w /etc/sudoers.d/omsagent to autoryzuje omsagent toorestart hello syslog i demonów omsagent. Jeśli dyrektywy "Dołącz" sudo nie są obsługiwane w wersji hello zainstalowany sudo, te wpisy zostaną zapisane zbyt/etc/sudoers.
* Konfiguracja syslog Hello jest zmodyfikowany tooforward podzbiór zdarzeń toohello agenta. Aby uzyskać więcej informacji, zobacz hello **Konfigurowanie zbierania danych** poniższej sekcji

### <a name="linux-data-collection-details"></a>Szczegóły pobierania danych systemu Linux
Witaj poniższej tabeli przedstawiono metody zbierania danych i inne szczegółowe informacje o jak zbierane są dane.

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
> Rsyslog lub syslog ng są wymagane toocollect komunikaty dziennika systemowego. demon syslog domyślne Hello w wersji 5 (sysklog) w wersji Red Hat Enterprise Linux, CentOS i Oracle Linux nie jest obsługiwana dla zbierania zdarzeń usługi syslog. toocollect syslog danych z tej wersji tych dystrybucji hello rsyslog demon powinien być zainstalowany i skonfigurowany tooreplace sysklog.
>
>

## <a name="quick-install"></a>Szybkiej instalacji
Uruchom następujące polecenia toodownload hello omsagent hello, weryfikowanie hello sumy kontrolnej, a następnie instalowanie i hello dołączyć agenta. Polecenia są dla 64-bitowej. Witaj identyfikator i klucz podstawowy znajdują się w portalu OMS hello w obszarze **ustawienia** na powitania **połączonych źródeł** kartę.

![szczegóły obszaru roboczego](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

Istnieje wiele innych metod tooinstall hello agent i jego uaktualnienie. Więcej o nich na [kroki tooinstall hello Agent pakietu OMS Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).

Można również wyświetlić hello [Azure przewodnik wideo](https://www.youtube.com/watch?v=mF1wtHPEzT0).

## <a name="choose-your-linux-data-collection-method"></a>Wybierz metodę zbierania danych systemu Linux
Jak można wybrać hello typy danych, która ma jak toocollect zależy od tego, czy ma portalu OMS hello toouse lub jeśli chcesz edytować różne pliki konfiguracji bezpośrednio na klientach systemu Linux. Jeśli wybierzesz toouse hello portal konfiguracji hello jest automatycznie wysyłane tooall klientów systemu Linux. Jeśli potrzebujesz różnych konfiguracji dla różnych klientów systemu Linux, będzie konieczne pliki klienta tooedit indywidualnie — lub użyj zamiast jak PowerShell DSC, Chef lub Puppet.

Można określić zdarzenia dziennika systemowego hello i liczniki wydajności, które mają toocollect za pomocą plików konfiguracji na komputerach z systemem Linux hello. *Jeśli została wybrana opcja tooconfigure zbierania danych przez edycję plików konfiguracyjnych agenta, należy wyłączyć Konfiguracja scentralizowana hello.*  Instrukcje znajdują się poniżej tooconfigure zbierania danych agenta hello pliki konfiguracji, a także konfiguracji centralnej toodisable wszystkich agentów OMS dla systemu Linux lub pojedynczych komputerów.

### <a name="disable-oms-management-for-an-individual-linux-computer"></a>Wyłącz zarządzanie OMS dla danego komputera systemu Linux
Scentralizowane zbieranie danych dla danych konfiguracji jest wyłączona dla danego komputera Linux z hello OMS_MetaConfigHelper.py skryptu. Może to być przydatne, jeśli podzbiorowi komputerów należy specjalne konfiguracji.

Konfiguracja scentralizowana toodisable:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

Konfiguracja scentralizowana Włącz toore:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a>Liczniki wydajności systemu Linux
Liczniki wydajności systemu Linux są podobne liczniki wydajności tooWindows — zarówno działają podobnie. Można użyć hello następujące procedury tooadd i skonfigurować je. Po dodaniu ich tooOMS, dane są zbierane dla nich co 30 sekund.

### <a name="tooadd-a-linux-performance-counter-in-oms"></a>tooadd licznika wydajności systemu Linux w OMS
1. tooconfigure OMS agentów dla systemu Linux przy użyciu portalu OMS hello, można dodać liczniki wydajności systemu Linux na stronie Ustawienia powitania kliknij **danych**.  
2. Na powitania **ustawienia** w obszarze **danych** , kliknij przycisk **liczników wydajności systemu Linux** , a następnie wybierz lub wpisz nazwę hello licznika hello ma tooadd.  
    ![dane](./media/log-analytics-linux-agents/oms-settings-data01.png)
3. Jeśli nie znasz hello Pełna nazwa licznika hello, możesz wpisać nazwę częściowe i zostanie wyświetlona lista dostępnych liczników. Po znalezieniu licznika hello mają tooadd, kliknij nazwę hello liście hello a następnie kliknij przycisk hello plus hello tooadd ikona licznika.
4. Po dodaniu licznika hello pojawia się liście hello wyróżnione z paskiem kolorowe liczników.
5. Domyślnie program hello **Zastosuj poniżej maszyny toomy konfiguracji** opcja jest zaznaczona. Jeśli chcesz toodisable wysyłanie danych konfiguracji, należy usunąć zaznaczenie hello.
6. Po zakończeniu modyfikowania liczniki wydajności, u dołu strony hello powitania kliknij **zapisać** toofinalize zmiany. Hello zmian konfiguracji, które zostały wprowadzone są następnie wysyłane hello tooall OMS agentów dla systemu Linux, które są zarejestrowane w usłudze OMS, zazwyczaj w ciągu 5 minut.

### <a name="configure-linux-performance-counters-in-oms"></a>Konfigurowanie liczników wydajności systemu Linux w OMS
Do liczników wydajności systemu Windows można wybrać określonego wystąpienia dla każdego licznika wydajności. Do liczników wydajności systemu Linux, niezależnie od wystąpienia wybranego licznika stosuje liczniki podrzędnych tooall hello nadrzędnego licznika. Witaj poniższej tabeli przedstawiono typowe wystąpień hello tooboth dostępne liczniki wydajności systemu Linux i Windows.

| **Nazwa wystąpienia** | **Znaczenie** |
| --- | --- |
| \_Całkowita liczba |Całkowita liczba wszystkich wystąpień hello |
| \* |Wszystkie wystąpienia |
| (/ &#124; / var) |Dopasowuje wystąpienia o nazwie: / lub /var |

Podobnie hello interwału wybranego licznika nadrzędnego stosuje tooall jego liczniki podrzędnych. Innymi słowy wszystkie interwałów próbkowania licznika podrzędnych hello i wystąpienia są również powiązane ze sobą.

### <a name="add-and-configure-performance-metrics-with-linux"></a>Dodawanie i Konfigurowanie metryki wydajności z systemem Linux
Toocollect metryki wydajności są kontrolowane przez konfigurację hello w/etc/opt/microsoft/omsagent/&lt;identyfikator obszaru roboczego&gt;/conf/omsagent.conf. Zobacz [metryki wydajności dostępne](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) dostępnych klas i metryki dla hello Agent pakietu OMS dla systemu Linux.

Każdy obiekt lub kategorii toocollect metryki wydajności powinien być zdefiniowany w pliku konfiguracyjnym hello jako pojedynczy `<source>` elementu. Składnia Hello zgodny wzorcem hello poniżej.

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

można konfigurować parametry Hello tego elementu są:

* **Obiekt\_nazwa**: hello nazwę obiektu hello kolekcji.
* **Wystąpienie\_regex**: *wyrażenia regularnego* Definiowanie które toocollect wystąpień. Witaj wartość: `.*` określa wszystkich wystąpień. metryki procesora toocollect tylko hello \_całkowita liczba wystąpień, można określić `_Total`. Metryka procesu toocollect dla hello tylko wystąpienia crond lub sshd, można określić: `(crond|sshd)`.
* **Licznik\_nazwa\_wyrażenia regularnego**: *wyrażenia regularnego* Definiowanie które toocollect liczniki (dla obiekt hello). Określ wszystkie liczniki dla obiekt hello toocollect: `.*`. toocollect wymiany tylko miejsca liczniki dla obiekt pamięci hello, można określić:`.+Swap.+`
* **Interwał:**: hello częstotliwości, w których hello są zbierane liczniki obiektu.

Witaj konfigurację domyślną dla metryki wydajności jest:

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
Jeśli serwer MySQL lub MariaDB serwer zostanie wykryte na komputerze hello po zainstalowaniu pakietu omsagent hello, jest automatycznie instalowany dostawcy dla serwera MySQL monitorowania wydajności. Ten dostawca łączy toohello lokalnego MySQL/MariaDB tooexpose Statystyka wydajności serwera. Należy poświadczenia użytkownika MySQL tooconfigure, dzięki czemu hello dostawcy dostęp hello serwer MySQL.

toodefine domyślnego konta użytkownika serwera MySQL hello na hoście lokalnym, użyj hello poniższy przykład polecenia.

> [!NOTE]
> Plik poświadczeń Hello musi być do odczytu przez konto omsagent hello. Zalecane jest uruchomienie polecenia mycimprovauth hello jako omsgent.
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


Alternatywnie można określić hello wymagane poświadczenia MySQL w pliku, tworząc plik hello: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Aby uzyskać więcej informacji o zarządzaniu MySQL poświadczeń do monitorowania za pomocą pliku mysql auth hello, zobacz [MySQL zarządzania, monitorowania poświadczenia w pliku uwierzytelniania hello](#manage-mysql-monitoring-credentials-in-the-authentication-file).

Zobacz [bazy danych uprawnienia wymagane do liczników wydajności MySQL](#database-permissions-required-for-mysql-performance-counters) szczegółowe informacje o obiekcie uprawnień wymaganych przez hello MySQL użytkownika toocollect dane dotyczące wydajności serwera MySQL.

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a>Włącz Apache HTTP Server liczniki wydajności za pomocą poleceń systemu Linux
W przypadku wykrycia Apache HTTP Server na komputerze powitania po zainstalowaniu pakietu omsagent hello, jest automatycznie instalowany dostawcy dla Apache HTTP Server monitorowania wydajności. Ten dostawca zależy od Apache "module", który musi zostać załadowane do hello Apache HTTP Server w kolejności tooaccess danych dotyczących wydajności.

Można załadować modułu hello z hello następujące polecenie:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload hello Apache modułu monitorowania, uruchom następujące polecenie hello:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a>tooview danych wydajności przy użyciu analizy dzienników
1. W portalu usługi Operations Management Suite powitania kliknij hello wyszukiwania dziennika.
2. Na pasku wyszukiwania hello, wpisz `* (Type=Perf)` tooview wszystkie liczniki wydajności.

Ponieważ OMS również zbieranie danych licznika wydajności systemu Windows, użytkownik powinien zakresu rozwijanej hello dane specyficzne dla tooLinux wyszukiwania. Hello poniższy przykład czy Pokaż wydajności danych określonego tooan przykład Linux server o nazwie Chorizo21.

```
Type=Perf Computer=chorizo*
```

![przykład serwera wyświetlane w wynikach wyszukiwania](./media/log-analytics-linux-agents/oms-perfsearch01.png)

W wynikach powitania kliknij **metryki** tooview hello liczniki, które zebrano dane. Dane w czasie rzeczywistym jest wyświetlany na wykresach dla każdego licznika.

![metrics](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a>Dziennik systemu
SYSLOG jest zdarzeniem rejestrowania protokołu podobne tooWindows dzienniki zdarzeń — zarówno działają podobnie, podczas wyświetlania w OMS.

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a>tooadd nowego zakładu dziennika systemu Linux w OMS
1. Na powitania **ustawienia** w obszarze **danych** , kliknij przycisk **Syslog** a następnie toohello lewej hello i ikony, wpisz nazwę hello hello instrumentu syslog, które mają tooadd.
    ![Systemu Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)
2. Jeśli nie znasz hello Pełna nazwa instrumentu hello, możesz wpisać nazwę częściowe i zostanie wyświetlona lista dostępnych syslog urządzeń. Do wyszukania hello syslog zakładzie mają tooadd, kliknij nazwę hello liście hello a następnie kliknij przycisk hello plus hello tooadd ikona funkcję dziennika systemowego.
3. Po dodaniu zakładzie hello wydaje się liście hello wyróżnione z paskiem kolorowe. Następnie wybierz wag hello (kategorie informacji zakładzie syslog), które mają toocollect.
4. U dołu strony hello powitania kliknij **zapisać** toofinalize zmiany. Hello zmian konfiguracji, które zostały wprowadzone są następnie wysyłane hello tooall OMS agentów dla systemu Linux, które są zarejestrowane w usłudze OMS, zazwyczaj w ciągu 5 minut.

### <a name="configure-linux-syslog-facilities-in-linux"></a>Konfigurowanie urządzeń dziennika systemu Linux w systemie Linux
Zdarzenia dziennika systemowego są wysyłane z hello demon syslog, na przykład rsyslog lub syslog ng, portów lokalnych tooa hello agent nasłuchuje. Domyślnie port 25224. Po zainstalowaniu agenta hello domyślnej konfiguracji programu syslog jest stosowany. Znaleziono w lokalizacji:

Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf

SYSLOG ng: /etc/syslog-ng/syslog-ng.conf

Konfiguracja syslog agenta pakietu OMS domyślne Hello przekazuje zdarzenia dziennika systemowego z wszystkich urządzeń z ważnością, ostrzeżenie lub nowszej.

> [!NOTE]
> Edytuj hello syslog konfiguracji, należy ponownie uruchomić demon syslog hello hello zmiany tootake efektu.
>
>

Witaj syslog konfigurację domyślną dla hello Agent pakietu OMS dla systemu Linux dla OMS jest:

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

### <a name="tooview-all-syslog-events-with-log-analytics"></a>tooview wszystkie zdarzenia dziennika systemowego z analizy dzienników
1. W portalu usługi Operations Management Suite powitania kliknij hello **wyszukiwania dziennika** kafelka.
2. W hello **zarządzanie dziennikiem** grupowania, wybierz wyszukiwania wstępnie zdefiniowanych syslog, a następnie wybierz jeden toorun go.

Ten przykład przedstawia wszystkie zdarzenia dziennika systemowego.

![Zdarzenia dziennika systemowego pokazano wyszukiwania dziennika](./media/log-analytics-linux-agents/oms-linux-syslog.png)

Teraz możesz przejść do szczegółów wyników wyszukiwania.

## <a name="linux-alerts"></a>Alerty systemu Linux
Jeśli używasz Nagios lub Zabbix toomanage Twojego maszyny z systemem Linux, a następnie OMS może odbierać hello alerty generowane przez te narzędzia. Ponieważ nie ma obecnie nie metody tooconfigure przychodzących alertów danych przy użyciu portalu OMS hello. Zamiast tego należy tooedit wysyłania tooOMS alerty konfiguracji pliku toostart.

### <a name="collect-alerts-from-nagios"></a>Zbieraj alerty z Nagios
toocollect alertów z serwera Nagios, należy hello toomake następujące zmiany w konfiguracji.

1. Udziel hello użytkownika **omsagent** dostęp do odczytu pliku dziennika Nagios toohello (tj. /var/log/nagios/nagios.log). Zakładając, że plik nagios.log hello jest własnością grupy hello **nagios** , można dodać użytkownika hello **omsagent** toohello **nagios** grupy.

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. Modyfikowanie pliku omsagent.confconfiguration hello (/ etc/opt/microsoft/omsagent/&lt;identyfikator obszaru roboczego&gt;/conf/omsagent.conf). Upewnij się, że hello następujące wpisy są obecne i nie komentarze wychodzących:

    ```
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
    ```
3. Uruchom ponownie demon omsagent hello:

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a>Zbieraj alerty z Zabbix
toocollect alertów z serwera Zabbix będziesz wykonywać podobne kroki toothose dla Nagios powyżej, z wyjątkiem potrzebujesz toospecify użytkownika i hasło w *zwykły tekst*. To nie jest idealnym rozwiązaniem, ale prawdopodobnie zmienią się wkrótce. tooaddress ten problem, zaleca się tworzenie hello użytkownika, a następnie przyznać jej tylko toomonitor uprawnienia.

Przykład sekcji pliku konfiguracji omsagent.conf hello (/ etc/opt/microsoft/omsagent/&lt;identyfikator obszaru roboczego&gt;/conf/omsagent.conf) dla Zabbix powinno przypominać następujące hello:

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
Po skonfigurowaniu tooOMS alerty z systemem Linux komputerów toosend kilka prostych dziennika wyszukiwania zapytania tooview hello alerty mogą być używane. Witaj następującego zapytania wyszukiwania zwraca wszystkie alerty hello zarejestrowane, które zostały wygenerowane. Na przykład czy jakieś problem występuje w infrastrukturze IT, następnie w wyniku hello poniższy przykład zapytania może wskazywać, gdzie może pochodzić hello problem. I mogą łatwo przechodzenia w alertach toohello przez źródło systemu toohelp wąskie badaniu. Witaj korzyścią jest nie musi mieć systemy zarządzania toovarious toogo od początku hello — pod warunkiem, że alerty są wysyłane tooOMS, można uruchomić istnieje.

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a>tooview Nagios wszystkie alerty z analizy dzienników
1. W portalu usługi Operations Management Suite powitania kliknij hello **wyszukiwania dziennika** kafelka.
2. Na pasku zapytania hello wpisz hello następującego zapytania wyszukiwania

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Nagios alertów przedstawianych w dzienniku wyszukiwania](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

Po hello wyniki wyszukiwania, możesz przejść do szczegółów dodatkowych szczegółów takich jak *stan alertu*.

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a>tooview wszystkie alerty Zabbix z analizy dzienników
1. W portalu usługi Operations Management Suite powitania kliknij hello **wyszukiwania dziennika** kafelka.
2. Na pasku zapytania hello wpisz hello następującego zapytania wyszukiwania

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Zabbix alertów przedstawianych w dzienniku wyszukiwania](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

Po hello wyniki wyszukiwania, możesz przejść do szczegółów dodatkowych szczegółów takich jak *AlertName*.

## <a name="compatibility-with-system-center-operations-manager"></a>Zgodność z programem System Center Operations Manager
Witaj Agent pakietu OMS dla systemu Linux udostępnia pliki binarne agenta hello agenta programu System Center Operations Manager. Instalowanie hello Agent pakietu OMS dla systemu Linux w systemie, w obecnie zarządzany przez program Operations Manager uaktualnień hello OMI i SCX pakietów na komputerze hello tooa nowszej wersji. Witaj Agent pakietu OMS dla systemów Linux i System Center 2012 R2 są zgodne. Jednak **System Center 2012 SP1 i wcześniejsze wersje nie są obecnie zgodne lub nie jest obsługiwany z hello Agent pakietu OMS dla systemu Linux.**

> [!NOTE]
> Jeśli hello Agent pakietu OMS dla systemu Linux jest zainstalowana tooa komputera, który nie jest obecnie zarządzany przez program Operations Manager, a później mają toomanage hello komputera z programem Operations Manager, należy zmodyfikować konfigurację OMI hello przed odnajdowania hello komputera. **Ten krok jest zbędny, jeśli hello agenta programu Operations Manager została zainstalowana przed hello Agent pakietu OMS dla systemu Linux.**
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a>Witaj tooenable Agent pakietu OMS dla systemu Linux toocommunicate z programem Operations Manager
1. Edytuj hello /etc/opt/omi/conf/omiserver.conf pliku
2. Upewnij się, że powitania od wiersza z **httpsport =** definiuje hello portu 1270. Takie jak`httpsport=1270`
3. Uruchom ponownie serwer OMI hello:

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a>Uprawnienia bazy danych wymagane dla liczników wydajności MySQL
toogrant uprawnienia tooa MySQL monitorowania użytkownika, użytkownik udzielającym hello musi mieć uprawnienie "GRANT option" hello, jak również udzielenia uprawnienia hello.

Aby hello użytkownika MySQL tooreturn wydajności danych hello użytkownika będą muszą uzyskiwać dostęp do toohello następujące zapytania:

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

Ponadto toothese zapytania hello MySQL użytkownika wymagane są następujące domyślne tabele toohello dostępu wybierz OPCJĘ:

* INFORMATION_SCHEMA
* MySQL

Te uprawnienia można otrzymać, uruchamiając następujące polecenia grant hello.

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a>Zarządzanie monitorowania poświadczenia w pliku uwierzytelniania hello MySQL
Hello następujące sekcje ułatwiają zarządzanie poświadczeniami MySQL.

### <a name="configure-hello-mysql-omi-provider"></a>Skonfiguruj hello dostawcy MySQL OMI
Hello MySQL OMI dostawcy wymaga, aby użytkownik MySQL wstępnie skonfigurowane i zainstalowane w kolejności tooquery hello kondycji wydajności informacji z wystąpienia MySQL hello bibliotek klienta MySQL.

### <a name="mysql-omi-authentication-file"></a>Plik authentication MySQL OMI
Dostawca MySQL OMI używa toodetermine plik uwierzytelniania, jakiego bind adres i port wystąpienia MySQL hello nasłuchuje na i jakie poświadczenia toouse toogather metryki. Podczas instalacji hello MySQL OMI dostawcy rozpocznie skanowanie plików konfiguracyjnych my.cnf MySQL (lokalizacje domyślne) bind adres i port i częściowo hello zestaw plików uwierzytelniania MySQL OMI.

toocomplete monitorowanie wystąpienia serwera MySQL, dodać wstępnie wygenerowany plik authentication MySQL OMI w poprawnym katalogu hello.

### <a name="authentication-file-format"></a>Format pliku uwierzytelniania
Hello plik authentication MySQL OMI jest plik tekstowy, który zawiera informacje o:

* Port
* Adres BIND
* Nazwa_użytkownika MySQL
* Kodowanie Base64 hasła

Hello plik authentication MySQL OMI tylko przyznaje uprawnienia do odczytu/zapisu toohello Linux użytkownika, która go wygenerowała.

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

Domyślny plik authentication MySQL OMI zawiera domyślne wystąpienie i numer portu, w zależności od tego, jakie informacje są dostępne i przeanalizowany z hello znaleziono plik konfiguracji MySQL.

Hello domyślnego wystąpienia jest toomake oznacza wiele wystąpień MySQL na jednym hoście Linux łatwiejsze zarządzanie i jest oznaczona przez wystąpienie hello z portem 0. Wszystkie wystąpienia dodano będzie dziedziczyć właściwości z wystąpienia domyślnego hello. Na przykład jeśli wystąpienie MySQL nasłuchiwanie na porcie "3308" zostanie dodany, powiązanego adresu hello domyślnego wystąpienia, username i password kodowany w standardzie Base64 będzie można tootry używane i monitorowanie wystąpienia hello nasłuchiwanie 3308. Jeśli wystąpienie hello na 3308 jest tooanother powiązany adres i używa hello tego samego nazwa_użytkownika MySQL i para hasło tylko hello respecification hello bind adres jest niezbędny i hello inne właściwości dziedziczone.

Przykłady plik authentication hello przypominać następujące hello.

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
| Port |Port reprezentuje hello bieżącego portu hello MySQL nasłuchuje wystąpienie.  Hello port 0 oznacza, że następujące właściwości hello są używane dla domyślnego wystąpienia. |
| Adres BIND |Hello powiązać adres jest hello bieżący MySQL bind — adres |
| nazwa użytkownika |Tej nazwy użytkownika hello hello MySQL użytkownika mają wystąpienie serwera toouse toomonitor hello MySQL. |
| Hasło kodowane w formacie Base64 |Jest to hasło hello hello MySQL monitorowania użytkownika zakodowane w formacie Base64. |
| Aktualizacje automatyczne |Po uaktualnieniu hello MySQL OMI dostawcy dostawcy hello Skanuj ponownie zmiany w pliku my.cnf hello i Zastąp plik MySQL OMI Authentication hello. Tej flagi tootrue lub FAŁSZ w zależności od toohello wymagane aktualizacje MySQL OMI uwierzytelniania pliku zestawu. |

#### <a name="authentication-file-location"></a>Lokalizacja pliku uwierzytelniania
Witaj MySQL OMI uwierzytelniania plików powinny być znajduje się w następującej lokalizacji hello i o nazwie "mysql uwierzytelniania":

/var/OPT/Microsoft/MySQL-cimprov/auth/omsagent/MySQL-auth

Plik Hello (i katalog auth/omsagent) powinna być własnością hello omsagent użytkownika.

## <a name="agent-logs"></a>Dzienniki agentów
Dzienniki Hello hello Agent pakietu OMS dla systemu Linux jest na:

/ var/opt/microsoft/omsagent/&lt;identyfikator obszaru roboczego&gt;/log/

Dzienniki Hello hello wynosi Agent pakietu OMS dla systemu Linux dla programu omsconfig (konfiguracja agenta):

/ var/opt/microsoft/omsconfig/log /

Dzienniki dla składników OMI i SCX hello (udostępniających dane metryk wydajności) znajduje się na:

/ var/opt/omi/log/i /var/opt/microsoft/scx/log

## <a name="troubleshooting-hello-oms-agent-for-linux"></a>Rozwiązywanie problemów z hello Agent pakietu OMS dla systemu Linux
Użyj powitania po toodiagnose informacji i rozwiązywania typowych problemów.

Jeśli żaden z hello Rozwiązywanie problemów z informacjami w tej sekcji pomaga, umożliwia także hello następujące zasoby toohelp rozwiązanie problemu.

* Klienci z Premier pomocy technicznej można rejestrować sprawy pomocy technicznej za pośrednictwem [Premier](https://premier.microsoft.com/)
* Klienci z umowami pomocy technicznej platformy Azure może rejestrować przypadków pomocy technicznej w hello [portalu Azure](https://manage.windowsazure.com/?getsupport=true)
* Plik [problem GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)
* Forum opinii pomysły i toocreate raport o usterce [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)

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
> Edycji plików konfiguracyjnych dla liczników wydajności i syslog zostaną zastąpione, jeśli jest włączona konfiguracja portalu OMS. Możesz wyłączyć konfigurację w hello portalu OMS (dla wszystkich węzłów) lub pojedynczych węzłów, uruchamiając następujące hello:
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a>Włączenie rejestrowania debugowania
debugowania tooenable rejestrowania, można użyć hello OMS dane wyjściowe wtyczki i pełne dane wyjściowe.

#### <a name="oms-output-plugin"></a>Dodatek dane wyjściowe OMS
FluentD umożliwia toospecify wtyczki hello poziomów rejestrowania dla dziennika różne poziomy wejścia i wyjścia. toospecify poziomu inny dziennik OMS danych wyjściowych, zmień konfigurację agenta ogólne hello w hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` pliku.

Dolnej hello pliku konfiguracyjnego hello zmienić hello `log_level` właściwość z `info` zbyt`debug`.

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

Rejestrowanie debugowania umożliwia usługę oddzielone typ, liczba elementów danych, a czas trwania toosend toohello przekazywania toosee umieścić w zadaniu wsadowym.

*Przykładowy dziennik debugowania włączone:*

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a>Pełne dane wyjściowe
Zamiast używać hello OMS dane wyjściowe wtyczki, można również wyprowadzać elementów danych bezpośrednio za`stdout`, która jest widoczna w hello Agent pakietu OMS dla pliku dziennika systemu Linux.

W pliku konfiguracyjnym ogólne agent pakietu OMS hello na `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, komentarz hello OMS output wtyczki, dodając `#` przed każdym wierszu.

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

Poniżej hello wtyczki dane wyjściowe, Usuń komentarz hello w następujących sekcji, usuwając hello hello `#` symbol hello początku każdego wiersza.

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a>Przekazany dalej komunikaty dziennika systemowego nie są wyświetlane w dzienniku hello
#### <a name="probable-causes"></a>Prawdopodobne przyczyny
* Hello zastosowano konfigurację toohello Linux serwera nie zezwolić na zbieranie hello wysyłane urządzeń i/lub poziomy dziennika
* SYSLOG nie są przekazywane poprawnie toohello Linux serwera
* Witaj liczbę komunikatów przekazywanych na sekundę są za szerokie dla konfiguracji podstawowej hello hello Agent pakietu OMS dla systemu Linux toohandle

#### <a name="resolutions"></a>Rozwiązania
* Sprawdź tej konfiguracji hello w portalu OMS hello Syslog ma wszystkie urządzenia hello i poziomy dziennika poprawne hello
  * **Portalu OMS > Ustawienia > danych > Syslog**
* Sprawdź tego macierzystego syslog wiadomości demonów (`rsyslog`, `syslog-ng`) są możliwe tooreceive wiadomości powitania przekazywane
* Sprawdź ustawienia zapory na tooensure serwera Syslog hello czy wiadomości nie są blokowane
* Symulowanie tooOMS komunikatów Syslog, przy użyciu hello `logger` polecenia — na przykład:
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a>Problemy z połączeniem tooOMS przy użyciu serwera proxy
#### <a name="probable-causes"></a>Prawdopodobne przyczyny
* określony powitania serwera proxy podczas instalowania i konfigurowania agenta hello jest niepoprawny
* punkty końcowe usługi OMS Hello nie są whitelistested w centrum danych.

#### <a name="resolutions"></a>Rozwiązania
* Zainstaluj ponownie hello Agent pakietu OMS dla systemu Linux przy użyciu następującego polecenia z opcją hello hello `-v` włączone. Dzięki temu pełne dane wyjściowe agenta hello łączących się za pośrednictwem hello proxy toohello usługę.
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * Witaj w dokumentacji serwera proxy OMS na [Konfigurowanie hello agenta do użycia z serwera proxy HTTP](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)
* Sprawdź, że hello następujące punkty końcowe usługi OMS białej

| Zasób agenta | Porty |
| --- | --- |
| &#42;. ods.opinsights.Azure.com |Port 443 |
| &#42;. OMS.opinsights.Azure.com |Port 443 |
| ods.systemcenteradvisor.com |Port 443 |
| &#42;.blob.core.windows.net/ |Port 443 |

### <a name="a-403-error-is-displayed-when-onboarding"></a>Zostanie wyświetlony błąd 403 podczas dołączania
#### <a name="probable-causes"></a>Prawdopodobne przyczyny
* Witaj, Data i godzina są niepoprawne na serwerze z systemem Linux
* Hello identyfikator obszaru roboczego i klucz obszaru roboczego, używane są nieprawidłowe

#### <a name="resolution"></a>Rozwiązanie
* Sprawdź czas hello na serwerze Linux z hello `date` polecenia. Jeśli powitalne danych jest większa niż lub mniej niż 15 minut od hello bieżącą godzinę, dołączania kończy się niepowodzeniem. toocorrect, zaktualizuj hello datę i/lub strefy czasowej serwera z systemem Linux.
* najnowszą wersję hello Agent pakietu OMS Linux Hello powiadamia użytkownika, jeśli różnica czasu powoduje błąd dołączania
* Przy użyciu zintegrowanego środowiska odzyskiwania hello poprawny identyfikator i klucz obszaru roboczego. Zobacz [dołączania przy użyciu wiersza polecenia hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) Aby uzyskać więcej informacji.

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a>500 Błąd lub błąd 404 pojawia się w pliku dziennika powitania po dołączania
Jest to znany problem występujący podczas przekazywania pierwszy hello danych Linux pod obszarem roboczym pakietu OMS. Nie dotyczy to danych wysyłanych lub innych problemów. Możesz zignorować hello błędy podczas początkowego procesu dołączania.

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a>Nie ma danych Nagios hello portalu OMS
#### <a name="probable-causes"></a>Prawdopodobne przyczyny
* Witaj omsagent użytkownik nie ma tooread uprawnienia z pliku dziennika hello Nagios
* Hello Nagios źródła i sekcje filtru nadal są ujęte w pliku omsagent.conf hello

#### <a name="resolutions"></a>Rozwiązania
* Dodaj użytkownika omsagent hello w kolejności tooread z hello Nagios pliku. Zobacz [alerty Nagios](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) Aby uzyskać więcej informacji.
* W pliku konfiguracji ogólnej systemu Linux na hello Agent pakietu OMS `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, upewnij się, że **zarówno** hello Nagios źródłowy oraz filtr sekcje mają komentarze usuwane, toohello podobnie poniższy przykład.

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


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a>Dane systemu Linux nie jest wyświetlane w portalu OMS hello
#### <a name="probable-causes"></a>Prawdopodobne przyczyny
* Toohello dołączania usługę nie powiodło się.
* Toohello połączenia, który jest zablokowany przez usługę OMS
* Kopia zapasowa jest Hello Agent pakietu OMS danych systemu Linux

#### <a name="resolutions"></a>Rozwiązania
* Sprawdzić tego toohello dołączania usługę zakończyło się powodzeniem, upewniając się, że hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` istnieje.
* Przy użyciu zintegrowanego środowiska odzyskiwania hello omsadmin.sh wiersza polecenia. Zobacz [dołączania przy użyciu wiersza polecenia hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) Aby uzyskać więcej informacji.
* Jeśli przy użyciu serwera proxy, należy użyć hello proxy kroki rozwiązywania problemów powyżej
* W niektórych przypadkach gdy hello Agent pakietu OMS dla systemu Linux nie mogą komunikować się z hello usługę, dane na powitania agenta jest rozmiar buforu pełnej kopii zapasowej toohello 50 MB. Uruchom ponownie hello Agent pakietu OMS dla systemu Linux, uruchamiając hello `/opt/microsoft/omsagent/bin/service_control restart` polecenia.
  >[AZURE.NOTE] Tego problemu w 1.1.0-28 wersję agenta i nowszych.

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a>W portalu OMS hello nie zastosowano konfigurację liczników wydajności dziennika systemu Linux
#### <a name="probable-causes"></a>Prawdopodobne przyczyny
* agent konfiguracji Hello w hello Agent pakietu OMS dla systemu Linux nie odebrał hello najnowszej konfiguracji z portalu OMS hello.
* Witaj poprawione ustawień w portalu hello nie zostały zastosowane

#### <a name="resolutions"></a>Rozwiązania
`omsconfig`jest agentem konfiguracji hello w hello Agent pakietu OMS dla systemu Linux, które pobierają zmiany konfiguracji portalu OMS co 5 minut. Ta konfiguracja jest następnie zastosowane toohello Agent pakietu OMS dla systemu Linux pliki konfiguracji znajduje się w `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.

* W niektórych przypadkach hello Agent pakietu OMS dla systemu Linux konfiguracji agenta nie może być możliwe toocommunicate z usługą konfiguracji portalu hello powodujące najnowszej konfiguracji nie są stosowane.
* Sprawdź, że hello `omsconfig` agent został zainstalowany z następujących hello:

  * `dpkg --list omsconfig` lub `rpm -qi omsconfig`
  * Jeśli nie jest zainstalowany, zainstaluj ponownie najnowszą wersję hello hello Agent pakietu OMS dla systemu Linux
* Sprawdź, że hello `omsconfig` agenta może komunikować się z hello usługę

  * Uruchom hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` polecenia
    * Witaj polecenie powyżej zwraca hello konfigurację agenta pobiera z portalu hello, w tym ustawienia Syslog, liczniki wydajności systemu Linux i dzienników niestandardowych
    * W przypadku niepowodzenia powyższego polecenia hello Uruchom hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` polecenia. To polecenie wymusza hello omsconfig agenta toocommunicate hello OMS usługi tooretrieve hello najnowszej konfiguracji.

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a>Niestandardowe dane dziennika systemu Linux nie jest wyświetlany w hello portalu OMS
#### <a name="probable-causes"></a>Prawdopodobne przyczyny
* TooOMS przechodzenia do usługi nie powiodło się.
* Witaj **hello Zastosuj następujące toomy konfiguracji serwerów z systemem Linux** ustawienia nie zostały wybrane.
* omsconfig nie została pobrana hello najnowsze dziennik niestandardowy z portalu hello
* Witaj `omsagent` użycie jest dziennik niestandardowy hello tooaccess powodu tooa uprawnień problem lub `omsagent` nie został znaleziony. W takim przypadku zostanie wyświetlony hello następujące dane wyjściowe:
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* Jest to znany problem dotyczący hello sytuacji wyścigu, który został rozwiązany w hello Agent pakietu OMS dla 1.1.0-217 wersji systemu Linux

#### <a name="resolutions"></a>Rozwiązania
* Sprawdź, czy udało Ci się pomyślnie został załadowany, określając, czy hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` plik istnieje.
  * Jeśli potrzebne, dodać ponownie przy użyciu wiersza polecenia omsadmin.sh hello. Zobacz [dołączania przy użyciu wiersza polecenia hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) Aby uzyskać więcej informacji.
* W hello w portalu OMS **ustawienia** na powitania **danych** karcie, upewnij się, że hello **hello Zastosuj następujące toomy konfiguracji serwerów z systemem Linux** wybrane ustawienie  
  ![Zastosuj konfigurację](./media/log-analytics-linux-agents/customloglinuxenabled.png)
* Sprawdź, że hello `omsconfig` agenta może komunikować się z hello usługę

  * Uruchom hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` polecenia
  * Witaj polecenie powyżej zwraca hello konfigurację agenta pobiera z hello portalu, w tym ustawienia Syslog, liczniki wydajności systemu Linux i dzienników niestandardowych
  * W przypadku niepowodzenia powyższego polecenia hello Uruchom hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` polecenia. To polecenie wymusza hello omsconfig agenta toocommunicate z usługą OMS i pobrania najnowszej konfiguracji hello.

Zamiast hello Agent pakietu OMS dla użytkownika w systemie Linux uruchomiony jako użytkownik uprzywilejowanych `root`, hello Agent pakietu OMS dla systemu Linux jest uruchamiany jako hello `omsagent` użytkownika. W większości przypadków należy jawne uprawnienia przyznane użytkownikowi toohello w kolejności tooread niektórych plików.

uprawnienie toogrant zbyt`omsagent` użytkownika, uruchom następujące polecenia hello:

1. Dodaj hello `omsagent` użytkownika tooa określonej grupy z`sudo usermod -a -G <GROUPNAME> <USERNAME>`
2. Przyznaj wymaganego pliku toohello Uniwersalny dostęp do odczytu z`sudo chmod -R ugo+rw <FILE DIRECTORY>`

Istnieje znany problem dotyczący hello sytuacji wyścigu, który został rozwiązany w hello Agent pakietu OMS dla 1.1.0-217 wersji systemu Linux. Po zaktualizowaniu toohello najnowsza wersja agenta, uruchom hello następujące polecenia tooget hello najnowszą wersję hello dane wyjściowe wtyczki:

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a>Znane ograniczenia
Przejrzyj powitania po toolearn sekcje zawierają informacje o bieżącym ograniczenia hello Agent pakietu OMS dla systemu Linux.

### <a name="azure-diagnostics"></a>Diagnostyka Azure
Dla maszyn wirtualnych systemu Linux działających na platformie Azure dodatkowe czynności może być wymagane tooallow zbierania danych przez diagnostyki Azure i usługi Operations Management Suite. **W wersji 2.2** hello rozszerzenia diagnostyki dla systemu Linux jest wymagany dla zgodności z hello Agent pakietu OMS dla systemu Linux.

Aby uzyskać więcej informacji o instalowaniu i konfigurowaniu hello diagnostycznych rozszerzenia dla systemu Linux, zobacz [Użyj tooenable polecenia interfejsu wiersza polecenia Azure hello rozszerzenia diagnostycznych Linux](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).

**Uaktualnianie hello rozszerzenia diagnostyki Linux z too2.2 2.0 ASM interfejsu wiersza polecenia platformy Azure:**

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

**ARM**

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

Plik o nazwie PrivateConfig.json odwoływać się do tych przykładach poleceń. format Hello ten plik powinien być podobny hello następujące przykładowe.

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a>Sysklog nie jest obsługiwane.
Rsyslog lub syslog ng są wymagane toocollect komunikaty dziennika systemowego. demon syslog domyślne Hello w wersji 5 (sysklog) w wersji Red Hat Enterprise Linux, CentOS i Oracle Linux nie jest obsługiwana dla zbierania zdarzeń usługi syslog. toocollect syslog danych z tej wersji tych dystrybucji hello rsyslog demon powinien być zainstalowany i skonfigurowany tooreplace sysklog. Aby uzyskać więcej informacji o zamianę sysklog rsyslog, zobacz [zainstalować hello nowo utworzony rsyslog obr. / min](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).

## <a name="next-steps"></a>Następne kroki
* [Dodawanie rozwiązania analizy dzienników z galerii rozwiązań hello](log-analytics-add-solutions.md) tooadd funkcjonalność i zbieranie danych.
* Zapoznaj się z [dziennika wyszukiwania](log-analytics-log-searches.md) tooview szczegółowe informacje zebrane przez rozwiązania.
* Użyj [pulpity nawigacyjne](log-analytics-dashboards.md) toosave i wyświetlanie własne wyszukiwania.
