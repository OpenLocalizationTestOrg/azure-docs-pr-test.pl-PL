---
title: "aaaWire dane rozwiązanie w Log Analytics | Dokumentacja firmy Microsoft"
description: "Podczas transmisji danych jest skonsolidowanych danych sieci i wydajności z komputerów z agentami OMS, w tym programu Operations Manager oraz agenci połączone z systemem Windows. Dane sieci są łączone z toohelp danych z dziennika skorelować danych."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: banders
ms.openlocfilehash: adafdf98dfbda9d87759643a1a606a84eafd1348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a>Podczas transmisji danych 2.0 (wersja zapoznawcza) rozwiązania analizy dzienników

![Podczas transmisji danych symbolu](./media/log-analytics-wire-data/wire-data2-symbol.png)

Podczas transmisji danych jest skonsolidowanych danych sieci i wydajności z komputerów z agentów OMS, w tym programu Operations Manager, połączony z systemem Windows i Linux agentów. Dane sieci są łączone z Twojej innych toohelp danych dziennika skorelować danych.

Ponadto agentów tooOMS hello udostępniający dane rozwiązanie korzysta z agentów Dependency firmy Microsoft, które można zainstalować na komputerach w infrastrukturze IT. Tooand dane przesyłane zależności agentów monitora sieci z komputerów w sieci poziomy hello w 2 – 3 [OSI model](https://en.wikipedia.org/wiki/OSI_model), w tym hello różnych protokoły i porty używane. Dane są następnie wysyłane tooLog Analytics przy użyciu agentów.

> [!NOTE]
> Nie można dodać hello poprzedniej wersji hello udostępniający dane rozwiązanie toonew w obszarach roboczych. Jeśli masz hello oryginalnym rozwiązaniu udostępniający dane włączone, można kontynuować toouse go. Jednak toouse podczas transmisji danych 2.0, należy najpierw usunąć hello oryginalną wersją.

Domyślnie analizy dzienników zbiera dane zarejestrowane dla Procesora, pamięci, dysku i sieci danych wydajności z liczników wbudowanego w systemie Windows. Sieci i innych zbieranie danych odbywa się w czasie rzeczywistym dla każdego agenta, włącznie z podsieci i używany przez komputer hello protokoły poziomu aplikacji. Na stronie Ustawienia hello na karcie dzienniki hello można dodać liczniki wydajności.

Jeśli użyto [sFlow](http://www.sflow.org/) lub innego oprogramowania z [protokołu NetFlow firmy Cisco](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), następnie hello statystyk i dane pochodzące z udostępniający dane zostaną tooyou znane.

Oto niektóre z hello typy wbudowane zapytań wyszukiwania dziennika:

- Agenci udostępniający dane
- Adres IP agentów udostępniających dane o komunikacji sieciowej
- Komunikacja wychodząca według adresów IP
- Liczba bajtów wysłanych przez protokoły aplikacji
- Liczba bajtów wysłanych przez usługę aplikacji
- Bajty odebrane przez różnych protokołów
- Całkowita liczba bajtów wysłanych i odebranych według wersji adresu IP
- Średni czas oczekiwania dla połączenia, które zostały wiarygodny
- Komputer przetwarza sieciowej zainicjowały lub odebrały ruch
- Ilość ruchu sieciowego dla procesu

Podczas wyszukiwania przy użyciu udostępniający dane, można filtrować i grupy danych tooview informacji o hello top agentów i protokoły top. Lub kiedy można wyświetlić niektórych komputerów (adresów IP adresy MAC) przekazywane ze sobą, jak długo i ilość danych została wysłana — zasadniczo wyświetlić metadane dotyczące ruchu sieciowego, który jest na podstawie wyszukiwania.

Jednak ponieważ wyświetlasz metadanych nie jest zawsze przydatne podczas rozwiązywania szczegółowe. Podczas transmisji danych analizy dzienników nie jest pełną przechwytywania danych w sieci. Tak nie ma ona do rozwiązywania problemów głębokość poziomie pakietów. Witaj zaletą hello agenta, metody kolekcji tooother w porównaniu, czy nie ma urządzeń tooinstall, skonfiguruj ponownie przełączników sieciowych lub przeprowadzić skomplikowane konfiguracje. Podczas transmisji danych jest po prostu agenta na podstawie — należy zainstalować na komputerze agenta hello i będzie monitorować ruch sieci. Inną zaletą jest w przypadku obciążeń toomonitor działających w chmurze dostawcy lub dostawcy usług hostingowych lub Microsoft Azure, gdzie hello użytkownika nie posiada hello warstwy sieci szkieletowej.

## <a name="connected-sources"></a>Połączone źródła

Podczas transmisji danych dane są pobierane z hello Microsoft Dependency Agent. Hello Dependency Agent jest zależna od hello Agent pakietu OMS dla jego tooLog połączeń Analytics. To oznacza, że serwer musi mieć hello Agent pakietu OMS zainstalowany i skonfigurowany pierwszy, a następnie zainstaluj hello Dependency Agent. Witaj poniższej tabeli opisano źródeł hello połączone, które obsługuje hello udostępniający dane rozwiązanie.

| **Źródło połączenia** | **Obsługiwane** | **Opis** |
| --- | --- | --- |
| Agenci dla systemu Windows | Tak | Podczas transmisji danych analizuje i zbiera dane z komputerów z systemem Windows agenta. <br><br> W przypadku dodawania toohello [Agent pakietu OMS](log-analytics-windows-agents.md), agentów systemu Windows wymagają hello Microsoft Dependency Agent. Zobacz hello [obsługiwanych systemów operacyjnych](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) pełną listę wersji systemu operacyjnego. |
| Agenci dla systemu Linux | Tak | Podczas transmisji danych analizuje i zbiera dane z komputerów z systemem Linux agenta.<br><br> W przypadku dodawania toohello [Agent pakietu OMS](log-analytics-linux-agents.md), hello Microsoft Dependency Agent wymagają agentów systemu Linux. Zobacz hello [obsługiwanych systemów operacyjnych](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) pełną listę wersji systemu operacyjnego. |
| Grupa zarządzania programu System Center Operations Manager | Tak | Podczas transmisji danych analizuje i zbiera dane z agentów systemu Windows i Linux w połączonych [grupy zarządzania programu System Center Operations Manager](log-analytics-om-agents.md). <br><br> Połączenie bezpośrednie z tooLog komputera agenta programu System Center Operations Manager hello Analytics jest wymagana. Dane są przesyłane z tooLog grupy zarządzania hello Analytics. |
| Konto magazynu Azure | Nie | Podczas transmisji danych zbiera dane z komputery agenta, więc nie ma żadnych danych z niego toocollect z usługi Magazyn Azure. |

W systemie Windows hello Microsoft Monitoring Agent (MMA) jest używany przez toogather zarówno System Center Operations Manager, jak i analizy dzienników i przesyłania danych. W zależności od kontekstu hello agenta hello jest nazywany hello agenta programu System Center Operations Manager, Agent pakietu OMS, Agent analizy dziennika, MMA lub bezpośredniego agenta. System Center Operations Manager i Log Analytics zapewnia nieco inne wersje hello MMA. Te wersje strony każdy raport tooSystem Center Operations Manager, tooLog analityka lub tooboth.

W systemie Linux hello Agent pakietu OMS Linux zbiera i wysyła dane tooLog Analytics. Na serwerach z agentami bezpośredniego OMS lub na serwerach, które są dołączone tooLog Analytics za pomocą grup zarządzania programu System Center Operations Manager, można użyć podczas transmisji danych.

W tym artykule odwołuje się do agentów tooall czy Linux lub Windows, czy grupa zarządzania programu System Center Operations Manager połączonych tooa lub bezpośrednio tooLog Analytics nazywamy hello _agent pakietu OMS_. Użyjemy hello nazwę określonego wdrożenia agenta hello tylko wtedy, gdy jest wymagana dla kontekstu.

Hello Dependency Agent nie przesyła wszystkie dane, a nie wymaga żadnych zmian toofirewalls lub porty. Hello dane udostępniający dane są zawsze przesyłane przez tooLog agent pakietu OMS hello Analytics, albo bezpośrednio lub za pomocą hello OMS bramy.

![diagram agenta](./media/log-analytics-wire-data/agents.png)

Jeśli jesteś użytkownikiem programu System Center Operations Manager z tooLog podłączone grupy zarządzania Analytics:

- Dodatkowa konfiguracja nie jest wymagana, gdy agentów programu System Center Operations Manager można uzyskać dostęp do hello Internet tooconnect tooLog Analytics.
- Gdy agentów programu System Center Operations Manager nie może uzyskać dostęp do analizy dzienników za pośrednictwem Internetu hello należy tooconfigure hello bramy OMS toowork z programem System Center Operations Manager.

Jeśli używasz hello bezpośredniego agenta należy tooconfigure hello OMS samego agenta, tooLog tooconnect analityka lub tooyour OMS bramy. Witaj OMS bramy można pobrać z hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).

## <a name="prerequisites"></a>Wymagania wstępne

- Wymaga hello [szczegółowe dane i analiza](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) oferta rozwiązania.
- Jeśli używasz hello poprzedniej wersji hello udostępniający dane rozwiązanie, należy najpierw usunąć go. Jednak wszystkie dane zarejestrowane przez hello oryginalnym rozwiązaniu udostępniający dane są nadal dostępne w podczas transmisji danych w wersji 2.0 i wyszukiwania dziennika.
- Uprawnienia administratora są wymagane tooinstall lub odinstalować hello Dependency Agent.
- Witaj Dependency Agent musi zainstalowany na komputerze z 64-bitowym systemie operacyjnym.

### <a name="operating-systems"></a>Systemy operacyjne

Witaj poniższe sekcje zawierają listę hello obsługiwane systemy operacyjne dla hello Dependency Agent. Podczas transmisji danych nie obsługuje architektury 32-bitowego dla dowolnego systemu operacyjnego.

#### <a name="windows-server"></a>Windows Server

- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1

#### <a name="windows-desktop"></a>Pulpit systemu Windows

- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux, CentOS Linux i Oracle Linux (z RHEL jądra)

- Obsługiwane są tylko domyślnej i wersjach jądra systemu Linux SMP.
- Zwalnia jądra niestandardowe, takie jak rozszerzenia adresu fizycznego i Xen, nie są obsługiwane dla dowolnego dystrybucji systemu Linux. Na przykład system z wersji ciąg hello _2.6.16.21-0.8-xen_ nie jest obsługiwane.
- Niestandardowe jądra, w tym ponownych kompilacji standardowe jądra, nie są obsługiwane.
- CentOSPlus jądra nie jest obsługiwane.
- Oracle podzielenie Enterprise jądra (UEK) zostało opisane w dalszej części tego artykułu.

#### <a name="red-hat-linux-7"></a>Red Hat Linux 7

| **Wersja systemu operacyjnego** | **Wersja jądra** |
| --- | --- |
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7.2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6

| **Wersja systemu operacyjnego** | **Wersja jądra** |
| --- | --- |
| 6.0 | 2.6.32-71 |
| 6.1 | 2.6.32-131 |
| 6.2 | 2.6.32-220 |
| 6.3 | 2.6.32-279 |
| 6.4 | 2.6.32-358 |
| 6.5 | 2.6.32-431 |
| 6.6 | 2.6.32-504 |
| 6.7 | 2.6.32-573 |
| 6.8 | 2.6.32-642 |

#### <a name="red-hat-linux-5"></a>Red Hat Linux 5

| **Wersja systemu operacyjnego** | **Wersja jądra** |
| --- | --- |
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398 <br> 2.6.18-400 <br>2.6.18-402 <br>2.6.18-404 <br>2.6.18-406 <br> 2.6.18-407 <br> 2.6.18-408 <br> 2.6.18-409 <br> 2.6.18-410 <br> 2.6.18-411 <br> 2.6.18-412 <br> 2.6.18-416 <br> 2.6.18-417 <br> 2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Linux przedsiębiorstwa z jądra podzielenie Enterprise

#### <a name="oracle-linux-6"></a>Oracle Linux 6

| **Wersja systemu operacyjnego** | **Wersja jądra** |
| --- | --- |
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4 | Oracle 2.6.39-400 (UEK R2) |
| 6.5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| **Wersja systemu operacyjnego** | **Wersja jądra** |
| --- | --- |
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11

| **Wersja systemu operacyjnego** | **Wersja jądra** |
| --- | --- |
| 11 | 2.6.27 |
| 11 Z DODATKIEM SP1 | 2.6.32 |
| 11 Z DODATKIEM SP2 | 3.0.13 |
| 11 Z DODATKIEM SP3 | 3.0.76 |
| 11 Z DODATKIEM SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10

| **Wersja systemu operacyjnego** | **Wersja jądra** |
| --- | --- |
| Z DODATKIEM SP4 10 | 2.6.16.60 |

#### <a name="dependency-agent-downloads"></a>Zależności agenta pliki do pobrania

| **Plik** | **SYSTEM OPERACYJNY** | **Wersja** | **ALGORYTM SHA-256** |
| --- | --- | --- | --- |
| [InstallDependencyAgent Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |



## <a name="configuration"></a>Konfiguracja

Wykonaj następujące kroki tooconfigure hello udostępniający dane rozwiązanie dla obszarów roboczych hello.

1. Włącz rozwiązania analizy dziennika aktywności hello z hello [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) lub za pomocą hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).
2. Zainstaluj hello Dependency Agent na każdym komputerze, na którym chcesz tooget dane. Witaj Dependency Agent można monitorować sąsiadów tooimmediate połączeń, więc nie trzeba agenta na każdym komputerze.

### <a name="install-hello-dependency-agent-on-windows"></a>Zainstaluj hello Dependency Agent w systemie Windows

Uprawnienia administratora są wymagane tooinstall lub odinstaluj agenta hello.

Witaj Dependency Agent jest zainstalowany na komputerach z systemem Windows za pośrednictwem InstallDependencyAgent Windows.exe. Po uruchomieniu tego pliku wykonywalnego bez żadnych opcji uruchamia kreatora, że możesz wykonać tooinstall interaktywnie.

Użyj następujących kroków tooinstall hello Dependency Agent na każdym komputerze z systemem Windows hello:

1. Zainstaluj hello Agent pakietu OMS za pomocą instrukcji hello na [toohello komputerów Windows połączenia usługi Analiza dzienników w usłudze Azure](log-analytics-windows-agents.md).
2. Pobierz agenta systemu Windows hello za pomocą łącza hello hello w poprzedniej sekcji, a następnie uruchom go za pomocą następującego polecenia hello: InstallDependencyAgent Windows.exe
3. Wykonaj hello kreatora tooinstall hello agenta.
4. W przypadku niepowodzenia toostart hello Dependency Agent Sprawdź hello dzienniki, aby uzyskać szczegółowe informacje o błędzie. Na agentów systemu Windows hello katalog dziennika jest %Programfiles%\Microsoft Agent\logs zależności.

#### <a name="windows-command-line"></a>Wiersz polecenia systemu Windows

Za pomocą opcji z powitania po tooinstall tabeli z wiersza polecenia. toosee listę flagi instalacji hello, uruchom Instalatora hello przy użyciu hello /? Flaga w następujący sposób.

InstallDependencyAgent Windows.exe /?

| **Flaga** | **Opis** |
| --- | --- |
| <code>/?</code> | Pobierz listę hello opcje wiersza polecenia. |
| <code>/S</code> | Wykonaj instalację dyskretną bez monitowania użytkownika. |

Pliki dla agenta zależności Windows hello są umieszczane w C:\Program Files\Microsoft Dependency Agent domyślnie.

### <a name="install-hello-dependency-agent-on-linux"></a>Zainstaluj hello Dependency Agent w systemie Linux

Dostęp do konta root jest wymagane tooinstall lub skonfigurować hello agenta.

Witaj Dependency Agent jest zainstalowany na komputery z systemem Linux za pomocą Linux64.bin InstallDependencyAgent, skrypt powłoki z samowyodrębniający plikiem binarnym. Plik hello można uruchomić przy użyciu _sh_ lub Dodaj sam plik toohello uprawnienia do wykonania.

Użyj hello następujące kroki tooinstall hello Dependency Agent na każdym komputerze z systemem Linux:

1. Zainstaluj hello Agent pakietu OMS za pomocą instrukcji hello na [zbierania danych i zarządzać nimi z komputerów z systemem Linux](log-analytics-agent-linux.md).
2. Pobierz agenta systemu Linux zależności hello za pomocą łącza hello w poprzedniej sekcji hello, a następnie zainstaluj go jako głównego za pomocą następującego polecenia hello: sh InstallDependencyAgent Linux64.bin
3. W przypadku niepowodzenia toostart hello Dependency Agent Sprawdź hello dzienniki, aby uzyskać szczegółowe informacje o błędzie. Na agentów systemu Linux jest katalog dziennika hello: /var/opt/microsoft/dependency-agent/log.

toosee listę flagi instalacji hello, uruchom program instalacyjny hello z hello `-help` Flaga w następujący sposób.

```
InstallDependencyAgent-Linux64.bin -help
```

| **Flaga** | **Opis** |
| --- | --- |
| <code>-help</code> | Pobierz listę hello opcje wiersza polecenia. |
| <code>-s</code> | Wykonaj instalację dyskretną bez monitowania użytkownika. |
| <code>--check</code> | Sprawdź uprawnienia i hello systemu operacyjnego, ale nie należy instalować hello agenta. |

Pliki hello Dependency Agent są umieszczane w hello następujące katalogi:

| **Pliki** | **Lokalizacja** |
| --- | --- |
| Podstawowe pliki | /OPT/Microsoft/Dependency-Agent |
| Pliki dziennika | /var/OPT/Microsoft/Dependency-Agent/log |
| Pliki konfiguracji | /etc/OPT/Microsoft/Dependency-Agent/config |
| Pliki wykonywalne usługi | /OPT/Microsoft/Dependency-Agent/bin/Microsoft-Dependency-Agent<br><br>/OPT/Microsoft/Dependency-Agent/bin/Microsoft-Dependency-Agent-Manager |
| Pliki binarne magazynu | /var/OPT/Microsoft/Dependency-Agent/Storage |

### <a name="installation-script-examples"></a>Przykłady skryptów instalacji

tooeasily wdrażanie hello Dependency Agent na wiele serwerów na raz, ale toouse skryptu. Można użyć następującego skryptu przykłady toodownload hello i zainstalować hello Dependency Agent w systemie Windows lub Linux.

#### <a name="powershell-script-for-windows"></a>Skrypt programu PowerShell dla systemu Windows

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a>Skrypt powłoki dla systemu Linux

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a>Konfiguracja żądanego stanu

Witaj toodeploy Dependency Agent za pomocą konfiguracji żądanego stanu można użyć modułu xPSDesiredStateConfiguration hello i kod, takie jak następujące hello:

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install hello Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-hello-dependency-agent"></a>Odinstaluj hello Dependency Agent

Użyj hello następujące sekcje toohelp Usuń hello Dependency Agent.

#### <a name="uninstall-hello-dependency-agent-on-windows"></a>Odinstaluj hello Dependency Agent w systemie Windows

Administrator może odinstalować hello zależności agenta dla systemu Windows za pomocą Panelu sterowania.

Administrator można również uruchomić %Programfiles%\Microsoft Agent\Uninstall.exe zależności toouninstall hello Dependency Agent.

#### <a name="uninstall-hello-dependency-agent-on-linux"></a>Odinstaluj hello Dependency Agent w systemie Linux

Odinstaluj toocompletely hello Dependency Agent z systemem Linux, należy usunąć samego agenta hello i hello łącznik, który jest automatycznie instalowany z hello agenta. Można je odinstalować, zarówno przy użyciu hello następującego polecenia:

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a>Pakiety administracyjne

Po aktywowaniu podczas transmisji danych w obszarze roboczym analizy dzienników pakietu administracyjnego 300 KB są wysyłane tooall serwerów z systemem Windows hello w tym obszarze roboczym. Jeśli używasz programu System Center Operations Manager agentów w [podłączonej grupy zarządzania](log-analytics-om-agents.md), wdrożeniu hello monitora zależności pakietu administracyjnego programu System Center Operations Manager. Jeśli agenci hello są połączone bezpośrednio Log Analytics zapewnia hello pakietu administracyjnego.

Pakiet administracyjny Hello nosi nazwę Microsoft.IntelligencePacks.ApplicationDependencyMonitor. Jest ona zapisywana w: %Programfiles%\Microsoft monitorowania Agent\Agent\Health usługi State\Management pakietów. źródło danych Hello, który korzysta z pakietu administracyjnego hello jest: % Program files%\Microsoft monitorowanie Agent\Agent\Health usługi State\Resources&lt;AutoGeneratedID&gt;\ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="using-hello-solution"></a>Za pomocą rozwiązania hello

**Instalowanie i konfigurowanie hello rozwiązania**

Użyj powitania po tooinstall informacji i skonfiguruj hello rozwiązania.

- Hello udostępniający dane rozwiązanie pobrania danych z komputerów z systemem Windows Server 2012 R2, Windows 8.1 i nowszych systemów operacyjnych.
- Microsoft .NET Framework 4.0 lub nowszy jest wymagany na miejscu tooacquire udostępniający dane z komputerów.
- Dodaj hello udostępniający dane rozwiązanie tooyour analizy dzienników roboczego przy użyciu hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md). Nie są wymagane żadne dalsze czynności konfiguracyjne.
- Jeśli chcesz tooview udostępniający dane dla konkretnego rozwiązania należy toohave hello rozwiązanie już dodany tooyour obszaru roboczego.

Po zostać zainstalowani agenci i zainstalowaniu hello rozwiązania, w obszarze roboczym pojawi się Kafelek hello podczas transmisji danych 2.0.

> [!NOTE]
> Obecnie musisz użyć hello OMS tooview portalu podczas transmisji danych. Nie można użyć hello tooview portalu Azure podczas transmisji danych.

![Podczas transmisji danych kafelków](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-hello-wire-data-20-solution"></a>Za pomocą rozwiązania hello podczas transmisji danych 2.0

W portalu OMS hello, kliknij przycisk hello **podczas transmisji danych 2.0** kafelka tooopen hello udostępniający dane z pulpitu nawigacyjnego. pulpit nawigacyjny Hello zawiera bloki hello hello w poniższej tabeli. Każdy blok wyświetla się too10 elementów pasujących do kryteriów w bloku hello określenia zakresu zakresu i czasu. Można uruchomić wyszukiwania dziennika, który zwraca wszystkie rekordy, klikając **zobaczyć wszystkie** u dołu hello bloku hello lub przez kliknięcie nagłówka bloku hello.

| **Blok** | **Opis** |
| --- | --- |
| Agenci przechwytujący ruch sieciowy | Pokazuje hello liczbę agentów, które są Przechwytywanie ruchu sieciowego i list hello top 10 komputerów, które są Przechwytywanie ruchu. Kliknij toorun numer hello dziennika wyszukiwanie <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>. Kliknij komputer w toorun listy hello zwracanie hello łączna liczba bajtów przechwytywane wyszukiwanie dziennika. |
| Lokalne podsieci | Pokazuje liczbę hello podsieci lokalne, które zostały odnalezione agentów.  Kliknij toorun numer hello dziennika wyszukiwanie <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> które wyświetla listę wszystkich podsieci z hello liczbę bajtów przesyłanych w ramach każdej z nich. Kliknij przycisk podsieci hello toorun listy wyszukiwania dziennika zwracanie hello łączna liczba bajtów przesyłanych w ramach hello podsieci. |
| Protokoły poziomu aplikacji | Pokazuje numer hello protokołów na poziomie aplikacji w użyciu, wykrywane przez agentów. Kliknij toorun numer hello dziennika wyszukiwanie <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>. Kliknij przycisk wyszukiwania dziennika, zwracając hello całkowita liczba bajtów wysłanych przy użyciu protokołu hello toorun protokołu. |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Podczas transmisji danych z pulpitu nawigacyjnego](./media/log-analytics-wire-data/wire-data-dash.png)

Można użyć hello **agenci przechwytujący ruch sieciowy** toodetermine bloku jaka przepustowość sieci jest są używane przez komputery. Ten blok pomoże Ci łatwo hello Znajdź _chattiest_ komputera w danym środowisku. Komputery te może być przeciążony działający nieprawidłowo lub przy użyciu więcej zasobów sieci niż zwykle.

![Przykład wyszukiwania dziennika](./media/log-analytics-wire-data/log-search-example01.png)

Analogicznie, można użyć hello **podsieci lokalne** toodetermine bloku ilość ruchu sieciowego jest przenoszona do podsieci. Użytkownicy często definiować podsieci wokół najważniejsze obszary, w przypadku ich aplikacji. Ten blok oferuje zapewnia wgląd w tych obszarach.

![Przykład wyszukiwania dziennika](./media/log-analytics-wire-data/log-search-example02.png)

Witaj **protokoły poziomu aplikacji** bloku przydaje się, dlatego warto wiedzieć, jakie protokoły są używane. Na przykład może oczekiwać SSH toonot jest używany w danym środowisku sieciowym. Wyświetlanie informacji o dostępnych w bloku hello można szybko potwierdzenia lub disprove Twoje oczekiwania.

![Przykład wyszukiwania dziennika](./media/log-analytics-wire-data/log-search-example03.png)

W tym przykładzie użytkownik może Wejdź do SSH szczegóły toosee komputery, które korzystają z protokołu SSH i inne szczegóły komunikacji.

![Pokaż wyniki wyszukiwania](./media/log-analytics-wire-data/ssh-details.png)

Jest również przydatne tooknow Jeśli ruchu protokołu jest zwiększenie lub zmniejszenie wraz z upływem czasu. Na przykład jeśli wzrasta hello ilość danych przesyłanych przez aplikację, która może być coś, co należy zwrócić uwagę, lub czy można znaleźć warte wymienienia.

## <a name="input-data"></a>Dane wejściowe

Podczas transmisji danych zbiera metadane dotyczące ruchu sieciowego przy użyciu agentów hello, które mają włączone. Każdy agent wysyła dane dotyczące co 15 s.

## <a name="output-data"></a>dane wyjściowe

Rekord o typie _WireData_ jest tworzony dla każdego typu danych wejściowych. Rejestruje WireData mają właściwości wyświetlane hello w poniższej tabeli:

| Właściwość | Opis |
|---|---|
| Computer (Komputer) | Nazwa komputera, w których zebrano dane |
| TimeGenerated | Czas hello rekordu |
| LocalIP | Adres IP komputera lokalnego hello |
| SessionState | Połączone lub rozłączone |
| ReceivedBytes | Liczba bajtów odebranych |
| ProtocolName | Nazwa hello protokół sieciowy używany |
| Wersję adresu IP ustawioną | Wersji protokołu IP |
| Kierunek | Przychodzący lub wychodzący |
| MaliciousIP | Adres IP znanego złośliwego źródła |
| Ważność | Ważność podejrzanych złośliwego oprogramowania |
| RemoteIPCountry | Kraj hello zdalny adres IP |
| ManagementGroupName | Nazwa grupy zarządzania programu Operations Manager hello |
| SourceSystem | Źródło, gdzie zostały zebrane dane |
| SessionStartTime | Czas rozpoczęcia sesji |
| SessionEndTime | Godzina zakończenia sesji |
| LocalSubnet | Podsieć, w których zebrano dane |
| LocalPortNumber | Numer portu lokalnego |
| RemoteIP | Zdalny adres IP używany przez komputer zdalny hello |
| RemotePortNumber | Numer portu używany przez hello zdalny adres IP |
| Identyfikator sesji | Unikatowa wartość, która identyfikuje sesji komunikacji między dwoma adresami IP |
| SentBytes | Liczba bajtów wysłanych |
| TotalBytes | Całkowita liczba bajtów wysłanych podczas sesji |
| ApplicationProtocol | Typ protokołu sieciowego używane   |
| Identyfikator procesu | Identyfikator procesu systemu Windows |
| Parametr | Ścieżka i nazwa pliku hello procesu |
| RemoteIPLongitude | Wartości długości geograficznej IP |
| RemoteIPLatitude | Wartość szerokości geograficznej IP |


## <a name="next-steps"></a>Następne kroki

- [Wyszukaj dzienniki](log-analytics-log-searches.md) tooview szczegółowe podczas transmisji danych wyszukiwanie rekordów.
