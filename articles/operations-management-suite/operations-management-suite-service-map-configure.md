---
title: "Konfigurowanie usługi mapy w Operations Management Suite | Dokumentacja firmy Microsoft"
description: "Mapa usługi jest rozwiązania Operations Management Suite, który automatycznie odnajduje składniki aplikacji w systemach Windows i Linux oraz mapy komunikacji między usługami. Ten artykuł zawiera szczegółowe informacje dotyczące wdrażania mapy usługi w danym środowisku i korzystania z niego w różnych scenariuszach."
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
ms.openlocfilehash: e23173fb6708104c39071145595e4eec3454ee76
ms.sourcegitcommit: 1fbaa2ccda2fb826c74755d42a31835d9d30e05f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/22/2018
---
# <a name="configure-service-map-in-operations-management-suite"></a>Konfigurowanie usługi mapy w Operations Management Suite
Mapa usługi automatycznie odnajduje składniki aplikacji w systemach Windows i Linux oraz mapuje komunikację między usługami. Służy on do wyświetlania serwerów jako traktować ich — jako połączonych systemy, które dostarczają usług krytycznych. Mapy usług zawiera połączeń między serwerami, procesów i portów w dowolnej architekturze połączenia TCP z konfiguracja nie jest wymagane, innego niż instalacji agenta.

W tym artykule opisano konfigurowanie agentów mapy usługi i przechodzenia do szczegółów. Uzyskać przy użyciu mapy usługi, zobacz [programu rozwiązania mapy usługi Operations Management Suite](operations-management-suite-service-map.md).

## <a name="dependency-agent-downloads"></a>Zależności agenta pliki do pobrania
| Plik | System operacyjny | Wersja | SHA-256 |
|:--|:--|:--|:--|
| [InstallDependencyAgent-Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.3.0 | 1F5261CAAF6C8DF4E03E4927DA918B3461B40B41C6BF5845803878D7CF975693 |
| [InstallDependencyAgent-Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.3.0 | 7BADFF2411899114F0214766160E4E871A2462DC137141CEEDEFAF528F428ADD  |


## <a name="connected-sources"></a>Połączone źródła
Mapa usług dane są pobierane z Microsoft Dependency Agent. Agent zależności zależy od agenta pakietu OMS dla jego połączenia z pakietem Operations Management Suite. Oznacza to, że serwer musi mieć zainstalowany i skonfigurowany najpierw Agent pakietu OMS, a następnie może być zainstalowany Agent zależności. W poniższej tabeli opisano połączonych źródeł, które obsługuje rozwiązania mapy usługi.

| Połączone źródło | Obsługiwane | Opis |
|:--|:--|:--|
| Agenci dla systemu Windows | Yes | Mapa usług analizuje i zbiera dane z komputerów z systemem Windows agenta. <br><br>Oprócz [Agent pakietu OMS](../log-analytics/log-analytics-windows-agent.md), agentów systemu Windows wymagają Microsoft Dependency Agent. Zobacz [obsługiwanych systemów operacyjnych](#supported-operating-systems) pełną listę wersji systemu operacyjnego. |
| Agenci dla systemu Linux | Yes | Mapa usług analizuje i zbiera dane z komputerów z systemem Linux agenta. <br><br>Oprócz [Agent pakietu OMS](../log-analytics/log-analytics-linux-agents.md), Microsoft Dependency Agent wymagają agentów systemu Linux. Zobacz [obsługiwanych systemów operacyjnych](#supported-operating-systems) pełną listę wersji systemu operacyjnego. |
| Grupa zarządzania programu System Center Operations Manager | Yes | Mapa usług analizuje i zbiera dane z agentów systemu Windows i Linux w połączonych [grupy zarządzania programu System Center Operations Manager](../log-analytics/log-analytics-om-agents.md). <br><br>Bezpośrednie połączenie z komputera agenta programu System Center Operations Manager Operations Management Suite jest wymagana. Dane są przesyłane dalej z grupy zarządzania do repozytorium usługi Operations Management Suite.|
| Konto magazynu Azure | Nie | Mapy usługi zbiera dane z komputerami agenta, więc nie ma żadnych danych z niego do zbierania z usługi Azure Storage. |

Mapy usługi obsługuje tylko 64-bitowych platform.

W systemie Windows, Microsoft Monitoring Agent (MMA) jest używany zarówno przez System Center Operations Manager i Operations Management Suite do zbierania i wysyłania danych monitorowania. (Ten agent jest nazywane agenta programu System Center Operations Manager, Agent pakietu OMS, Agent analizy dziennika, MMA lub bezpośredniego agenta, w zależności od kontekstu.) System Center Operations Manager i Operations Management Suite zawiera pole poza z różnych wersji MMA. Te wersje strony każdy raport do programu System Center Operations Manager, Operations Management Suite lub obu.  

W systemie Linux, Agent pakietu OMS gromadzi systemu Linux i wysyła dane do usługi Operations Management Suite monitorowania. Na serwerach z agentami bezpośredniego OMS lub na serwerach, które są dołączone do usługi Operations Management Suite za pośrednictwem grup zarządzania programu System Center Operations Manager, możesz użyć mapy usługi.  

W tym artykule, firma Microsoft będzie odwoływać się do wszystkich agentów — czy Linux lub Windows, czy połączony z grupą zarządzania programu System Center Operations Manager lub bezpośrednio do usługi Operations Management Suite — jako "Agent pakietu OMS." Nazwa określonego wdrożenia agenta będą używane tylko wtedy, gdy jest wymagana dla kontekstu.

Agent mapy usług nie przesyła wszystkie dane, a nie wymaga zmian zapory lub porty. Agent pakietu OMS do usługi Operations Management Suite, przesyłania danych na mapie usługi zawsze, bezpośrednio lub za pośrednictwem bramy OMS.

![Agenci mapy usług](media/oms-service-map/agents.png)

Jeśli jesteś klientem programu System Center Operations Manager z grupą zarządzania podłączone do usługi Operations Management Suite:

- Jeśli agentów programu System Center Operations Manager można uzyskać dostępu do Internetu do nawiązania połączenia usługi Operations Management Suite, nie jest wymagana żadna konfiguracja dodatkowych.  
- Agentów programu System Center Operations Manager nie może uzyskać dostęp do usługi Operations Management Suite za pośrednictwem Internetu, należy skonfigurować bramę OMS do pracy z programem System Center Operations Manager.
  
Jeśli używasz bezpośredniej Agent pakietu OMS, należy skonfigurować agenta pakietu OMS do połączenia usługi Operations Management Suite lub bramy OMS. Brama OMS można pobrać z [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).

### <a name="management-packs"></a>Pakiety administracyjne
Po aktywowaniu mapy usługi z obszarem roboczym usługi Operations Management Suite pakietu administracyjnego 300 KB są wysyłane do wszystkich serwerów z systemem Windows w tym obszarze roboczym. Jeśli używasz programu System Center Operations Manager agentów w [podłączonej grupy zarządzania](../log-analytics/log-analytics-om-agents.md), mapy usługi pakietu administracyjnego wdrażania programu System Center Operations Manager. Jeżeli agenci są połączone bezpośrednio Operations Management Suite zapewnia pakietu administracyjnego.

Pakiet administracyjny nosi nazwę Microsoft.IntelligencePacks.ApplicationDependencyMonitor. Jest ona zapisywana w %Programfiles%\Microsoft Packs\ State\Management usługi Agent\Agent\Health monitorowanie. Źródło danych, które korzysta z pakietu administracyjnego jest % Program files%\Microsoft monitorowanie Agent\Agent\Health usługi State\Resources\<AutoGeneratedID > \Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="installation"></a>Instalacja
### <a name="install-the-dependency-agent-on-microsoft-windows"></a>Zainstaluj agenta zależności w systemie Microsoft Windows
Aby zainstalować lub odinstalować agenta wymagane są uprawnienia administratora.

Dependency Agent jest zainstalowany na komputerach z systemem Windows za pośrednictwem InstallDependencyAgent Windows.exe. Po uruchomieniu tego pliku wykonywalnego bez żadnych opcji uruchamia kreatora, który można wykonać w celu zainstalowania interaktywnie.  

Aby zainstalować agenta zależności na każdym komputerze z systemem Windows, wykonaj następujące kroki:

1.  Zainstaluj agenta pakietu OMS zgodnie z instrukcjami podanymi w [komputery Windows połączenia z usługą analizy dzienników na platformie Azure](../log-analytics/log-analytics-windows-agent.md).
2.  Pobierz agenta systemu Windows i uruchom go za pomocą następującego polecenia: <br>`InstallDependencyAgent-Windows.exe`
3.  Użyj kreatora, aby zainstalować agenta.
4.  Jeśli Dependency Agent nie powiedzie się, sprawdź dzienniki, aby uzyskać szczegółowe informacje o błędzie. Agentów systemu Windows katalog dziennika jest %Programfiles%\Microsoft Agent\logs zależności. 

#### <a name="windows-command-line"></a>Wiersz polecenia systemu Windows
Opcje z poniższej tabeli służą do instalacji z wiersza polecenia. Aby wyświetlić listę flagi instalacji, należy uruchomić Instalatora przy użyciu /? Flaga w następujący sposób.

    InstallDependencyAgent-Windows.exe /?

| Flaga | Opis |
|:--|:--|
| /? | Pobierz listę opcji wiersza polecenia. |
| /S | Wykonaj instalację dyskretną bez monitowania użytkownika. |

Pliki agenta zależności systemu Windows są umieszczane w C:\Program Files\Microsoft Dependency Agent domyślnie.

### <a name="install-the-dependency-agent-on-linux"></a>Zainstaluj agenta zależności w systemie Linux
Dostęp do konta root jest wymagane do zainstalowania i skonfigurowania agenta.

Dependency Agent jest zainstalowany na komputery z systemem Linux za pomocą Linux64.bin InstallDependencyAgent, skrypt powłoki z samowyodrębniający plikiem binarnym. Możesz uruchomić plik przy użyciu sh lub Dodaj uprawnienia w samym pliku do wykonywania.
 
Aby zainstalować agenta zależności na każdym komputerze z systemem Linux, wykonaj następujące kroki:

1.  Zainstaluj agenta pakietu OMS zgodnie z instrukcjami podanymi w [zbierania danych i zarządzać nimi z komputerów z systemem Linux](https://technet.microsoft.com/library/mt622052.aspx).
2.  Zainstaluj agenta systemu Linux zależności jako główny przy użyciu następującego polecenia:<br>`sh InstallDependencyAgent-Linux64.bin`
3.  Jeśli Dependency Agent nie powiedzie się, sprawdź dzienniki, aby uzyskać szczegółowe informacje o błędzie. W agencie Linux katalog dziennika jest /var/opt/microsoft/dependency-agent/log.

Aby wyświetlić listę flagi instalacji, uruchom instalację programu pomocy flagi w następujący sposób.

    InstallDependencyAgent-Linux64.bin -help

| Flaga | Opis |
|:--|:--|
| -help | Pobierz listę opcji wiersza polecenia. |
| -s | Wykonaj instalację dyskretną bez monitowania użytkownika. |
| — Sprawdź | Sprawdź uprawnienia i systemu operacyjnego, ale nie należy instalować agenta. |

Pliki programu Agent zależności są umieszczane w następujących katalogów:

| Pliki | Lokalizacja |
|:--|:--|
| Podstawowe pliki | /opt/microsoft/dependency-agent |
| Pliki dziennika | /var/OPT/Microsoft/Dependency-Agent/log |
| Pliki konfiguracji | /etc/opt/microsoft/dependency-agent/config |
| Pliki wykonywalne usługi | /opt/microsoft/dependency-agent/bin/microsoft-dependency-agent<br>/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager |
| Pliki binarne magazynu | /var/opt/microsoft/dependency-agent/storage |

## <a name="installation-script-examples"></a>Przykłady skryptów instalacji
Aby łatwo wdrożyć agenta zależności na wiele serwerów na raz, pomaga za pomocą skryptu. W poniższych przykładach skrypt umożliwia pobranie i zainstalowanie agenta zależności w systemu Windows lub Linux.

### <a name="powershell-script-for-windows"></a>Skrypt programu PowerShell dla systemu Windows
```PowerShell
Invoke-WebRequest "https://aka.ms/dependencyagentwindows" -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S
```

### <a name="shell-script-for-linux"></a>Skrypt powłoki dla systemu Linux
```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
sudo sh InstallDependencyAgent-Linux64.bin -s
```

## <a name="azure-vm-extension"></a>Rozszerzenia maszyny Wirtualnej platformy Azure
Możesz z łatwością wdrożyć agenta zależności przy użyciu maszyn wirtualnych platformy Azure [rozszerzenia maszyny Wirtualnej Azure](https://docs.microsoft.com/azure/virtual-machines/windows/extensions-features).  Rozszerzenie maszyny Wirtualnej Azure można wdrożyć agenta zależności maszyn wirtualnych za pomocą skryptu programu PowerShell lub bezpośrednio w szablonie usługi Azure Resource Manager maszyny Wirtualnej.  Rozszerzenie jest dostępna dla systemów Windows (DependencyAgentWindows), jak i Linux (DependencyAgentLinux).  W przypadku wdrożenia za pośrednictwem rozszerzenia maszyny Wirtualnej Azure, agentów może automatycznie zaktualizowana do najnowszej wersji.

Aby wdrożyć rozszerzenie maszyny Wirtualnej Azure za pomocą programu PowerShell, można skorzystaj z następującego przykładu:
```PowerShell
#
# Deploy the Dependency Agent to every VM in a Resource Group
#

$version = "9.1"
$ExtPublisher = "Microsoft.Azure.Monitoring.DependencyAgent"
$OsExtensionMap = @{ "Windows" = "DependencyAgentWindows"; "Linux" = "DependencyAgentLinux" }
$rmgroup = "<Your Resource Group Here>"

Get-AzureRmVM -ResourceGroupName $rmgroup |
ForEach-Object {
    ""
    $name = $_.Name
    $os = $_.StorageProfile.OsDisk.OsType
    $location = $_.Location
    $vmRmGroup = $_.ResourceGroupName
    "${name}: ${os} (${location})"
    Date -Format o
    $ext = $OsExtensionMap.($os.ToString())
    $result = Set-AzureRmVMExtension -ResourceGroupName $vmRmGroup -VMName $name -Location $location `
    -Publisher $ExtPublisher -ExtensionType $ext -Name "DependencyAgent" -TypeHandlerVersion $version
    $result.IsSuccessStatusCode
}
```

Łatwiejsze sposobem zapewnienia Dependency Agent znajduje się na poszczególnych maszyn wirtualnych ma zawierać agenta do szablonu usługi Azure Resource Manager.  Należy pamiętać, że Dependency Agent nadal zależy od agenta pakietu OMS, więc [rozszerzenia maszyny Wirtualnej agenta pakietu OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-vm-extension) należy najpierw wdrożyć.  Poniższy fragment JSON można dodać do *zasobów* części szablonu.
```JSON
"type": "Microsoft.Compute/virtualMachines/extensions",
"name": "[concat(parameters('vmName'), '/DependencyAgent')]",
"apiVersion": "2017-03-30",
"location": "[resourceGroup().location]",
"dependsOn": [
"[concat('Microsoft.Compute/virtualMachines/', parameters('vmName'))]"
],
"properties": {
    "publisher": "Microsoft.Azure.Monitoring.DependencyAgent",
    "type": "DependencyAgentWindows",
    "typeHandlerVersion": "9.1",
    "autoUpgradeMinorVersion": true
}

```


## <a name="desired-state-configuration"></a>Konfiguracja żądanego stanu
Aby wdrożyć Dependency Agent za pomocą konfiguracji żądanego stanu, można użyć modułu xPSDesiredStateConfiguration i kodu podobne do poniższych:
```
configuration ServiceMap {

Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = "C:\InstallDependencyAgent-Windows.exe"

Node localhost
{ 
    # Download and install the Dependency Agent
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
### <a name="uninstall-the-dependency-agent-on-windows"></a>Odinstaluj agenta zależności w systemie Windows
Administrator może odinstalować zależności agenta dla systemu Windows za pomocą Panelu sterowania.

Administrator można również uruchomić %Programfiles%\Microsoft Agent\Uninstall.exe zależności można odinstalować agenta zależności.

### <a name="uninstall-the-dependency-agent-on-linux"></a>Odinstaluj agenta zależności w systemie Linux
Zależności agenta można odinstalować z systemem Linux przy użyciu następującego polecenia.
<br>RHEL, CentOs lub Oracle:
```
sudo rpm -e dependency-agent
```
Ubuntu:
```
sudo dpkg --purge dependency-agent
```
## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli masz problemy z Instalowanie i uruchamianie mapy usług w tej sekcji mogą pomóc. Jeśli nadal nie możesz rozwiązać problemu, skontaktuj się z Microsoft Support.

### <a name="dependency-agent-installation-problems"></a>Problemy z instalacją agenta zależności
#### <a name="installer-asks-for-a-reboot"></a>Instalator pyta o ponowne uruchomienie komputera
Zależności agenta *zazwyczaj* nie wymaga ponownego uruchomienia komputera po instalacji i dezinstalacji. Jednak w niektórych rzadkich przypadkach, Windows Server wymaga ponownego uruchomienia, aby kontynuować instalację. Dzieje się tak, gdy zależności, zwykle Microsoft Visual C++ Redistributable, wymaga ponownego uruchomienia ze względu na zablokowany plik.

#### <a name="message-unable-to-install-dependency-agent-visual-studio-runtime-libraries-failed-to-install-code--codenumber-appears"></a>Komunikat "nie można zainstalować agenta zależności: bibliotek środowiska uruchomieniowego Visual Studio nie może zainstalować (kod = [Numer_kodu])" pojawia się

Program Microsoft Dependency Agent jest oparty na bibliotek środowiska uruchomieniowego programu Microsoft Visual Studio. Zostanie wyświetlony komunikat, jeśli występuje problem podczas instalacji bibliotek. 

Instalatorzy biblioteki środowiska uruchomieniowego Utwórz dzienniki w folderze %LOCALAPPDATA%\temp. Plik jest dd_vcredist_arch_yyyymmddhhmmss.log, gdzie *arch* "x86" lub "amd64" i *rrrrmmddggmmss* jest data i godzina (24-godzinnym) podczas tworzenia dziennika. Dziennik zawiera szczegółowe informacje o problemie, który blokuje instalację.

Może być przydatne do zainstalowania [najnowsze bibliotek środowiska uruchomieniowego](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) samodzielnie pierwszy.

W poniższej tabeli wymieniono kody i sugerowanymi metodami rozwiązania.

| Kod | Opis | Rozwiązanie |
|:--|:--|:--|
| 0x17 | Biblioteka Instalator wymaga aktualizacji systemu Windows, który nie został zainstalowany. | Poszukaj w dzienniku ostatniego Instalator biblioteki.<br><br>Jeśli występuje odwołanie do "Windows8.1-KB2999226-x64.msu" wiersza "Błąd 0x80240017: nie można wykonać pakietu MSU" nie ma wymagań wstępnych instalacji KB2999226. Postępuj zgodnie z instrukcjami w sekcji wymagania wstępne [uniwersalnego C środowiska uruchomieniowego w systemie Windows](https://support.microsoft.com/kb/2999226). Może być konieczne, uruchom usługę Windows Update, a następnie ponownie uruchom wiele razy, aby można było zainstalować wymagania wstępne.<br><br>Ponownie uruchom Instalatora programu Microsoft Dependency Agent. |

### <a name="post-installation-issues"></a>Problemy po instalacji
#### <a name="server-doesnt-appear-in-service-map"></a>Serwer nie ma mapy usług
Jeśli instalacji agenta zależności zakończyło się pomyślnie, ale nie widzisz serwera w rozwiązaniu mapy usługi:
* Dependency Agent jest zainstalowany pomyślnie? Możesz to sprawdzić przez sprawdzanie, czy usługa jest zainstalowana i uruchomiona.<br><br>
**Windows**: Wyszukaj usługi o nazwie "Microsoft Dependency Agent."<br>
**Linux**: Wyszukaj uruchomione przetworzyć "microsoft zależności agenta."

* Czy na [wolnego cenowym Operations Management Suite/Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)? Umożliwia planu Free do pięciu unikatowych serwerów mapy usługi. Kolejne serwery będą serwerami nie będą wyświetlane w mapy usług, nawet jeśli poprzednie pięć już wysyłania danych.

* Jest danych wysyłania dziennika serwera i wydajności usługi Operations Management Suite? Przejdź do wyszukiwania dziennika i uruchom następujące zapytanie dla danego komputera: 

        * Computer="<your computer name here>" | measure count() by Type
        
  Czy został wyświetlony w wynikach różnych zdarzeń? To jest ostatnie dane? Jeśli tak, agenta pakietu OMS jest prawidłowego działania i komunikacji z usługą Operations Management Suite. Jeśli nie, sprawdź, czy Agent pakietu OMS na serwerze: [Rozwiązywanie problemów z usługą OMS agenta dla systemu Windows](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues) lub [Agent pakietu OMS dla systemu Linux Rozwiązywanie problemów z](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md).

#### <a name="server-appears-in-service-map-but-has-no-processes"></a>Serwer jest wyświetlany w mapy usług, ale ma żadne procesy
Jeśli zostanie wyświetlony w mapie usługi serwera, ale go nie ma procesu lub połączenia danych, który wskazuje Dependency Agent jest zainstalowany i działa, że sterownik jądra nie został załadowany. 

Sprawdź plik C:\Program Files\Microsoft zależności Agent\logs\wrapper.log (system Windows) lub plik /var/opt/microsoft/dependency-agent/log/service.log (Linux). Ostatnich wierszy w pliku powinny wskazywać, dlaczego jądra nie został załadowany. Na przykład jądra może nie być obsługiwany w systemie Linux, jeśli zaktualizowane z jądra.

## <a name="data-collection"></a>Zbieranie danych
Można oczekiwać, że każdy agent ma zostać przesłany około 25 MB na dzień, w zależności od sposobu złożonych zależności systemu. Każdy agent wysyła dane zależności mapy usług co 15 s.  

Zależności agenta zwykle zużywa 0,1 procent pamięci systemowej i procent 0,1 systemu Procesora.

## <a name="supported-azure-regions"></a>Obsługiwane regiony platformy Azure
Mapa usługi jest obecnie dostępna w następujących regionach platformy Azure:
- Wschodnie stany USA
- Europa Zachodnia
- Środkowo-zachodnie stany USA
- Azja Południowo-Wschodnia


## <a name="supported-operating-systems"></a>Obsługiwane systemy operacyjne
Poniższe sekcje zawierają listę obsługiwanych systemów operacyjnych dla agenta zależności. Mapy usług nie obsługuje architektury 32-bitowego dla dowolnego systemu operacyjnego.

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
- Zwalnia jądra niestandardowe, takie jak rozszerzenia adresu fizycznego i Xen, nie są obsługiwane dla dowolnego dystrybucji systemu Linux. Na przykład system z wersji ciąg "2.6.16.21-0.8-xen" nie jest obsługiwane.
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
| 7.4 | 3.10.0-693 |

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
| 6.9 | 2.6.32-696 |

#### <a name="red-hat-linux-5"></a>Red Hat Linux 5
| Wersja systemu operacyjnego | Wersja jądra |
|:--|:--|
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398<br>2.6.18-400<br>2.6.18-402<br>2.6.18-404<br>2.6.18-406<br>2.6.18-407<br>2.6.18-408<br>2.6.18-409<br>2.6.18-410<br>2.6.18-411<br>2.6.18-412<br>2.6.18-416<br>2.6.18-417<br>2.6.18-419<br>2.6.18-420 |

### <a name="ubuntu-server"></a>Ubuntu Server
- Niestandardowe jądra, w tym ponownych kompilacji standardowe jądra, nie są obsługiwane.

| Wersja systemu operacyjnego | Wersja jądra |
|:--|:--|
| 16.04 | 4.4.0-103<br>4.11.0-1016 |
| 14.04 | 3.13.0-137<br>4.4.0-103 |

### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Linux przedsiębiorstwa z jądra podzielenie Enterprise
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
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11
| Wersja systemu operacyjnego | Wersja jądra
|:--|:--|
| 11 SP2 | 3.0.101-0.7 |
| 11 SP3 | 3.0.101-0.47 |
| 11 SP4 | 3.0.101-65 |


## <a name="diagnostic-and-usage-data"></a>dane diagnostyczne i użycia
Firma Microsoft automatycznie zbiera dane użycia i wydajności przez korzystanie z usługi mapy usługi. Firma Microsoft używa tych danych do udostępniania i ulepszania jakości, bezpieczeństwa i integralności usługi mapy usługi. Dane obejmują informacje o konfiguracji oprogramowania, takie jak wersja systemu operacyjnego i. Zawiera także adres IP, nazwę DNS i nazwę stacji roboczej zapewnić dokładne i skuteczne funkcje do rozwiązywania problemów. Nie gromadzimy nazwisk, adresów ani innych informacji kontaktowych.

Aby uzyskać więcej informacji dotyczących zbierania i użycia danych, zobacz [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=512132).



## <a name="next-steps"></a>Kolejne kroki
- Dowiedz się, jak [użyć mapy usługi](operations-management-suite-service-map.md) po zostały wdrożone i skonfigurowane.
