---
title: "urządzenie StorSimple 8000 tootroubleshoot narzędzie aaaDiagnostics | Dokumentacja firmy Microsoft"
description: "Zawiera opis tryby urządzenia StorSimple hello i jak toouse środowiska Windows PowerShell dla StorSimple toochange hello tryb urządzenia."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a>Użyj hello narzędzia diagnostycznego StorSimple tootroubleshoot 8000 serii problemów z urządzeniami

## <a name="overview"></a>Omówienie

Witaj narzędzia diagnostycznego StorSimple diagnozuje toosystem pokrewne problemy, wydajność sieci i kondycja składnika sprzętu dla urządzenia StorSimple. Narzędzie diagnostyczne Hello służy w różnych scenariuszach. Te scenariusze obejmują obciążenia planowania, wdrażania urządzenia StorSimple oceny środowiska sieciowego hello i określania hello wydajności operacyjnej urządzenia. Ten artykuł zawiera omówienie narzędzia diagnostycznego hello i zawiera opis sposobu użycia narzędzia hello z urządzeniem StorSimple.

Narzędzie diagnostyczne Hello jest przeznaczone głównie dla urządzeń lokalnych, serii StorSimple 8000 (8100 i 8600).

## <a name="run-diagnostics-tool"></a>Uruchom narzędzie diagnostyczne

To narzędzie można uruchomić za pomocą interfejsu programu Windows PowerShell hello urządzenia StorSimple. Istnieją dwa sposoby tooaccess hello lokalnego interfejsu urządzenia:

* [Konsoli szeregowej urządzenia użyj PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
* [Zdalny dostęp do narzędzia hello za pośrednictwem hello środowiska Windows PowerShell dla urządzenia StorSimple](storsimple-remote-connect.md).

W tym artykule przyjęto założenie, że nawiązano połączenie toohello konsolą szeregową urządzenia przy użyciu programu PuTTY.

#### <a name="toorun-hello-diagnostics-tool"></a>Narzędzie diagnostyczne hello toorun

Po połączeniu interfejsu programu Windows PowerShell toohello hello urządzenia, należy wykonać hello następującego polecenia cmdlet hello toorun czynności.
1. Zaloguj się na konsoli szeregowej urządzenia toohello wykonując kroki hello w [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).

2. Wpisz następujące polecenie hello:

    `Invoke-HcsDiagnostics`

    Jeśli nie określono parametru zakresu hello, polecenia cmdlet hello wykonuje wszystkich testów diagnostycznych hello. Te testy obejmują systemu, kondycja składnika sprzętu, sieci i wydajności. 
    
    toorun tylko określone testy, określ parametr zakresu hello. Na przykład toorun tylko hello test sieci, typ

    `Invoke-HcsDiagnostics -Scope Network`

3. Zaznacz i skopiuj dane wyjściowe hello z hello PuTTY okna do pliku tekstowego w celu dalszej analizy.

## <a name="scenarios-toouse-hello-diagnostics-tool"></a>Narzędzie diagnostyczne hello toouse scenariuszy

Użyj hello diagnostyki narzędzia tootroubleshoot hello sieci, wydajności systemu i sprzętu kondycję hello systemu. Poniżej przedstawiono kilka możliwych scenariuszy:

* **Urządzenie w trybie offline** -Your StorSimple 8000 serii urządzenie jest w trybie offline. Z hello interfejsu programu Windows PowerShell, prawdopodobnie czy obu kontrolerów hello są uruchomione i działają prawidłowo.
    * Za pomocą tego narzędzia toothen określić hello stanu sieci.
         
         > [!NOTE]
         > Nie należy używać tego narzędzia tooassess wydajności i ustawienia sieciowe na urządzenie przed hello rejestracji (lub konfigurowanie za pomocą Kreatora instalacji). Prawidłowymi adresami IP są przypisywane toohello urządzenia podczas Kreatora konfiguracji i rejestracji. To polecenie cmdlet można uruchomić na urządzeniu, które nie jest zarejestrowane dla kondycji sprzętu i systemu. Parametr hello zakresu, na przykład:
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* **Problemy dotyczące urządzenia trwałe** — występują problemy dotyczące urządzenia, które wydają się toopersist. Na przykład kończy się niepowodzeniem rejestracji. Użytkownik może również występować problemy dotyczące urządzenia po urządzenia hello jest pomyślnie zarejestrowane i działa przez pewien czas.
    * W takim przypadku to narzędzie do wstępnego rozwiązywania problemów przed zalogowaniem się żądania obsługi z Support firmy Microsoft. Firma Microsoft zaleca uruchomienie tego narzędzia i przechwytywania hello dane wyjściowe tego narzędzia. Możesz także podać dane wyjściowe tooSupport tooexpedite procedury rozwiązywania problemów.
    * W przypadku dowolnego składnika lub klastra awariami sprzętu należy rejestrować w żądaniu pomocy technicznej.

* **Niska wydajność urządzenia** -Your StorSimple urządzenia jest powolne.
    * W takim przypadku Uruchom to polecenie cmdlet z tooperformance zestaw parametrów zakresu. Analizowanie danych wyjściowych hello. Pobierz chmury hello opóźnienia odczytu i zapisu. Hello używany zgłaszane opóźnienia jako maksymalną docelowy osiągalne, współczynnik niektórych obciążenie hello wewnętrzne przetwarzanie danych, a następnie Wdróż hello obciążeń w systemie hello. Aby uzyskać więcej informacji, przejdź zbyt[Użyj hello sieci test tootroubleshoot urządzenia wydajności](#network-test).


## <a name="diagnostics-test-and-sample-outputs"></a>Wyniki testów i przykładowych diagnostyki

### <a name="hardware-test"></a>Test sprzętu

Ten test określa stan hello hello składniki sprzętowe, oprogramowania układowego należy hello i oprogramowanie układowe dysku hello uruchomionych w systemie.

* składniki sprzętowe Hello zgłaszane są te składniki test hello nie powiodło się lub nie są dostępne w systemie hello.
* Hello należy oprogramowania układowego i dysku wersji oprogramowania układowego są raportowane hello kontrolera 0 i kontrolera 1 i udostępnionych składników w systemie. Aby uzyskać pełną listę składników sprzętowych przejdź do:

    * [Składniki w obudowie podstawowego](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [Składniki w obudowie EBOD](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> Jeśli test sprzętu hello zgłasza błędne składniki [Zaloguj żądania obsługi ze Microsoft Support](storsimple-contact-microsoft-support.md).

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a>Przykładowe dane wyjściowe testu sprzętu uruchamianie na urządzeniu 8100

Oto przykładowe dane wyjściowe z urządzenia StorSimple 8100. W urządzeniu modelu 8100 hello hello obudowa EBOD jest nieobecny. W związku z tym hello EBOD kontrolera składniki nie są zgłaszane.

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a>Test systemu

Ten test raporty hello informacje o systemie, dostępne aktualizacje hello, informacje o klastrze hello i hello usługi informacje o urządzeniu.

* informacje o systemie Hello obejmuje hello modelu, numer seryjny urządzenia strefy czasowej, stan kontrolera i wersji oprogramowania szczegółowe hello uruchomiona w systemie hello. Witaj toounderstand różnych parametrów systemu zgłoszone jako dane wyjściowe hello, przejdź za[interpretacji informacji o systemie](#appendix-interpreting-system-information).

* czy hello tryby zwykłych oraz konserwacji są dostępne raporty Hello dostępności aktualizacji i ich nazw skojarzonego pakietu. Jeśli `RegularUpdates` i `MaintenanceModeUpdates` są `false`, oznacza to, że hello aktualizacje nie są dostępne. Urządzenie jest aktualny.
* informacje o klastrze Hello zawiera hello informacje na temat różnych składników logicznych wszystkie grupy klastra moduł HCS hello i ich odpowiednich stanów. Jeśli widzisz grupy klastra w trybie offline, w tej sekcji raportu hello [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md).
* Witaj usługi informacje obejmują hello nazwy i Stanami wszystkich hello moduł HCS i usługi konfiguracji (ci) są uruchomione na urządzeniu. Informacje te są przydatne do hello Microsoft Support przy rozwiązywaniu problemu urządzenia hello.

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a>Przykładowe dane wyjściowe testu systemu uruchamianie na urządzeniu 8100

Oto przykładowe dane wyjściowe testu systemu hello uruchamianie na urządzeniu 8100.

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a>Test sieci

Ten test sprawdza hello stan hello interfejsów sieciowych, porty, DNS i NTP łączności z serwerem, SSL certyfikatu, poświadczeń konta magazynu, łączności toohello aktualizacji serwerów i łączności serwera proxy sieci web na urządzeniu StorSimple.

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a>Przykładowe dane wyjściowe sieci testów, gdy jest włączona tylko DATA0

Oto przykładowe dane wyjściowe hello 8100 urządzenia. Można zobaczyć w danych wyjściowych hello który:
* Tylko dane 0 i 1 danych interfejsy sieciowe są włączone i skonfigurowane.
* DANE 2 5 nie są włączone w portalu hello.
* Konfiguracja serwera DNS Hello jest prawidłowy i hello urządzenie można połączyć za pośrednictwem powitania serwera DNS.
* Witaj łączności serwera NTP również funkcjonuje prawidłowo.
* Otwartych portów 80 i 443. Jednak port 9354 jest zablokowany. Oparte na powitania [wymagania sieciowe systemu](storsimple-system-requirements.md), należy tooopen ten port komunikacji hello magistrali usługi.
* certyfikacji SSL Hello jest prawidłowy.
* urządzenie Hello można połączyć konto magazynu toohello: _myss8000storageacct_.
* serwery tooUpdate łączności Hello jest prawidłowy.
* nie skonfigurowano serwera proxy sieci web Hello na tym urządzeniu.

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a>Przykładowe dane wyjściowe testu sieci, gdy są włączone DATA0 i dane1

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a>Test wydajności

Ten test raportów wydajności chmury hello za pośrednictwem hello chmury odczytu i zapisu opóźnienia dla danego urządzenia. To narzędzie może być używane tooestablish linię bazową wydajności chmury hello, który można uzyskać z StorSimple. Hello narzędzie raporty hello maksymalną wydajność (najlepsze scenariusz dla opóźnienia odczytu i zapisu), który można uzyskać połączenia.

Jak narzędzie hello zgłasza maksymalną wydajność osiągalne hello, możemy użyć hello zgłosił opóźnienia odczytu i zapisu jako obiekty docelowe, wdrażając hello obciążeń.

Badanie Hello symuluje hello rozmiarów obiektu blob skojarzony z typami inny wolumin hello na urządzeniu hello. Do warstwy standardowych i kopii zapasowych woluminów przypiętych lokalnie użyj rozmiar obiektu blob 64 KB. Woluminy warstwowe z zaznaczoną opcją archiwum Użyj rozmiar danych obiektu blob 512 KB. Jeśli urządzenie ma woluminów warstwowych i przypiętych lokalnie skonfigurowane, tylko hello testu odpowiedniego too64 KB blob rozmiar danych jest uruchomiony.

toouse to narzędzie, wykonaj następujące kroki hello:

1.  Najpierw utwórz mieszane woluminy warstwowe i woluminy warstwowe z zaznaczoną opcją zarchiwizowane. Ta akcja gwarantuje, że narzędzia hello uruchamia testy hello 64 KB i 512 KB rozmiarów obiektu blob.

2. Po utworzeniu i skonfigurowanych woluminach hello, należy uruchomić polecenie cmdlet hello. Wpisz:

    `Invoke-HcsDiagnostics -Scope Performance`

3. Zanotuj opóźnienia odczytu i zapisu hello zgłoszone przez narzędzie hello. Ten test może upłynąć kilka minut toorun zgłasza wyniki hello.

4. W przypadku opóźnienia połączenia hello wszystko pod hello oczekiwano zakresu, a następnie hello opóźnienia zgłoszone przez narzędzie hello mogą być używane jako maksymalną osiągalne docelowego podczas wdrażania hello obciążeń. Współczynnik niektórych obciążenie przetwarzania danych wewnętrznych.

    Jeśli opóźnienia odczytu i zapisu hello zgłoszone przez narzędzie Diagnostyka hello są wysokiej:

    1. Konfigurowanie magazynu Analytics usług obiektów blob i analizowanie hello dane wyjściowe toounderstand hello opóźnienia dla hello kontem magazynu platformy Azure. Aby uzyskać szczegółowe instrukcje, przejdź zbyt[włączyć i skonfigurować analityka magazynu](../storage/common/storage-enable-and-view-metrics.md). Jeśli te opóźnienia również są liczbami toohello wysokiej i porównywanie, otrzymany od hello narzędzia diagnostycznego StorSimple, należy toolog żądanie usługi z usługą Azure storage.

    2. Jeśli opóźnienia konta magazynu hello niski, skontaktuj się z Twojego tooinvestigate administratora sieci opóźnienia wszelkie problemy w sieci.

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a>Przykładowe dane wyjściowe uruchamiać na urządzeniu 8100 testu wydajności

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a>Dodatku: informacje o systemie interpretowanie

W tym miejscu znajduje się tabela opisujące jaki hello mapowania różnych parametrów środowiska Windows PowerShell w hello informacje o systemie. 

| Parametr programu PowerShell    | Opis  |
|-------------------------|------------------|
| Identyfikator wystąpienia             | Każdy kontroler ma unikatowego identyfikatora lub identyfikator GUID skojarzony z nim.|
| Nazwa                    | Witaj przyjazna nazwa urządzenia hello zgodnie z konfiguracją za pośrednictwem portalu Azure hello podczas wdrażania urządzenia. Przyjazna nazwa domyślna Hello jest numer seryjny urządzenia hello. |
| Model                   | model Hello urządzenia serii StorSimple 8000. Hello model może być 8100 lub 8600.|
| numer seryjny            | numer seryjny urządzenia Hello przydzielono fabryki hello i 15 znaków. Wskazuje, na przykład 8600 SHX0991003G44HT:<br> 8600 — jest hello model urządzenia.<br>SHX — jest hello produkcyjny lokacji.<br> 0991003 — jest określony produkt. <br> Unikatowe numery seryjne toocreate zwiększany G44HT-hello są ostatnich 5 cyfr. Nie można sekwencyjnych zestawu.|
| Strefa czasowa                | Witaj urządzenia strefa czasowa zgodnie z konfiguracją hello portalu Azure podczas wdrażania urządzenia.|
| CurrentController       | Kontroler Hello czy interfejsu programu Windows PowerShell hello toothrough podłączonego urządzenia StorSimple.|
| ActiveController        | Kontroler Hello jest aktywna na urządzeniu, który kontroluje wszystkie operacje hello sieci i dysku. Może to być kontrolera 0 i kontrolera 1.  |
| Controller0Status       | Stan Hello kontrolera 0 na urządzeniu. Stan kontrolera Hello może być normalna w trybie odzyskiwania lub jest niedostępny.|
| Controller1Status       | Witaj stan kontrolera 1 na urządzeniu.  Stan kontrolera Hello może być normalna w trybie odzyskiwania lub jest niedostępny.|
| SystemMode              | Witaj ogólny stan urządzenia StorSimple. Stan urządzenia Hello może być normalne, konserwacji lub wycofany z eksploatacji (odpowiada toodeactivated w hello portalu Azure).|
| FriendlySoftwareVersion | Witaj przyjazną ciąg, który odpowiada wersji oprogramowania toohello urządzenia. Komputerze z systemem aktualizacji 4 wersja oprogramowania przyjazną hello będzie StorSimple 8000 serii aktualizacji 4.0.|
| HcsSoftwareVersion      | wersji oprogramowania moduł HCS Hello działającej na urządzeniu. Na przykład Witaj odpowiedniego tooStorSimple wersji oprogramowania moduł HCS 8000 serii aktualizacji 4.0 jest 6.3.9600.17820. |
| ApiVersion              | Wersja oprogramowania Hello hello interfejsu API programu PowerShell systemu Windows hello moduł HCS urządzenia.|
| VhdVersion              | Wersja oprogramowania Hello hello fabryki obrazu, który hello urządzenia został wysłany z. Po zresetowaniu urządzenia domyślnych toofactory uruchomieniu tej wersji oprogramowania.|
| OSVersion               | wersja systemu operacyjnego Windows Server hello działającej na urządzeniu hello oprogramowania Hello. urządzenia StorSimple Hello opiera się poza hello systemu Windows Server 2012 R2, który odpowiada too6.3.9600.|
| CisAgentVersion         | Wersja Hello agenta konfiguracji (ci) uruchomione na urządzeniu StorSimple. Ten agent pomaga komunikować się z usługą Menedżer StorSimple hello działające na platformie Azure.|
| MdsAgentVersion         | Witaj wersji odpowiedniego toohello Mds agenta uruchomionego na urządzeniu StorSimple. Ten agent przenosi toohello danych monitorowania i diagnostyki usługi (MDS).|
| Lsisas2Version          | Witaj odpowiednich sterowników toohello LSI wersji na urządzeniu StorSimple.|
| Pojemność                | Całkowita pojemność Hello urządzenia hello w bajtach.|
| RemoteManagementMode    | Wskazuje, czy urządzenie hello mogą być zarządzane zdalnie za pośrednictwem jej interfejsu programu Windows PowerShell. |
| FipsMode                | Wskazuje, czy tryb Stanów Zjednoczonych informacji przetwarzania Standard FIPS (Federal) hello jest włączony na twoim urządzeniu. standard Hello FIPS 140 definiuje zatwierdzone do użycia przez nas federalne systemów komputerowych dla instytucji rządowych hello ochrony danych poufnych algorytmów kryptograficznych. W przypadku urządzeń programu Update 4 lub nowszego trybie FIPS jest domyślnie włączona. |

## <a name="next-steps"></a>Następne kroki

* Dowiedz się hello [składni polecenia cmdlet Invoke-HcsDiagnostics hello](https://technet.microsoft.com/library/mt795371.aspx).

* Dowiedz się więcej o tym, jak za[Rozwiązywanie problemów dotyczących wdrożenia](storsimple-troubleshoot-deployment.md) na urządzeniu StorSimple.
