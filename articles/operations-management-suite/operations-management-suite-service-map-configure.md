---
title: "aaaConfigure mapy usługi w Operations Management Suite | Dokumentacja firmy Microsoft"
description: "Mapa usługi jest rozwiązaniem Operations Management Suite, który automatycznie odnajduje składniki aplikacji w systemie Windows i systemów Linux i map hello komunikacji między usługami. Ten artykuł zawiera szczegółowe informacje dotyczące wdrażania mapy usługi w danym środowisku i korzystania z niego w różnych scenariuszach."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: d3d66b45-9874-4aad-9c00-124734944b2e
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/18/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: 3127f4440f2886370f8ff617c405c6d70a926eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-service-map-in-operations-management-suite"></a>Konfigurowanie usługi mapy w Operations Management Suite
Mapy usług automatycznie odnajduje składniki aplikacji w systemach Windows i Linux oraz mapy hello komunikacji między usługami. Służy on tooview serwerów podczas Pomyśl o nich — jako połączonych systemy, które dostarczają usług krytycznych. Mapy usług zawiera połączeń między serwerami, procesów i portów w dowolnej architekturze połączenia TCP z konfiguracja nie jest wymagane, innego niż instalacji agenta.

W tym artykule opisano konfigurowanie agentów mapy usługi i dołączania szczegóły hello. Uzyskać przy użyciu mapy usługi, zobacz [programu hello rozwiązania mapy usługi Operations Management Suite](operations-management-suite-service-map.md).

## <a name="dependency-agent-downloads"></a>Zależności agenta pliki do pobrania
| Plik | System operacyjny | Wersja | ALGORYTM SHA-256 |
|:--|:--|:--|:--|
| [InstallDependencyAgent Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |


## <a name="connected-sources"></a>Połączone źródła
Mapa usług dane są pobierane z hello Microsoft Dependency Agent. Hello Dependency Agent jest zależna od hello Agent pakietu OMS dla jego tooOperations połączeń Management Suite. Oznacza to, że serwer musi mieć hello Agent pakietu OMS zainstalowany i skonfigurowany pierwszy i hello Dependency Agent można ją zainstalować. Witaj poniższej tabeli opisano źródeł hello połączone, które obsługuje hello rozwiązania mapy usługi.

| Źródło połączenia | Obsługiwane | Opis |
|:--|:--|:--|
| Agenci dla systemu Windows | Tak | Mapa usług analizuje i zbiera dane z komputerów z systemem Windows agenta. <br><br>W przypadku dodawania toohello [Agent pakietu OMS](../log-analytics/log-analytics-windows-agents.md), agentów systemu Windows wymagają hello Microsoft Dependency Agent. Zobacz hello [obsługiwanych systemów operacyjnych](#supported-operating-systems) pełną listę wersji systemu operacyjnego. |
| Agenci dla systemu Linux | Tak | Mapa usług analizuje i zbiera dane z komputerów z systemem Linux agenta. <br><br>W przypadku dodawania toohello [Agent pakietu OMS](../log-analytics/log-analytics-linux-agents.md), hello Microsoft Dependency Agent wymagają agentów systemu Linux. Zobacz hello [obsługiwanych systemów operacyjnych](#supported-operating-systems) pełną listę wersji systemu operacyjnego. |
| Grupa zarządzania programu System Center Operations Manager | Tak | Mapa usług analizuje i zbiera dane z agentów systemu Windows i Linux w połączonych [grupy zarządzania programu System Center Operations Manager](../log-analytics/log-analytics-om-agents.md). <br><br>Połączenie bezpośrednie z tooOperations komputera agenta programu System Center Operations Manager hello pakiet zarządzania jest wymagana. Dane są przesyłane z hello zarządzania grupy toohello Operations Management Suite repozytorium.|
| Konto magazynu Azure | Nie | Mapy usług zbiera dane z komputery agenta, więc nie ma żadnych danych z niego toocollect z usługi Magazyn Azure. |

Mapy usługi obsługuje tylko 64-bitowych platform.

W systemie Windows hello Microsoft Monitoring Agent (MMA) jest używany zarówno przez System Center Operations Manager i Operations Management Suite toogather i wysyłania danych monitorowania. (Ten agent jest nazywany hello agenta programu System Center Operations Manager, Agent pakietu OMS, Agent analizy dziennika, MMA lub bezpośredniego agenta, w zależności od kontekstu hello). System Center Operations Manager i Operations Management Suite zawiera wersji różnych pola typu "out powitania" hello MMA. Te wersje strony każdy raport tooSystem Center Operations Manager, tooOperations Management Suite lub tooboth.  

W systemie Linux hello Agent pakietu OMS dla systemu Linux gromadzi i wysyła monitorowania danych tooOperations Management Suite. Na serwerach z agentami bezpośredniego OMS lub na serwerach, które są dołączone tooOperations Management Suite za pośrednictwem grup zarządzania programu System Center Operations Manager, możesz użyć mapy usługi.  

W tym artykule, firma Microsoft będzie odwoływać się agentów tooall — czy Linux lub Windows, czy podłączone grupy zarządzania programu System Center Operations Manager tooa lub bezpośrednio tooOperations Management Suite — jak Witaj "Agent pakietu OMS." Użyjemy hello nazwę określonego wdrożenia agenta hello tylko wtedy, gdy jest wymagana dla kontekstu.

Hello mapy usługi agenta nie przesyła wszystkie dane, a nie wymaga żadnych zmian toofirewalls lub porty. Witaj tooOperations Agent pakietu OMS Management Suite przesyłania danych Hello mapy usługi zawsze, bezpośrednio lub za pośrednictwem hello OMS bramy.

![Agenci mapy usług](media/oms-service-map/agents.png)

Jeśli jesteś klientem programu System Center Operations Manager z tooOperations podłączone grupy zarządzania Management Suite:

- Jeśli agentów programu System Center Operations Manager można uzyskać dostęp do hello Internet tooconnect tooOperations Management Suite, nie jest wymagana żadna konfiguracja dodatkowych.  
- Agentów programu System Center Operations Manager nie może uzyskać dostęp do Operations Management Suite za pośrednictwem hello Internet, należy najpierw tooconfigure hello bramy OMS toowork z programem System Center Operations Manager.
  
Jeśli używasz hello bezpośredniego Agent pakietu OMS wymagany hello tooconfigure sam Agent pakietu OMS tooOperations tooconnect Management Suite lub tooyour OMS bramy. Witaj OMS bramy można pobrać z hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).

### <a name="management-packs"></a>Pakiety administracyjne
Po aktywowaniu mapy usługi z obszarem roboczym usługi Operations Management Suite pakietu administracyjnego 300 KB są wysyłane tooall serwerów z systemem Windows hello w tym obszarze roboczym. Jeśli używasz programu System Center Operations Manager agentów w [podłączonej grupy zarządzania](../log-analytics/log-analytics-om-agents.md), wdrożeniu hello mapy usługi pakietu administracyjnego programu System Center Operations Manager. Jeśli agenci hello są połączone bezpośrednio Operations Management Suite zapewnia hello pakietu administracyjnego.

Pakiet administracyjny Hello nosi nazwę Microsoft.IntelligencePacks.ApplicationDependencyMonitor. Jego napisane too%Programfiles%\Microsoft Packs\ State\Management usługi Agent\Agent\Health monitorowanie. Witaj źródła danych, które korzysta z pakietu administracyjnego hello jest % Program files%\Microsoft monitorowanie Agent\Agent\Health usługi State\Resources\<AutoGeneratedID > \ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="installation"></a>Instalacja
### <a name="install-hello-dependency-agent-on-microsoft-windows"></a>Zainstaluj hello Dependency Agent Microsoft Windows
Uprawnienia administratora są wymagane tooinstall lub odinstaluj agenta hello.

Hello Dependency Agent jest zainstalowany na komputerach z systemem Windows za pośrednictwem InstallDependencyAgent Windows.exe. Po uruchomieniu tego pliku wykonywalnego bez żadnych opcji uruchamia kreatora, że możesz wykonać tooinstall interaktywnie.  

Użyj następujących kroków tooinstall hello Dependency Agent na każdym komputerze z systemem Windows hello:

1.  Zainstaluj hello Agent pakietu OMS za pomocą instrukcji hello na [toohello komputerów Windows połączenia usługi Analiza dzienników w usłudze Azure](../log-analytics/log-analytics-windows-agents.md).
2.  Pobierz agenta systemu Windows hello i uruchomić go za pomocą hello następujące polecenie: <br>`InstallDependencyAgent-Windows.exe`
3.  Wykonaj hello kreatora tooinstall hello agenta.
4.  W przypadku niepowodzenia toostart hello Dependency Agent Sprawdź hello dzienniki, aby uzyskać szczegółowe informacje o błędzie. Na agentów systemu Windows hello katalog dziennika jest %Programfiles%\Microsoft Agent\logs zależności. 

#### <a name="windows-command-line"></a>Wiersz polecenia systemu Windows
Za pomocą opcji z powitania po tooinstall tabeli z wiersza polecenia. toosee listę flagi instalacji hello, uruchom Instalatora hello przy użyciu hello /? Flaga w następujący sposób.

    InstallDependencyAgent-Windows.exe /?

| Flaga | Opis |
|:--|:--|
| /? | Pobierz listę hello opcje wiersza polecenia. |
| / S | Wykonaj instalację dyskretną bez monitowania użytkownika. |

Pliki dla agenta zależności Windows hello są umieszczane w C:\Program Files\Microsoft Dependency Agent domyślnie.

### <a name="install-hello-dependency-agent-on-linux"></a>Zainstaluj hello Dependency Agent w systemie Linux
Dostęp do konta root jest wymagane tooinstall lub skonfigurować hello agenta.

Witaj Dependency Agent jest zainstalowany na komputery z systemem Linux za pomocą Linux64.bin InstallDependencyAgent, skrypt powłoki z samowyodrębniający plikiem binarnym. Możesz uruchomić plik hello przy użyciu sh lub dodać sam plik toohello uprawnienia do wykonania.
 
Użyj hello następujące kroki tooinstall hello Dependency Agent na każdym komputerze z systemem Linux:

1.  Zainstaluj hello Agent pakietu OMS za pomocą instrukcji hello na [zbierania danych i zarządzać nimi z komputerów z systemem Linux](https://technet.microsoft.com/library/mt622052.aspx).
2.  Zainstaluj agenta systemu Linux zależności hello jako główny przy użyciu następującego polecenia hello:<br>`sh InstallDependencyAgent-Linux64.bin`
3.  W przypadku niepowodzenia toostart hello Dependency Agent Sprawdź hello dzienniki, aby uzyskać szczegółowe informacje o błędzie. W agencie Linux hello katalog dziennika jest /var/opt/microsoft/dependency-agent/log.

toosee listę flagi instalacji hello, uruchom program instalacyjny hello z hello - flagi pomocy w następujący sposób.

    InstallDependencyAgent-Linux64.bin -help

| Flaga | Opis |
|:--|:--|
| -Pomoc | Pobierz listę hello opcje wiersza polecenia. |
| -s | Wykonaj instalację dyskretną bez monitowania użytkownika. |
| — Sprawdź | Sprawdź uprawnienia i hello systemu operacyjnego, ale nie należy instalować hello agenta. |

Pliki hello Dependency Agent są umieszczane w hello następujące katalogi:

| Pliki | Lokalizacja |
|:--|:--|
| Podstawowe pliki | /OPT/Microsoft/Dependency-Agent |
| Pliki dziennika | /var/OPT/Microsoft/Dependency-Agent/log |
| Pliki konfiguracji | /etc/OPT/Microsoft/Dependency-Agent/config |
| Pliki wykonywalne usługi | /OPT/Microsoft/Dependency-Agent/bin/Microsoft-Dependency-Agent<br>/OPT/Microsoft/Dependency-Agent/bin/Microsoft-Dependency-Agent-Manager |
| Pliki binarne magazynu | /var/OPT/Microsoft/Dependency-Agent/Storage |

## <a name="installation-script-examples"></a>Przykłady skryptów instalacji
tooeasily wdrażanie hello Dependency Agent na wiele serwerów na raz, ale toouse skryptu. Można użyć następującego skryptu przykłady toodownload hello i zainstalować hello Dependency Agent w systemie Windows lub Linux.

### <a name="powershell-script-for-windows"></a>Skrypt programu PowerShell dla systemu Windows
```PowerShell
Invoke-WebRequest "https://aka.ms/dependencyagentwindows" -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S
```

### <a name="shell-script-for-linux"></a>Skrypt powłoki dla systemu Linux
```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
sh InstallDependencyAgent-Linux64.bin -s
```

## <a name="desired-state-configuration"></a>Konfiguracja żądanego stanu
Witaj toodeploy Dependency Agent za pomocą konfiguracji żądanego stanu można użyć modułu xPSDesiredStateConfiguration hello i kod, takie jak następujące hello:
```
configuration ServiceMap {

Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = "C:\InstallDependencyAgent-Windows.exe"

Node localhost
{ 
    # Download and install hello Dependency Agent
    xRemoteFile DAPackage 
    {
        Uri = "https://aka.ms/dependencyagentwindows"
        DestinationPath = $DAPackageLocalPath
    }

    xPackage DA
    {
        Ensure="Present"
        Name = "Dependency Agent"
        Path = $DAPackageLocalPath
        Arguments = '/S'
        ProductId = ""
        InstalledCheckRegKey = "HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent"
        InstalledCheckRegValueName = "DisplayName"
        InstalledCheckRegValueData = "Dependency Agent"
        DependsOn = "[xRemoteFile]DAPackage"
    }
  }
}
```

## <a name="uninstallation"></a>Dezinstalacja
### <a name="uninstall-hello-dependency-agent-on-windows"></a>Odinstaluj hello Dependency Agent w systemie Windows
Administrator może odinstalować hello zależności agenta dla systemu Windows za pomocą Panelu sterowania.

Administrator można również uruchomić %Programfiles%\Microsoft Agent\Uninstall.exe zależności toouninstall hello Dependency Agent.

### <a name="uninstall-hello-dependency-agent-on-linux"></a>Odinstaluj hello Dependency Agent w systemie Linux
Odinstaluj toocompletely hello Dependency Agent z systemem Linux, należy usunąć samego agenta hello i hello łącznik, który jest automatycznie instalowany z hello agenta. Można je odinstalować, zarówno przy użyciu hello następującego polecenia:

    rpm -e dependency-agent dependency-agent-connector

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli masz problemy z Instalowanie i uruchamianie mapy usług w tej sekcji mogą pomóc. Jeśli nadal nie możesz rozwiązać problemu, skontaktuj się z Microsoft Support.

### <a name="dependency-agent-installation-problems"></a>Problemy z instalacją agenta zależności
#### <a name="installer-asks-for-a-reboot"></a>Instalator pyta o ponowne uruchomienie komputera
Witaj Dependency Agent *zazwyczaj* nie wymaga ponownego uruchomienia komputera po instalacji i dezinstalacji. Jednak w niektórych rzadkich przypadkach systemu Windows Server wymaga toocontinue ponowne uruchomienie instalacji. Dzieje się tak, gdy zależności, zwykle hello Microsoft Visual C++ Redistributable, wymaga ponownego uruchomienia ze względu na zablokowany plik.

#### <a name="message-unable-tooinstall-dependency-agent-visual-studio-runtime-libraries-failed-tooinstall-code--codenumber-appears"></a>Komunikat "tooinstall Dependency Agent: bibliotek środowiska uruchomieniowego Visual Studio tooinstall nie powiodło się (kod = [Numer_kodu])" pojawia się

Witaj Microsoft Dependency Agent jest oparty na bibliotek środowiska uruchomieniowego programu Microsoft Visual Studio hello. Zostanie wyświetlony komunikat, jeśli występuje problem podczas instalacji hello bibliotek. 

Instalatorzy biblioteki środowiska uruchomieniowego Hello Utwórz dzienniki w folderze %LOCALAPPDATA%\temp hello. Plik Hello jest dd_vcredist_arch_yyyymmddhhmmss.log, gdzie *arch* "x86" lub "amd64" i *rrrrmmddggmmss* jest hello Data i godzina (24-godzinnym) podczas tworzenia dziennika hello. Dziennik Hello szczegółowe informacje na temat problemu hello, która blokuje instalację.

Może być przydatne tooinstall hello [najnowsze bibliotek środowiska uruchomieniowego](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) samodzielnie pierwszy.

Witaj poniższej tabeli przedstawiono kody i sugerowanymi metodami rozwiązania.

| Kod | Opis | Rozwiązanie |
|:--|:--|:--|
| 0x17 | Witaj biblioteki Instalator wymaga aktualizacji systemu Windows, który nie został zainstalowany. | Szukaj w hello najnowsze biblioteki dziennika Instalatora.<br><br>Jeśli odwołanie za "Windows8.1-KB2999226-x64.msu" następuje wiersza "Błąd 0x80240017: Pakiet MSU tooexecute nie powiodło się," nie ma hello wymagania wstępne tooinstall KB2999226. Wykonaj instrukcje hello w sekcji wymagania wstępne hello [uniwersalnego C środowiska uruchomieniowego w systemie Windows](https://support.microsoft.com/kb/2999226). Może muszą toorun usługi Windows Update, a następnie ponownie wiele razy w kolejności tooinstall hello — wymagania wstępne.<br><br>Ponownie uruchom Instalatora Microsoft Dependency Agent hello. |

### <a name="post-installation-issues"></a>Problemy po instalacji
#### <a name="server-doesnt-appear-in-service-map"></a>Serwer nie ma mapy usług
Jeśli instalacji agenta zależności zakończyło się pomyślnie, ale nie widać na serwerze w ramach hello rozwiązania mapy usługi:
* Witaj Dependency Agent jest zainstalowany pomyślnie? Możesz to sprawdzić sprawdzanie toosee, jeśli usługa hello jest zainstalowana i uruchomiona.<br><br>
**Windows**: Wyszukaj hello usługi o nazwie "Microsoft Dependency Agent."<br>
**Linux**: Wyszukaj hello uruchomienie procesu "microsoft zależności agenta."

* Czy na powitania [wolnego cenowym Operations Management Suite/Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)? planu Free hello umożliwia toofive unikatowe serwery mapy usługi. Kolejne serwery będą serwerami nie będą wyświetlane w mapy usług, nawet jeśli hello wcześniejszych pięciu już wysyłania danych.

* Jest serwer wysyłania dziennika, a tooOperations danych wydajności Management Suite? Przejdź tooLog wyszukiwania, a następnie uruchom hello następujące zapytanie dla danego komputera: 

        * Computer="<your computer name here>" | measure count() by Type
        
  Czy został wyświetlony w wynikach hello różnych zdarzeń? Czy dane hello ostatnie? Jeśli tak, agenta pakietu OMS jest prawidłowego działania i komunikacji z usługą Operations Management Suite hello. Jeśli nie, sprawdź hello Agent pakietu OMS na serwerze: [Rozwiązywanie problemów z usługą OMS agenta dla systemu Windows](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues) lub [Agent pakietu OMS dla systemu Linux Rozwiązywanie problemów z](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md).

#### <a name="server-appears-in-service-map-but-has-no-processes"></a>Serwer jest wyświetlany w mapy usług, ale ma żadne procesy
Jeśli widzisz serwera w mapie usługi, ale go nie ma procesu lub połączenia danych, która wskazuje, że hello Dependency Agent jest zainstalowany i działa, ale sterownik jądra hello nie został załadowany. 

Sprawdź plik C:\Program Files\Microsoft zależności Agent\logs\wrapper.log hello (system Windows) lub plik /var/opt/microsoft/dependency-agent/log/service.log (Linux). ostatni wiersze pliku hello Hello powinny wskazywać, dlaczego hello jądra nie został załadowany. Na przykład jądra hello może nie być obsługiwany w systemie Linux, jeśli zaktualizowane z jądra.

## <a name="data-collection"></a>Zbieranie danych
Można oczekiwać, że każdy agent tootransmit około 25 MB na dzień, w zależności od sposobu złożonych zależności systemu. Każdy agent wysyła dane zależności mapy usług co 15 s.  

Witaj Dependency Agent zwykle zużywa 0,1% pamięci systemowej i 0,1 procent Procesora systemu.

## <a name="supported-azure-regions"></a>Obsługiwane regiony platformy Azure
Mapa usługi jest obecnie dostępna w hello następujące regiony platformy Azure:
- Wschodnie stany USA
- Europa Zachodnia
- Środkowo-zachodnie stany USA


## <a name="supported-operating-systems"></a>Obsługiwane systemy operacyjne
Witaj poniższe sekcje zawierają listę hello obsługiwane systemy operacyjne dla hello Dependency Agent. Mapy usług nie obsługuje architektury 32-bitowego dla dowolnego systemu operacyjnego.

### <a name="windows-server"></a>Windows Server
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1

### <a name="windows-desktop"></a>Pulpit systemu Windows
- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux, CentOS Linux i Oracle Linux (z RHEL jądra)
- Obsługiwane są tylko domyślnej i wersjach jądra systemu Linux SMP.
- Zwalnia jądra niestandardowe, takie jak rozszerzenia adresu fizycznego i Xen, nie są obsługiwane dla dowolnego dystrybucji systemu Linux. Na przykład system z wersji ciąg hello "2.6.16.21-0.8-xen" nie jest obsługiwana.
- Niestandardowe jądra, w tym ponownych kompilacji standardowe jądra, nie są obsługiwane.
- CentOSPlus jądra nie jest obsługiwane.
- Oracle podzielenie Enterprise jądra (UEK) zostało opisane w dalszej części tego artykułu.


#### <a name="red-hat-linux-7"></a>Red Hat Linux 7
| Wersja systemu operacyjnego | Wersja jądra |
|:--|:--|
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7.2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6
| Wersja systemu operacyjnego | Wersja jądra |
|:--|:--|
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
| Wersja systemu operacyjnego | Wersja jądra |
|:--|:--|
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398<br>2.6.18-400<br>2.6.18-402<br>2.6.18-404<br>2.6.18-406<br>2.6.18-407<br>2.6.18-408<br>2.6.18-409<br>2.6.18-410<br>2.6.18-411<br>2.6.18-412<br>2.6.18-416<br>2.6.18-417<br>2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Linux przedsiębiorstwa z jądra podzielenie Enterprise

#### <a name="oracle-linux-6"></a>Oracle Linux 6
| Wersja systemu operacyjnego | Wersja jądra
|:--|:--|
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4 | Oracle 2.6.39-400 (UEK R2) |
| 6.5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| Wersja systemu operacyjnego | Wersja jądra
|:--|:--|
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11
| Wersja systemu operacyjnego | Wersja jądra
|:--|:--|
| 11 | 2.6.27 |
| 11 Z DODATKIEM SP1 | 2.6.32 |
| 11 Z DODATKIEM SP2 | 3.0.13 |
| 11 Z DODATKIEM SP3 | 3.0.76 |
| 11 Z DODATKIEM SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10
| Wersja systemu operacyjnego | Wersja jądra
|:--|:--|
| Z DODATKIEM SP4 10 | 2.6.16.60 |

## <a name="diagnostic-and-usage-data"></a>dane diagnostyczne i użycia
Firma Microsoft automatycznie zbiera dane użycia i wydajności przez korzystanie z hello usługi mapy usługi. Firma Microsoft używa tego tooprovide danych i poprawy hello jakości, bezpieczeństwa i integralności hello usługi mapy usługi. Dane obejmują informacje o konfiguracji oprogramowania, takie jak wersja systemu operacyjnego i hello. Zawiera także adres IP, nazwę DNS i nazwę stacji roboczej w kolejności tooprovide dokładne i skuteczne funkcje do rozwiązywania problemów. Nie gromadzimy nazwisk, adresów ani innych informacji kontaktowych.

Aby uzyskać więcej informacji dotyczących zbierania i użycia danych, zobacz hello [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=512132).



## <a name="next-steps"></a>Następne kroki
- Dowiedz się, jak za[użyć mapy usługi](operations-management-suite-service-map.md) po zostały wdrożone i skonfigurowane.
