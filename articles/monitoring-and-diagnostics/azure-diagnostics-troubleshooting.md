---
title: aaaTroubleshooting diagnostyki Azure | Dokumentacja firmy Microsoft
description: "Rozwiązywanie problemów, gdy za pomocą diagnostyki Azure w maszynach wirtualnych platformy Azure, sieci szkieletowej usług lub usługi w chmurze."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 66469bce-d457-4d1e-b550-a08d2be4d28c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: robb
ms.openlocfilehash: daaf9fa4c40982eb9ba04030d7e8ea1ad9fe085b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-troubleshooting"></a>Rozwiązywanie problemów Diagnostyka Azure
Rozwiązywanie problemów z toousing odpowiednich informacji diagnostycznych platformy Azure. Aby uzyskać więcej informacji na diagnostycznych platformy Azure, zobacz [Omówienie diagnostyki Azure](azure-diagnostics.md).

## <a name="logical-components"></a>Logiczne składniki
**Uruchamianie diagnostyki wtyczki programu (DiagnosticsPluginLauncher.exe)**: uruchamia hello Azure Diagnostics rozszerzenia. Służy jako wpis hello procesu punktu.

**Diagnostyka wtyczki (DiagnosticsPlugin.exe)**: główny proces, który jest uruchamiana przez hello uruchamiania powyższej i konfiguruje hello agenta monitorowania, uruchamia ją i zarządza nimi jego okres istnienia. 

**Monitoring Agent (MonAgent\*procesy .exe)**: te procesy hello zbiorczego pracy hello; np. monitorowanie, zbierania i przekazywania hello danych diagnostycznych.  

## <a name="logartifact-paths"></a>Ścieżki dziennika/artefaktów
Poniżej przedstawiono hello ścieżki toosome ważne dzienniki i artefaktów. Firma Microsoft zachować przywołuje toothese w całym hello pozostałej części dokumentu hello:
### <a name="cloud-services"></a>Cloud Services
| Artefaktów | Ścieżka |
| --- | --- |
| **Plik konfiguracji diagnostyki Azure** | %SYSTEMDRIVE%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<wersji > \Config.txt |
| **Pliki dziennika** | C:\Logs\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<wersji > \ |
| **Magazyn lokalny dla danych diagnostycznych** | C:\Resources\Directory\<CloudServiceDeploymentID >.\< RoleName >. DiagnosticStore\WAD0107\Tables |
| **Plik konfiguracji agenta monitorowania** | C:\Resources\Directory\<CloudServiceDeploymentID >.\< RoleName >. DiagnosticStore\WAD0107\Configuration\MaConfig.xml |
| **Pakiet rozszerzenia Diagnostyka Azure** | %SYSTEMDRIVE%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<wersji > |
| **Ścieżka narzędzia kolekcji dziennika** | %SYSTEMDRIVE%\Packages\GuestAgent\ |
| **Plik dziennika MonAgentHost** | C:\Resources\Directory\<CloudServiceDeploymentID >.\< RoleName >. DiagnosticStore\WAD0107\Configuration\MonAgentHost. < seq_num > .log |

### <a name="virtual-machines"></a>Maszyny wirtualne
| Artefaktów | Ścieżka |
| --- | --- |
| **Plik konfiguracji diagnostyki Azure** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<wersji > \RuntimeSettings |
| **Pliki dziennika** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<wersji > \Logs\ |
| **Magazyn lokalny dla danych diagnostycznych** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion > \WAD0107\Tables |
| **Plik konfiguracji agenta monitorowania** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion > \WAD0107\Configuration\MaConfig.xml |
| **Plik stanu** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<wersji > \Status |
| **Pakiet rozszerzenia Diagnostyka Azure** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion >|
| **Ścieżka narzędzia kolekcji dziennika** | C:\WindowsAzure\Packages |
| **Plik dziennika MonAgentHost** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion > \WAD0107\Configuration\MonAgentHost. < seq_num > .log |

## <a name="metric-data-doesnt-show-in-azure-portal"></a>Dane nie pojawiają się w portalu Azure
Diagnostyka Azure zapewnia zbiór danych metryki, które mogą być wyświetlane w portalu Azure. Jeśli masz problemy z tych danych w portalu konta magazynu diagnostyki hello wyboru -> WADMetrics\* tabeli toosee, jeśli istnieją odpowiednie rekordy metryki hello. W tym miejscu hello PartitionKey tabeli hello jest hello identyfikator zasobu maszyny wirtualnej lub zestaw skali maszyny wirtualnej, a hello RowKey jest nazwa metryki hello tj. Nazwa licznika wydajności.

Jeśli identyfikator zasobu hello jest niepoprawny, sprawdź konfigurację diagnostyki -> metryki -> ResourceId toosee, jeśli identyfikator zasobu hello jest ustawiony poprawnie.

Jeśli nie ma żadnych danych dla określonej metryki hello, sprawdź konfigurację diagnostyki -> PerformanceCounter toosee, jeśli Metryka hello (licznika wydajności) jest dołączony. Włącz firma Microsoft hello następujące liczniki domyślnie.
- \Processor(_Total)\% Processor Time
- \Memory\Available Bytes
- Aplikacje \ASP.NET (__całkowita__) \Requests/Sec
- Aplikacje \ASP.NET (__całkowita__) \Errors/s
- \ASP.NET\Requests umieszczonych w kolejce.
- \ASP.NET\Requests odrzucone
- \Processor(W3wp)\% czas procesora
- Bajty \Private \Process (w3wp)
- \Process(WaIISHost)\% czas procesora
- Bajty \Private \Process (WaIISHost)
- \Process(WaWorkerHost)\% czas procesora
- Bajty \Private \Process (WaWorkerHost)
- \Memory\Page błędów na sekundę
- \.NET CLR pamięci (_globalne_)\% czasu odzyskiwania pamięci
- Bajty zapisu \Disk \LogicalDisk (C:) / s
- \Disk \LogicalDisk (C:) do odczytu w bajtach na sekundę
- Bajty zapisu \Disk \LogicalDisk (D:) / s
- \Disk \LogicalDisk (D:) do odczytu w bajtach na sekundę

Jeśli konfiguracja hello została poprawnie ustawiona, ale nie widać danych metryki hello nadal, zgodna z wytycznymi hello poniżej hello wskazówki.


## <a name="azure-diagnostics-is-not-starting"></a>Diagnostyka Azure nie jest uruchamiana.
Przyjrzyj się **DiagnosticsPluginLauncher.log** i **DiagnosticsPlugin.log** plików z lokalizacji hello hello podane powyżej dla informacji o tym, dlaczego diagnostyki nie powiodło się toostart pliki dziennika. 

Jeśli te dzienniki wskazują `Monitoring Agent not reporting success after launch`, oznacza to, wystąpił błąd podczas uruchamiania MonAgentHost.exe. Przeglądać hello dzienników dla tej lokalizacji hello określić `MonAgentHost log file` hello powyżej w sekcji.

ostatni wiersz Hello hello plików dziennika zawiera kod zakończenia hello.  

```
DiagnosticsPluginLauncher.exe Information: 0 : [4/16/2016 6:24:15 AM] DiagnosticPlugin exited with code 0
```
Jeśli okaże się **ujemna** kod zakończenia, zapoznaj się toohello [tabeli Kod zakończenia](#azure-diagnostics-plugin-exit-codes) w hello [odwołania](#references).

## <a name="diagnostics-data-is-not-logged-tooazure-storage"></a>Dane diagnostyczne jest rejestrowane nie tooAzure magazynu
Ustal, czy żadne dane nie pokazuje, czy tylko niektóre z danych hello nie pojawia się.

### <a name="diagnostics-infrastructure-logs"></a>Dzienniki infrastruktury diagnostyki
Dzienniki infrastruktury diagnostyki jest, którym diagnostyki azure rejestruje wszystkie błędy, które działa w. Upewnij się, że włączono ([jak?](#how-to-check-diagnostics-extension-configuration)) zbieranie dzienników diagnostycznych infrastruktury w konfiguracji i szybko Wyszukaj błędy odpowiednich wyświetlanych w hello `DiagnosticInfrastructureLogsTable` tabeli na koncie skonfigurowany magazyn.

### <a name="no-data-is-showing-up"></a>Żadne dane nie pokazuje
Najczęstszą przyczyną Hello całkowicie brakujących danych zdarzenia jest informacji o koncie magazynu nieprawidłowo zdefiniowany.

Rozwiązanie: Poprawić konfigurację diagnostyki i ponowne zainstalowanie diagnostyki.

Jeśli konto magazynu hello jest skonfigurowana poprawnie, zdalnego pulpitu na powitania komputera i upewnij się, że DiagnosticsPlugin.exe i MonAgentCore.exe są uruchomione. Jeśli nie są uruchomione, wykonaj [nie uruchamia się diagnostyki Azure](#azure-diagnostics-is-not-starting). Jeśli są uruchomione procesy hello, przejść za[dane pierwsze przechwycone lokalnie](#is-data-getting-captured-locally) i wykonaj w tym przewodniku stamtąd.

### <a name="part-of-hello-data-is-missing"></a>Brakuje części hello danych
W przypadku uzyskiwania niektórych danych, ale nie innych. Oznacza to, że zbieranie danych hello / transfer potoku jest ustawiony poprawnie. Wykonaj podpunkty hello Oto toonarrow dół jaki problem hello:
#### <a name="is-collection-configured"></a>Skonfigurowano kolekcji: 
Diagnostyka konfiguracji zawiera część hello, która sprawia, że dla określonego typu toobe dane zbierane. [Przejrzyj konfigurację](#how-to-check-diagnostics-extension-configuration) toomake się, że nie szukasz danych możesz nie zostały skonfigurowane dla kolekcji.
#### <a name="is-hello-host-generating-data"></a>Hello host generuje dane:
- **Liczniki wydajności**: Otwórz monitora wydajności i Sprawdź licznik hello.
- **Dzienniki śledzenia**: pulpitu zdalnego do hello maszyny Wirtualnej, a następnie dodaj TextWriterTraceListener toohello w pliku konfiguracji aplikacji.  Zobacz tooset http://msdn.microsoft.com/library/sk36c28t.aspx się hello tekst odbiornika.  Upewnij się, że hello `<trace>` element ma `<trace autoflush="true">`.<br />
Jeśli nie widzisz generowanych dzienniki śledzenia, należy wykonać [więcej o śledzenia dzienniki Brak](#more-about-trace-logs-missing).
- **Ślady ETW**: pulpitu zdalnego do maszyny Wirtualnej hello i zainstaluj narzędzia PerfView.  W narzędzia PerfView uruchamiany plik -> polecenia User -> etwprovder1 nasłuchiwania, etwprovider2 itp.  Należy pamiętać, że polecenia nasłuchiwania hello jest rozróżniana wielkość liter i nie może być spacji między hello rozdzielaną przecinkami listę dostawców ETW.  Polecenie hello nie powiedzie się toorun, po kliknięciu przycisku "Logowanie" hello w prawej dolnej hello hello narzędzia Perfview narzędzia toosee, który jaka była próba toorun i jakie wyniku hello jest.  Zakładając, że hello dane wejściowe są poprawne, następnie nowe okno będzie pop w górę i w ciągu kilku sekund zostanie rozpoczęta wyświetlanie śladów ETW.
- **Dzienniki zdarzeń**: pulpitu zdalnego na powitania maszyny Wirtualnej. Otwórz `Event Viewer` i upewnij się, istnieje hello zdarzenia.
#### <a name="is-data-getting-captured-locally"></a>Dane pobierania przechwytywania lokalnie:
Następnie upewnij się, że dane hello jest wprowadzenie przechwytywane lokalnie.
dane Hello lokalnie są przechowywane w `*.tsf` plików [hello lokalnego magazynu dla danych diagnostycznych](#log-artifacts-path). Różne rodzaje dzienniki uzyskać zebrane w różnych `.tsf` plików. nazwy Hello są podobne toohello nazwy tabeli w magazynie azure. Na przykład `Performance Counters` uzyskać zbierane w `PerformanceCountersTable.tsf`, dzienniki zdarzeń uzyskać zebrane w `WindowsEventLogsTable.tsf`. Użyj instrukcji hello w [lokalnego wyodrębniania dziennika](#local-log-extraction) sekcji tooopen hello lokalną kolekcję plików i upewnij się, że ich wprowadzenie zebrane na dysku.

Jeśli nie, zobacz dzienniki pobierania pobierane lokalnie i ma już zweryfikowaniu się, że hello host jest generowania danych, prawdopodobnie masz problem z konfiguracją. Zapoznaj się uważnie hello odpowiedniej sekcji konfiguracji. Również przejrzeć konfigurację hello wygenerowany dla MonitoringAgent [MaConfig.xml](#log-artifacts-path) i upewnij się, że ma niektórych części opisujący źródło dziennika odpowiednich hello i że nie zostaną utracone w tłumaczeniu między konfiguracji Diagnostyka azure i konfiguracji agenta monitorowania.
#### <a name="is-data-getting-transferred"></a>Jest przekazywane pobierania danych:
Jeśli po sprawdzeniu danych hello jest pierwsze przechwycone lokalnie, ale nadal nie widać na koncie magazynu: 
- Najpierw i, upewnij się, podane konto magazynu poprawne i że użytkownik ma nie przerzuceniem hello etc.for klucze podane konto magazynu. Dla usług w chmurze, czasami widzimy, że osoby nie aktualizuj ich `useDevelopmentStorage=true`.
- Jeśli pod warunkiem, że konto magazynu jest poprawna. Upewnij się, że nie ma pewne ograniczenia sieci, które nie zezwalają na punkty końcowe magazynu publicznego tooreach hello składników. Jednym ze sposobów toodo, będący tooremote pulpitu na powitania maszyny i spróbuj toowrite coś toohello magazynu tego samego konta użytkownika.
- Na koniec można spróbuj i zobacz, jakie niepowodzenia są zgłaszane przez agenta monitorowania. Agent monitorowania zapisuje dzienniki jej `maeventtable.tsf` znajduje się w [hello lokalnego magazynu dla danych diagnostycznych](#log-artifacts-path). Postępuj zgodnie z instrukcjami wyświetlanymi w [lokalnego wyodrębniania dziennika](#local-log-extraction) sekcji tooopen ten plik i spróbuj i ustalić, czy istnieją `errors` wskazujący błędów tooread lokalnych plików lub zapis toostorage.

### <a name="capturing--archiving-logs"></a>Przechwytywanie / archiwizowanie dzienników
Wykonano kroki hello powyżej kroki, ale nie można dowiedzieć się, co jest nieprawidłowa i są myślenia o skontaktowaniu się z pomocą techniczną. Witaj najpierw pracownik może poprosić o jest toocollect dzienniki z komputera. Wykonując tego użytkownika, można zaoszczędzić czas. Uruchom hello `CollectGuestLogs.exe` narzędzia na [ścieżkę dostępu do dziennika narzędzia kolekcji](#log-artifacts-path) i generuje plik zip ze wszystkich odpowiednich dzienników azure w hello tym samym folderze.

## <a name="diagnostics-data-tables-not-found"></a>Dane diagnostyczne nie znaleziono tabel
tabele Hello w magazynie Azure zawierający zdarzenia ETW są nazywane przy użyciu hello następującego kodu:

```C#
        if (String.IsNullOrEmpty(eventDestination)) {
            if (e == "DefaultEvents")
                tableName = "WADDefault" + MD5(provider);
            else
                tableName = "WADEvent" + MD5(provider) + eventId;
        }
        else
            tableName = "WAD" + eventDestination;
```

Oto przykład:

```XML
        <EtwEventSourceProviderConfiguration provider="prov1">
          <Event id="1" />
          <Event id="2" eventDestination="dest1" />
          <DefaultEvents />
        </EtwEventSourceProviderConfiguration>
        <EtwEventSourceProviderConfiguration provider="prov2">
          <DefaultEvents eventDestination="dest2" />
        </EtwEventSourceProviderConfiguration>
```
```JSON
"EtwEventSourceProviderConfiguration": [
    {
        "provider": "prov1",
        "Event": [
            {
                "id": 1
            },
            {
                "id": 2,
                "eventDestination": "dest1"
            }
        ],
        "DefaultEvents": {
            "eventDestination": "DefaultEventDestination",
            "sinks": ""
        }
    },
    {
        "provider": "prov2",
        "DefaultEvents": {
            "eventDestination": "dest2"
        }
    }
]
```
Spowoduje to wygenerowanie 4 tabel:

| Wydarzenie | Nazwa tabeli |
| --- | --- |
| Dostawca = "prov1" &lt;identyfikator zdarzenia = "1" /&gt; |WADEvent + MD5("prov1") + "1" |
| Dostawca = "prov1" &lt;identyfikator zdarzenia = "2" eventDestination = "dest1" /&gt; |WADdest1 |
| Dostawca = "prov1" &lt;DefaultEvents /&gt; |WADDefault+MD5("prov1") |
| Dostawca = "prov2" &lt;DefaultEvents eventDestination = "dest2" /&gt; |WADdest2 |

## <a name="references"></a>Dokumentacja

### <a name="how-toocheck-diagnostics-extension-configuration"></a>Jak toocheck Konfiguracja rozszerzenia diagnostyki
Najprostszym sposobem toocheck Hello konfiguracji rozszerzenia toonavigate toohttp://resources.azure.com, przejść toohello wirtualnych maszyny lub usługę w chmurze na które hello rozszerzenie Azure Diagnostics (IaaSDiagnostics / PaaDiagnostics) jest zagrożona.

Alternatywnie pulpitu zdalnego na komputerze hello i znajduje się w pliku konfiguracji diagnostyki Azure hello opisane w odpowiedniej sekcji hello [tutaj](#log-artifacts-path).

W przypadku wyszukać **Microsoft.Azure.Diagnostics** następnie dla hello **xmlCfg** lub **WadCfg** pola. 

W przypadku maszyn wirtualnych Jeśli pole WadCfg hello jest obecny, oznacza to, że hello config jest w formacie JSON. Jeśli pole xmlCfg hello jest obecny, oznacza to, hello config jest w formacie XML i jest kodowany w formacie base64. Należy zbyt[zdekodować](http://www.bing.com/search?q=base64+decoder) hello toosee kod XML, który został załadowany przez diagnostyki.

Dla roli usługi w chmurze, w przypadku wybrania konfiguracji hello z dysku, dane hello jest kodowanie base64, konieczne będzie zbyt[zdekodować](http://www.bing.com/search?q=base64+decoder) hello toosee kod XML, który został załadowany przez diagnostyki.

### <a name="azure-diagnostics-plugin-exit-codes"></a>Kody zakończenia wtyczki Diagnostyka Azure
Dodatek Hello zwraca hello następujące kody zakończenia:

| Kod zakończenia | Opis |
| --- | --- |
| 0 |Powodzenie. |
| -1 |Błąd rodzajowy. |
| -2 |Nie można tooload hello rcf pliku.<p>Ten błąd wewnętrzny tylko powinien nastąpić, jeśli niepoprawnie, uruchamiania wtyczki agenta gościa hello ręcznie jest wywoływana na powitania maszyny Wirtualnej. |
| -3 |Nie można załadować pliku konfiguracji hello diagnostyki.<p><p>Rozwiązanie: Spowodowane nie przeszły sprawdzanie poprawności schematu pliku konfiguracji. rozwiązanie Hello jest tooprovide pliku konfiguracji, który jest zgodny ze schematem hello. |
| -4 |Inne wystąpienie hello monitorowania agenta diagnostyki już używa hello zasobu lokalnego katalogu.<p><p>Rozwiązanie: Określ inną wartość dla **LocalResourceDirectory**. |
| -6 |Uruchamianie wtyczki agenta gościa Hello podjęto diagnostyki toolaunch z nieprawidłowy wiersz polecenia.<p><p>Ten błąd wewnętrzny tylko powinien nastąpić, jeśli niepoprawnie, uruchamiania wtyczki agenta gościa hello ręcznie jest wywoływana na powitania maszyny Wirtualnej. |
| -10 |wtyczki diagnostyki Hello został zakończony z powodu nieobsługiwanego wyjątku. |
| -11 |agent gościa Hello była toocreate hello procesu odpowiedzialnego za monitorowanie hello agenta monitorowania i uruchamiania.<p><p>Rozwiązanie: Sprawdź, czy wystarczające zasoby systemowe są dostępne toolaunch nowych procesów.<p> |
| -101 |Nieprawidłowe argumenty podczas wywoływania metody hello diagnostyki wtyczki.<p><p>Ten błąd wewnętrzny tylko powinien nastąpić, jeśli niepoprawnie, uruchamiania wtyczki agenta gościa hello ręcznie jest wywoływana na powitania maszyny Wirtualnej. |
| -102 |proces wtyczki Hello jest tooinitialize, samej siebie.<p><p>Rozwiązanie: Sprawdź, czy wystarczające zasoby systemowe są dostępne toolaunch nowych procesów. |
| -103 |proces wtyczki Hello jest tooinitialize, samej siebie. W szczególności jest toocreate hello rejestratora obiekt.<p><p>Rozwiązanie: Sprawdź, czy wystarczające zasoby systemowe są dostępne toolaunch nowych procesów. |
| -104 |Plik rcf hello tooload dostarczonej przez agenta gościa hello.<p><p>Ten błąd wewnętrzny tylko powinien nastąpić, jeśli niepoprawnie, uruchamiania wtyczki agenta gościa hello ręcznie jest wywoływana na powitania maszyny Wirtualnej. |
| -105 |wtyczki diagnostyki Hello nie można otworzyć pliku konfiguracji hello diagnostyki.<p><p>Ten błąd wewnętrzny tylko powinien nastąpić, jeśli niepoprawnie, wtyczki diagnostyki hello ręcznie jest wywoływana na powitania maszyny Wirtualnej. |
| -106 |Nie można odczytać pliku konfiguracji hello diagnostyki.<p><p>Rozwiązanie: Spowodowane nie przeszły sprawdzanie poprawności schematu pliku konfiguracji. To rozwiązanie hello jest tooprovide pliku konfiguracji, który jest zgodny ze schematem hello. Zobacz [jak toocheck Konfiguracja rozszerzenia diagnostyki](#how-to-check-diagnostics-extension-configuration). |
| -107 |Witaj zasobu katalogu przebiegu toohello agenta monitorowania jest nieprawidłowy.<p><p>Ten błąd wewnętrzny tylko powinien nastąpić, jeśli niepoprawnie, hello agenta monitorowania ręcznie jest wywoływana na powitania maszyny Wirtualnej.</p> |
| -108 |Tooconvert hello diagnostyki plik konfiguracji do hello plikiem konfiguracji agenta monitorowania.<p><p>Ten błąd wewnętrzny tylko powinien nastąpić, jeśli wtyczki diagnostyki hello ręcznie została wywołana z nieprawidłowy plik konfiguracji. |
| -110 |Błąd konfiguracji diagnostyki ogólne.<p><p>Ten błąd wewnętrzny tylko powinien nastąpić, jeśli wtyczki diagnostyki hello ręcznie została wywołana z nieprawidłowy plik konfiguracji. |
| -111 |Nie można toostart hello agenta monitorowania.<p><p>Rozwiązanie: Sprawdź, czy dostępne są wystarczające zasoby systemu. |
| -112 |Błąd ogólny |

### <a name="local-log-extraction"></a>Wyodrębnianie lokalnym dzienniku
Witaj agenta monitorowania zbiera dzienniki i artefaktów jak `.tsf` plików. `.tsf`plik nie jest do odczytu, ale można przekonwertować go do `.csv` w następujący sposób: 

```
<Azure diagnostics extension package>\Monitor\x64\table2csv.exe <relevantLogFile>.tsf
```
Nowy plik o nazwie `<relevantLogFile>.csv` zostaną utworzone w hello sama ścieżka jako odpowiadającego hello `.tsf` pliku.

**Uwaga**: wystarczy toorun tego narzędzia na powitania tsf głównego pliku (np. PerformanceCountersTable.tsf). Hello załączonych plików (np. PerformanceCountersTables_\*\*001.tsf, PerformanceCountersTables_\*\*tsf 002. itp.) zostaną automatycznie przetworzone.

### <a name="more-about-trace-logs-missing"></a>Więcej informacji na temat Brak dzienniki śledzenia

**Uwaga:** najczęściej dotyczy to usługi toocloud tylko, jeśli nie skonfigurowano hello DiagnosticsMonitorTraceListener na aplikacji działających na maszynie Wirtualnej IaaS. 

- Upewnij się, że hello, DiagnosticMonitorTraceListener jest skonfigurowany na powitania plik web.config lub app.config.  Jest to konfiguracja domyślna w projekty usługi w chmurze, ale niektórzy klienci komentarz go poza, co spowoduje toonot instrukcje śledzenia hello zebrane przez diagnostyki. 
- Jeśli nie pobierania dziennikach z hello OnStart lub uruchom — metoda upewnij się, że hello DiagnosticMonitorTraceListener znajduje się w pliku app.config hello.  Domyślnie jest on w pliku web.config hello, ale dotyczy tylko toocode działających w w3wp.exe; Dlatego należy go uruchomionych w WaIISHost.exe śladów toocapture app.config.
- Upewnij się, że używasz Diagnostics.Trace.TraceXXX zamiast Diagnostics.Debug.WriteXXX.  Witaj debugować instrukcje zostaną usunięte z kompilacji wydania.
- Upewnij się, że kod hello skompilowany faktycznie liniami hello Diagnostics.Trace (Użyj reflektora, narzędzia ildasm lub ILSpy tooverify).  Polecenia Diagnostics.Trace są usuwane z hello kompilowane dane binarne, chyba że symbol kompilacji warunkowej śledzenia hello jest używany.  Jeśli przy użyciu programu msbuild toobuild hello projektu to typowe toorun problem do.

## <a name="known-issues-and-mitigations"></a>Znane problemy i środki zaradcze
Poniżej przedstawiono listę znanych problemów z znane środki zaradcze:

**1. .NET 4.5 zależności:**

WAD ma zależności aparatu plików wykonywalnych w ramach platformy .NET 4.5 lub nowszym. Podczas hello zapisu to wszystkie maszyny obsługi administracyjnej dla usługi w chmurze, a także wszystkie oficjalnego azure obrazy maszyny wirtualnej podstawowej ma .NET 4.5 lub wcześniej zainstalowane. Jest jednak nadal możliwe tooland w sytuacji, gdy spróbujesz toorun WAD na komputerze, który nie ma .NET 4.5 lub nowszy. Dzieje się tak podczas tworzenia komputera poza stary obraz lub migawki; lub przenieść niestandardowego dysku.

Zazwyczaj jest to manifesty jako kod zakończenia **255** podczas uruchamiania DiagnosticsPluginLauncher.exe. Błąd sytuacji powodu toohello nieobsługiwany wyjątek: 
```
System.IO.FileLoadException: Could not load file or assembly 'System.Threading.Tasks, Version=1.5.11.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies
```

**Ograniczenie:** instalacji platformy .NET 4.5 lub nowszej na tym komputerze.

**2. Dostępne w magazynu, ale nie są wyświetlane w portalu danych liczników wydajności**

Maszyny wirtualne środowisko portalu przedstawia niektóre liczniki wydajności domyślnie. Jeśli nie są one wyświetlane i wiesz, że dane hello jest wprowadzenie wygenerowane, ponieważ jest ona dostępna w magazynie. Sprawdzanie:
- Jeśli hello dane w magazynie mają nazwy liczników w języku angielskim. Jeśli nazwy licznika hello nie są w języku angielskim, portalu metryki wykresu nie będzie toorecognize może go.
- Jeśli używane są symbole wieloznaczne (\*) w nazwy licznika wydajności hello portalu nie będą mogli toocorrelate hello skonfigurowane i zebranych licznika.

**Środki zaradcze**: Zmień tooEnglish języka hello maszyny dla konta system. Region -> Panel sterowania -> administracyjne -> Ustawienia kopii -> Usuń zaznaczenie pola wyboru "Zapraszamy ekranu i systemu kont", aby hello niestandardowych język nie jest stosowane toosystem konta. Upewnij się, że nie należy używać symbole wieloznaczne, jeśli ma portalu toobe środowiska głównej zużycia.
