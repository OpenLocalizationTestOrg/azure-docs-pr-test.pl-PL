---
title: "Rozwiązywanie problemów z diagnostyki Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: a0cb529836b14df71e83616f4f625a002c535b7b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-diagnostics-troubleshooting"></a>Rozwiązywanie problemów Diagnostyka Azure
Rozwiązywanie problemów z informacje istotne przy użyciu diagnostyki Azure. Aby uzyskać więcej informacji na diagnostycznych platformy Azure, zobacz [Omówienie diagnostyki Azure](azure-diagnostics.md).

## <a name="logical-components"></a>Logiczne składniki
**Uruchamianie diagnostyki wtyczki programu (DiagnosticsPluginLauncher.exe)**: uruchamia rozszerzenia diagnostyki Azure. Służy jako wpis punktu procesu.

**Diagnostyka wtyczki (DiagnosticsPlugin.exe)**: główny proces, który jest uruchamiana przez uruchamiania powyższej i konfiguruje agenta monitorowania, uruchamia ją i zarządza nimi jego okres istnienia. 

**Monitoring Agent (MonAgent\*procesy .exe)**: te procesy czy większość pracy; np. monitorowanie, zbierania i przekazywania danych diagnostycznych.  

## <a name="logartifact-paths"></a>Ścieżki dziennika/artefaktów
Poniżej przedstawiono ścieżki do niektórych dzienników ważne i artefaktów. Firma Microsoft zachować odwołujących się do tych w dalszej części dokumentu:
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
Diagnostyka Azure zapewnia zbiór danych metryki, które mogą być wyświetlane w portalu Azure. Jeśli masz problemy z tych danych w portalu, sprawdź konto magazynu diagnostyki -> WADMetrics\* tabeli, aby sprawdzić, czy są odpowiednie rekordy metryki. W tym miejscu PartitionKey tabeli jest identyfikator zasobu maszyny wirtualnej lub zestaw skali maszyny wirtualnej, a RowKey jest nazwa metryki, np. Nazwa licznika wydajności.

Jeśli identyfikator zasobu jest nieprawidłowy, sprawdź konfigurację diagnostyki -> metryki -> ResourceId, aby zobaczyć, czy identyfikator zasobu jest ustawiony poprawnie.

Jeśli nie ma żadnych danych dla określonej metryki, sprawdź konfigurację diagnostyki -> PerformanceCounter, jeśli metryka (licznika wydajności) jest dołączony. Domyślnie włączyć następujące liczniki.
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

Jeśli konfiguracja została poprawnie ustawiona, ale nadal nie widzisz dane metryk, postępuj zgodnie z wytycznymi poniżej, aby uzyskać dalsze badanie.


## <a name="azure-diagnostics-is-not-starting"></a>Diagnostyka Azure nie jest uruchamiana.
Przyjrzyj się **DiagnosticsPluginLauncher.log** i **DiagnosticsPlugin.log** plików z lokalizacji plików dziennika podanego powyżej, aby uzyskać informacje dotyczące przyczyny diagnostyki nie powiodło się. 

Jeśli te dzienniki wskazują `Monitoring Agent not reporting success after launch`, oznacza to, wystąpił błąd podczas uruchamiania MonAgentHost.exe. Poszukaj w dziennikach który w lokalizacji wskazanej dla `MonAgentHost log file` w powyższej sekcji.

Ostatni wiersz w pliku dziennika zawiera kod wyjścia.  

```
DiagnosticsPluginLauncher.exe Information: 0 : [4/16/2016 6:24:15 AM] DiagnosticPlugin exited with code 0
```
Jeśli okaże się **ujemna** kod zakończenia, zapoznaj się [tabeli Kod zakończenia](#azure-diagnostics-plugin-exit-codes) w [odwołania](#references).

## <a name="diagnostics-data-is-not-logged-to-azure-storage"></a>Dane diagnostyczne jest nie zalogował się do usługi Azure Storage
Ustal, czy żadne dane nie pokazuje, czy tylko niektóre dane nie pojawia się.

### <a name="diagnostics-infrastructure-logs"></a>Dzienniki infrastruktury diagnostyki
Dzienniki infrastruktury diagnostyki jest, którym diagnostyki azure rejestruje wszystkie błędy, które działa w. Upewnij się, że włączono ([jak?](#how-to-check-diagnostics-extension-configuration)) zbieranie dzienników diagnostycznych infrastruktury w konfiguracji i szybko znaleźć odpowiednie błędów, które pojawiają się w `DiagnosticInfrastructureLogsTable` tabeli na koncie skonfigurowany magazyn.

### <a name="no-data-is-showing-up"></a>Żadne dane nie pokazuje
Najczęstszą przyczyną zdarzenia, które są całkowicie brakujące dane, jest nieprawidłowo zdefiniowany informacji o koncie magazynu.

Rozwiązanie: Poprawić konfigurację diagnostyki i ponowne zainstalowanie diagnostyki.

Jeśli konto magazynu jest poprawnie skonfigurowana, zdalnego pulpitu na komputerze i upewnij się, że DiagnosticsPlugin.exe i MonAgentCore.exe są uruchomione. Jeśli nie są uruchomione, wykonaj [nie uruchamia się diagnostyki Azure](#azure-diagnostics-is-not-starting). Jeśli są uruchomione procesy, należy przejść do [dane pierwsze przechwycone lokalnie](#is-data-getting-captured-locally) i wykonaj w tym przewodniku stamtąd.

### <a name="part-of-the-data-is-missing"></a>Brakuje części danych
W przypadku uzyskiwania niektórych danych, ale nie innych. Oznacza to, że zbieranie danych / transfer potoku jest ustawiony poprawnie. Podpunkty w tym miejscu należy wykonać, aby zawęzić problemu:
#### <a name="is-collection-configured"></a>Skonfigurowano kolekcji: 
Diagnostyka konfiguracji zawiera element, który powoduje, że dla określonego typu danych mają być zbierane. [Przejrzyj konfigurację](#how-to-check-diagnostics-extension-configuration) się upewnić, że nie szukasz danych nie zostały skonfigurowane dla kolekcji.
#### <a name="is-the-host-generating-data"></a>Host generuje dane:
- **Liczniki wydajności**: Otwórz monitora wydajności i Sprawdź licznik.
- **Dzienniki śledzenia**: pulpitu zdalnego do maszyny Wirtualnej i Dodaj TextWriterTraceListener do pliku config aplikacji.  Zobacz http://msdn.microsoft.com/library/sk36c28t.aspx do skonfiguruj odbiornik tekstu.  Upewnij się, że `<trace>` element ma `<trace autoflush="true">`.<br />
Jeśli nie widzisz generowanych dzienniki śledzenia, należy wykonać [więcej o śledzenia dzienniki Brak](#more-about-trace-logs-missing).
- **Ślady ETW**: pulpitu zdalnego do maszyny Wirtualnej i zainstaluj narzędzia PerfView.  W narzędzia PerfView uruchamiany plik -> polecenia User -> etwprovder1 nasłuchiwania, etwprovider2 itp.  Należy pamiętać, że polecenia nasłuchiwania jest rozróżniana wielkość liter i nie może być spacji między rozdzielana przecinkami lista dostawców ETW.  Polecenie nie powiedzie się do uruchomienia, po kliknięciu przycisku "Dziennik" w prawym dolnym rogu narzędzia narzędzia Perfview, co zostało próbował uruchomić i wynik był.  Zakładając, że dane wejściowe są poprawne, następnie nowe okno będzie pop w górę i w ciągu kilku sekund zostanie rozpoczęta wyświetlanie śladów ETW.
- **Dzienniki zdarzeń**: pulpitu zdalnego do maszyny Wirtualnej. Otwórz `Event Viewer` i upewnij się, istnieje zdarzenia.
#### <a name="is-data-getting-captured-locally"></a>Dane pobierania przechwytywania lokalnie:
Następnie upewnij się, że pierwsze lokalnie przechwyceniu danych.
Dane lokalne są przechowywane w `*.tsf` plików [lokalnego magazynu dla danych diagnostycznych](#log-artifacts-path). Różne rodzaje dzienniki uzyskać zebrane w różnych `.tsf` plików. Nazwy są podobne do nazwy tabeli w magazynie azure. Na przykład `Performance Counters` uzyskać zbierane w `PerformanceCountersTable.tsf`, dzienniki zdarzeń uzyskać zebrane w `WindowsEventLogsTable.tsf`. Postępuj zgodnie z instrukcjami w [lokalnego wyodrębniania dziennika](#local-log-extraction) sekcji, aby otworzyć pliki kolekcji lokalnej i upewnij się, że ich wprowadzenie zebrane na dysku.

Jeśli nie widzisz dzienników pobierania zebranych lokalnie i już sprawdzeniu, że host jest generowania danych, prawdopodobnie jest problem z konfiguracją. Zapoznaj się uważnie odpowiedniej sekcji konfiguracji. Również przejrzeć konfigurację wygenerowany dla MonitoringAgent [MaConfig.xml](#log-artifacts-path) i upewnij się, że ma niektórych części opisu źródła odpowiednich dziennika oraz że nie zostaną utracone w tłumaczeniu między konfiguracji diagnostyki azure i Konfiguracja agenta monitorowania.
#### <a name="is-data-getting-transferred"></a>Jest przekazywane pobierania danych:
Jeśli po sprawdzeniu danych jest pierwsze przechwycone lokalnie, ale nadal nie widać na koncie magazynu: 
- Najpierw i, upewnij się, podane konto magazynu poprawne i że użytkownik ma nie przerzuceniem etc.for klucze konta magazynu podanego. Dla usług w chmurze, czasami widzimy, że osoby nie aktualizuj ich `useDevelopmentStorage=true`.
- Jeśli pod warunkiem, że konto magazynu jest poprawna. Upewnij się, że nie ma pewne ograniczenia sieci, które nie zezwalają na składniki do osiągnięcia magazynu publicznych punktów końcowych. Jednym ze sposobów to zrobić ma pulpitu zdalnego do maszyny i spróbuj Napisz coś do tego samego konta magazynu samodzielnie.
- Na koniec można spróbuj i zobacz, jakie niepowodzenia są zgłaszane przez agenta monitorowania. Agent monitorowania zapisuje dzienniki jej `maeventtable.tsf` znajduje się w [lokalnego magazynu dla danych diagnostycznych](#log-artifacts-path). Postępuj zgodnie z instrukcjami wyświetlanymi w [lokalnego wyodrębniania dziennika](#local-log-extraction) sekcji, aby otworzyć ten plik i spróbuj i ustalić, czy istnieją `errors` wskazujące na awarie do odczytu plików lokalnych lub zapisu w magazynie.

### <a name="capturing--archiving-logs"></a>Przechwytywanie / archiwizowanie dzienników
Wykonano kroki powyższe kroki, ale nie można dowiedzieć się, co jest nieprawidłowa i są myślenia o skontaktowaniu się z pomocą techniczną. W pierwszej kolejności pracownik może poprosić o jest zbieranie dzienników z komputera. Wykonując tego użytkownika, można zaoszczędzić czas. Uruchom `CollectGuestLogs.exe` narzędzia na [ścieżkę dostępu do dziennika narzędzia kolekcji](#log-artifacts-path) i generuje plik zip ze wszystkich odpowiednich dzienników azure w tym samym folderze.

## <a name="diagnostics-data-tables-not-found"></a>Dane diagnostyczne nie znaleziono tabel
Tabel w magazynie Azure zawierający zdarzenia ETW są nazywane, używając następującego kodu:

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

### <a name="how-to-check-diagnostics-extension-configuration"></a>Sprawdzanie konfiguracji rozszerzenia diagnostyki
Najprostszym sposobem, aby sprawdzić konfigurację rozszerzenia przejdź do http://resources.azure.com, przejdź do maszyny wirtualnej lub usługi w chmurze na którym rozszerzenie Azure Diagnostics (IaaSDiagnostics / PaaDiagnostics) jest zagrożona.

Alternatywnie pulpitu zdalnego do maszyny i znajduje się w pliku konfiguracji diagnostyki Azure opisane w odpowiedniej sekcji [tutaj](#log-artifacts-path).

W przypadku wyszukać **Microsoft.Azure.Diagnostics** następnie dla **xmlCfg** lub **WadCfg** pola. 

W przypadku maszyn wirtualnych Jeśli pole WadCfg jest obecny, oznacza to, że konfiguracji jest w formacie JSON. Jeśli pole xmlCfg jest obecny, oznacza to, konfiguracji jest w formacie XML i jest kodowany w formacie base64. Musisz [zdekodować](http://www.bing.com/search?q=base64+decoder) aby zobaczyć plik XML, który został załadowany przez diagnostyki.

Dla roli usługi w chmurze, w przypadku wybrania konfiguracji z dysku, dane są kodowanie base64, konieczne będzie [zdekodować](http://www.bing.com/search?q=base64+decoder) aby zobaczyć plik XML, który został załadowany przez diagnostyki.

### <a name="azure-diagnostics-plugin-exit-codes"></a>Kody zakończenia wtyczki Diagnostyka Azure
Wtyczka zwraca następujący kod zakończenia:

| Kod zakończenia | Opis |
| --- | --- |
| 0 |Powodzenie. |
| -1 |Błąd rodzajowy. |
| -2 |Nie można załadować pliku rcf.<p>Ten błąd wewnętrzny tylko powinien nastąpić, jeśli niepoprawnie, uruchamiania wtyczki agenta gościa ręcznie jest wywoływana na maszynie Wirtualnej. |
| -3 |Nie można załadować pliku konfiguracji diagnostyki.<p><p>Rozwiązanie: Spowodowane nie przeszły sprawdzanie poprawności schematu pliku konfiguracji. Rozwiązanie jest zapewnienie pliku konfiguracji, który jest zgodny ze schematem. |
| -4 |Inne wystąpienie agenta monitorowania diagnostyki już używa zasobu lokalnego katalogu.<p><p>Rozwiązanie: Określ inną wartość dla **LocalResourceDirectory**. |
| -6 |Uruchamianie wtyczki agenta gościa próba uruchomienie diagnostyki z nieprawidłowy wiersz polecenia.<p><p>Ten błąd wewnętrzny tylko powinien nastąpić, jeśli niepoprawnie, uruchamiania wtyczki agenta gościa ręcznie jest wywoływana na maszynie Wirtualnej. |
| -10 |Wtyczki diagnostyki został zakończony z powodu nieobsługiwanego wyjątku. |
| -11 |Agent gościa nie może utworzyć procesu odpowiedzialnego za uruchamianie i monitorowanie agenta monitorowania.<p><p>Rozwiązanie: Sprawdź, czy wystarczające zasoby systemowe są dostępne na uruchomienie nowych procesów.<p> |
| -101 |Nieprawidłowe argumenty podczas wywoływania metody wtyczki diagnostyki.<p><p>Ten błąd wewnętrzny tylko powinien nastąpić, jeśli niepoprawnie, uruchamiania wtyczki agenta gościa ręcznie jest wywoływana na maszynie Wirtualnej. |
| -102 |Proces wtyczki nie jest w stanie się zainicjować.<p><p>Rozwiązanie: Sprawdź, czy wystarczające zasoby systemowe są dostępne na uruchomienie nowych procesów. |
| -103 |Proces wtyczki nie jest w stanie się zainicjować. W szczególności jest nie można utworzyć obiektu rejestratora.<p><p>Rozwiązanie: Sprawdź, czy wystarczające zasoby systemowe są dostępne na uruchomienie nowych procesów. |
| -104 |Nie można załadować pliku rcf dostarczonej przez agenta gościa.<p><p>Ten błąd wewnętrzny tylko powinien nastąpić, jeśli niepoprawnie, uruchamiania wtyczki agenta gościa ręcznie jest wywoływana na maszynie Wirtualnej. |
| -105 |Dodatek diagnostyki nie można otworzyć pliku konfiguracji diagnostyki.<p><p>Ten błąd wewnętrzny tylko powinien nastąpić, jeśli niepoprawnie, wtyczki diagnostyki ręcznie jest wywoływana na maszynie Wirtualnej. |
| -106 |Nie można odczytać pliku konfiguracji diagnostyki.<p><p>Rozwiązanie: Spowodowane nie przeszły sprawdzanie poprawności schematu pliku konfiguracji. Dlatego rozwiązania ma na celu dostarczenie pliku konfiguracji, który jest zgodny ze schematem. Zobacz [Sprawdzanie konfiguracji rozszerzenia diagnostyki](#how-to-check-diagnostics-extension-configuration). |
| -107 |Do agenta monitorowania przebiegu katalogu zasobu jest nieprawidłowy.<p><p>Ten błąd wewnętrzny tylko powinno się zdarzyć, jeśli niepoprawnie, agent monitorowania ręcznie jest wywoływana na maszynie Wirtualnej.</p> |
| -108 |Nie można przekonwertować pliku konfiguracji diagnostyki w pliku konfiguracji agenta monitorowania.<p><p>Ten błąd wewnętrzny tylko powinno się zdarzyć, jeśli wtyczka diagnostyki ręcznie została wywołana z nieprawidłowy plik konfiguracji. |
| -110 |Błąd konfiguracji diagnostyki ogólne.<p><p>Ten błąd wewnętrzny tylko powinno się zdarzyć, jeśli wtyczka diagnostyki ręcznie została wywołana z nieprawidłowy plik konfiguracji. |
| -111 |Nie można uruchomić agenta monitorowania.<p><p>Rozwiązanie: Sprawdź, czy dostępne są wystarczające zasoby systemu. |
| -112 |Błąd ogólny |

### <a name="local-log-extraction"></a>Wyodrębnianie lokalnym dzienniku
Agent monitorowania zbiera dzienniki i artefaktów jak `.tsf` plików. `.tsf`plik nie jest do odczytu, ale można przekonwertować go do `.csv` w następujący sposób: 

```
<Azure diagnostics extension package>\Monitor\x64\table2csv.exe <relevantLogFile>.tsf
```
Nowy plik o nazwie `<relevantLogFile>.csv` zostaną utworzone w tej samej ścieżce jako odpowiednie `.tsf` pliku.

**Uwaga**: musisz uruchomić to narzędzie przed tsf głównego pliku (np. PerformanceCountersTable.tsf). Załączonych plików (np. PerformanceCountersTables_\*\*001.tsf, PerformanceCountersTables_\*\*tsf 002. itp.) zostaną automatycznie przetworzone.

### <a name="more-about-trace-logs-missing"></a>Więcej informacji na temat Brak dzienniki śledzenia

**Uwaga:** najczęściej dotyczy to usługi w chmurze tylko, jeśli nie skonfigurowano DiagnosticsMonitorTraceListener na aplikacji działających na maszynie Wirtualnej IaaS. 

- Upewnij się, że DiagnosticMonitorTraceListener jest skonfigurowany w pliku web.config lub app.config.  Jest to konfiguracja domyślna w projekty usługi w chmurze, ale niektórzy klienci komentarz dotyczący, się, które spowoduje instrukcji śledzenia do nie zostać zebrane przez diagnostyki. 
- Jeśli nie pobierania dziennikach z metody OnStart lub uruchom upewnij się, że DiagnosticMonitorTraceListener znajduje się w pliku app.config.  Domyślnie jest on w pliku web.config, ale dotyczą tylko kodu uruchamianego w w3wp.exe; Dlatego należy go w pliku app.config do przechwytywania danych śledzenia w WaIISHost.exe.
- Upewnij się, że używasz Diagnostics.Trace.TraceXXX zamiast Diagnostics.Debug.WriteXXX.  Debugować instrukcje zostaną usunięte z kompilacji wydania.
- Upewnij się, że skompilowanego kodu faktycznie zawiera wiersze Diagnostics.Trace (Użyj reflektor, narzędzia ildasm lub ILSpy, aby sprawdzić).  Polecenia Diagnostics.Trace są usuwane z skompilowanym plikiem binarnym, chyba że używany jest symbol kompilacji warunkowej śledzenia.  Jeśli przy użyciu programu msbuild, aby skompilować projekt to powszechny problem do wykonania.

## <a name="known-issues-and-mitigations"></a>Znane problemy i środki zaradcze
Poniżej przedstawiono listę znanych problemów z znane środki zaradcze:

**1. .NET 4.5 zależności:**

WAD ma zależności aparatu plików wykonywalnych w ramach platformy .NET 4.5 lub nowszym. W czasie zapisywania to wszystkie maszyny obsługi administracyjnej dla usługi w chmurze, a także wszystkie oficjalnego azure obrazy maszyny wirtualnej podstawowej mieć .NET 4.5 powyżej zainstalowany lub. Nadal jest jednak możliwe przejście w sytuacji, gdy zostanie podjęta próba uruchomienia WAD, na komputerze, który nie ma .NET 4.5 lub nowszy. Dzieje się tak podczas tworzenia komputera poza stary obraz lub migawki; lub przenieść niestandardowego dysku.

Zazwyczaj jest to manifesty jako kod zakończenia **255** podczas uruchamiania DiagnosticsPluginLauncher.exe. Błąd odbywa się z powodu nieobsługiwanego wyjątku: 
```
System.IO.FileLoadException: Could not load file or assembly 'System.Threading.Tasks, Version=1.5.11.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies
```

**Ograniczenie:** instalacji platformy .NET 4.5 lub nowszej na tym komputerze.

**2. Dostępne w magazynu, ale nie są wyświetlane w portalu danych liczników wydajności**

Maszyny wirtualne środowisko portalu przedstawia niektóre liczniki wydajności domyślnie. Jeśli nie są one wyświetlane i wiesz, że dane jest generowanych, ponieważ jest ona dostępna w magazynie. Sprawdzanie:
- Jeśli w magazynie danych nazwy licznika w języku angielskim. Jeśli nazwy liczników nie są w języku angielskim, portalu metryki wykresu nie będzie można go rozpoznać.
- Jeśli używane są symbole wieloznaczne (\*) w Twojej nazwy licznika wydajności portalu nie będzie służące do skorelowania skonfigurowane i zebranych liczników.

**Środki zaradcze**: zmiana języka na komputerze język angielski dla konta system. Region -> Panel sterowania -> administracyjne -> Ustawienia kopiowania -> Usuń zaznaczenie pola wyboru "Zapraszamy ekranu i systemu kont", aby języka niestandardowej nie ma zastosowania do konta systemu. Upewnij się, że nie należy używać symbole wieloznaczne, jeśli ma portalu, aby być środowiska głównej zużycia.
