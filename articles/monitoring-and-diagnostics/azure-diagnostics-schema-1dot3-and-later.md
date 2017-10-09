---
title: "Schemat konfiguracji 1.3 i późniejsze rozszerzenia diagnostyki aaaAzure | Dokumentacja firmy Microsoft"
description: "Wersja schematu 1.3 i nowszym diagnostyki Azure dostarczana jako część programu hello Microsoft Azure SDK 2.4 lub nowszy."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: robb
ms.openlocfilehash: bd15d3a79ea818fcb3235854717e58d5da36518e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a>1.3 diagnostyki Azure i nowszym schemat konfiguracji
> [!NOTE]
> Hello rozszerzenie Azure Diagnostics jest składnik hello używany toocollect liczniki wydajności i innych danych statystycznych z:
> - Azure Virtual Machines 
> - Zestawy skali maszyn wirtualnych
> - Service Fabric 
> - Cloud Services 
> - Grupy zabezpieczeń sieci
> 
> Ta strona jest tylko istotne, jeśli używasz tych usług.

Ta strona jest nieprawidłowa dla wersji 1.3 i nowsze (Azure SDK 2.4 i nowszych). Nowsze sekcji konfiguracji są tooshow komentarze, w jakiej wersji zostały one dodane.  

Plik konfiguracyjny Hello opisane w tym miejscu jest tooset używanych ustawień diagnostycznych konfiguracji rozpoczyna monitorowanie hello diagnostyki.  

rozszerzenie Hello jest używany w połączeniu z innymi produktami firmy Microsoft diagnostyki, takich jak Azure monitora, usługi Application Insights i analizy dzienników.



Pobierz definicję schematu pliku konfiguracji publicznego hello, wykonując następujące polecenia programu PowerShell hello:  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

Aby uzyskać więcej informacji o korzystaniu z diagnostyki Azure, zobacz [rozszerzenia diagnostyki Azure](azure-diagnostics.md).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Przykładowy plik konfiguracji diagnostyki hello  
 Hello poniższy przykład przedstawia plik diagnostyki typowych konfiguracji:  

```xml  
<?xml version="1.0" encoding="utf-8"?>  
<DiagnosticsConfiguration  xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">   
  <PublicConfig>  
    <WadCfg>  
      <DiagnosticMonitorConfiguration overallQuotaInMB="10000">  

        <PerformanceCounters scheduledTransferPeriod="PT1M">  
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />  
        </PerformanceCounters>  

        <Directories scheduledTransferPeriod="PT5M">  
          <IISLogs containerName="iislogs" />  
          <FailedRequestLogs containerName="iisfailed" />  

          <DataSources>  
            <DirectoryConfiguration containerName="mynewprocess">  
              <Absolute path="C:\MyNewProcess" expandEnvironment="false" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="badapp">  
              <Absolute path="%SYSTEMDRIVE%\BadApp" expandEnvironment="true" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="goodapp">  
              <LocalResource name="Skippy" relativePath="..\PeanutButter"/>  
            </DirectoryConfiguration>  
          </DataSources>  

        </Directories>  

        <EtwProviders>  
          <EtwEventSourceProviderConfiguration   
                       provider="MyProviderClass"   
                       scheduledTransferPeriod="PT5M">  
            <Event id="0"/>  
            <Event id="1" eventDestination="errorTable"/>  
            <DefaultEvents />  
          </EtwEventSourceProviderConfiguration>  
          <EtwManifestProviderConfiguration provider="5974b00b-84c2-44bc-9e58-3a2451b4e3ad" scheduledTransferLogLevelFilter="Information" scheduledTransferPeriod="PT2M">  
            <Event id="0"/>  
            <DefaultEvents eventDestination="defaultTable"/>  
          </EtwManifestProviderConfiguration>  
        </EtwProviders>  

        <WindowsEventLog scheduledTransferPeriod="PT5M">  
          <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>  
          <DataSource name="System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]" />  
          <DataSource name="System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]" />  
        </WindowsEventLog>  

        <Logs  bufferQuotaInMB="1024"   
             scheduledTransferPeriod="PT1M"   
             scheduledTransferLogLevelFilter="Verbose"   
             sinks="ApplicationInsights.AppLogs"/>  <!-- sinks attribute added in 1.5 -->  

        <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
          <CrashDumpConfiguration processName="mynewprocess.exe" />  
          <CrashDumpConfiguration processName="badapp.exe"/>  
        </CrashDumps>  

        <DockerSources> <!-- Added in 1.9 --> 
          <Stats enabled="true" sampleRate="PT1M" scheduledTransferPeriod="PT1M" />
        </DockerSources>

      </DiagnosticMonitorConfiguration>  

      <SinksConfig>   <!-- Added in 1.5 -->  
        <Sink name="ApplicationInsights">   
          <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>   
          <Channels>   
            <Channel logLevel="Error" name="Errors"  />   
            <Channel logLevel="Verbose" name="AppLogs"  />   
          </Channels>   
        </Sink>   
        <Sink name="EventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryEventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryStorageAccount"> <!-- Added in 1.7 -->
          <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" />
        </Sink>
   </SinksConfig>

  </WadCfg>  

  <StorageAccount>diagstorageaccount</StorageAccount>
  <StorageType>TableAndBlob</StorageType> <!-- Added in 1.8 -->  
  </PublicConfig>  

  <PrivateConfig>  <!-- Added in 1.3 -->  
    <StorageAccount name="" key="" endpoint="" sasToken="{sas token}"  />  <!-- sasToken in Private config added in 1.8.1 -->  
    <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
   
    <SecondaryStorageAccounts>
       <StorageAccount name="secondarydiagstorageaccount" key="{base64 encoded key}" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
   
    <SecondaryEventHubs>
       <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
    </SecondaryEventHubs>

  </PrivateConfig>  
  <IsEnabled>true</IsEnabled>  
</DiagnosticsConfiguration>  

```  

Odpowiednik JSON hello poprzedniego pliku konfiguracyjnego XML. 

Hello PublicConfig i PrivateConfig są rozdzielone, ponieważ w większości przypadków użycia json, są przekazywane jako różne zmienne. Tych przypadkach obejmują szablony Menedżera zasobów, zestawu skalowania maszyn wirtualnych programu PowerShell i programu Visual Studio. 

```json
"PublicConfig" {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 10000,
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT1M",
                        "unit": "percent"
                    }
                ]
            },
            "Directories": {
                "scheduledTransferPeriod": "PT5M",
                "IISLogs": {
                    "containerName": "iislogs"
                },
                "FailedRequestLogs": {
                    "containerName": "iisfailed"
                },
                "DataSources": [
                    {
                        "containerName": "mynewprocess",
                        "Absolute": {
                            "path": "C:\\MyNewProcess",
                            "expandEnvironment": false
                        }
                    },
                    {
                        "containerName": "badapp",
                        "Absolute": {
                            "path": "%SYSTEMDRIVE%\\BadApp",
                            "expandEnvironment": true
                        }
                    },
                    {
                        "containerName": "goodapp",
                        "LocalResource": {
                            "relativePath": "..\\PeanutButter",
                            "name": "Skippy"
                        }
                    }
                ]
            },
            "EtwProviders": {
                "sinks": "",
                "EtwEventSourceProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT5M",
                        "provider": "MyProviderClass",
                        "Event": [
                            {
                                "id": 0
                            },
                            {
                                "id": 1,
                                "eventDestination": "errorTable"
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ],
                "EtwManifestProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT2M",
                        "scheduledTransferLogLevelFilter": "Information",
                        "provider": "5974b00b-84c2-44bc-9e58-3a2451b4e3ad",
                        "Event": [
                            {
                                "id": 0
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT5M",
                "DataSource": [
                    {
                        "name": "System!*[System[Provider[@Name='Microsoft Antimalware']]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Verbose",
                "sinks": "ApplicationInsights.AppLogs"
            },
            "CrashDumps": {
                "directoryQuotaPercentage": 30,
                "dumpType": "Mini",
                "containerName": "wad-crashdumps",
                "CrashDumpConfiguration": [
                    {
                        "processName": "mynewprocess.exe"
                    },
                    {
                        "processName": "badapp.exe"
                    }
                ]
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "ApplicationInsights",
                    "ApplicationInsights": "{Insert InstrumentationKey}",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "Errors"
                            },
                            {
                                "logLevel": "Verbose",
                                "name": "AppLogs"
                            }
                        ]
                    }
                },
                {
                    "name": "EventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryEventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryStorageAccount",
                    "StorageAccount": {
                        "name": "secondarydiagstorageaccount",
                        "endpoint": "https://core.windows.net"
                    }
                }
            ]
        }
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```json
"PrivateConfig" {
    "storageAccountName": "diagstorageaccount",
    "storageAccountKey": "{base64 encoded key}",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "EventHub": {
        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    },
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "key": "{base64 encoded key}",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    },
    "SecondaryEventHubs": {
        "EventHub": [
            {
                "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                "SharedAccessKeyName": "SendRule",
                "SharedAccessKey": "{base64 encoded key}"
            }
        ]
    }
}

```

## <a name="reading-this-page"></a>Odczytywanie tej strony  
 Hello tagi po są mniej więcej w kolejności przedstawionej w hello poprzedzających przykład.  Jeśli widzisz pełny opis, których można oczekiwać, wyszukaj strony hello hello elementu lub atrybutu.  

## <a name="common-attribute-types"></a>Popularne typy atrybutów  
 **scheduledTransferPeriod** atrybutu pojawia się w kilku elementów. Jest hello odstęp między toostorage zaplanowane transferów zaokrąglona w górę toohello najbliższej minutę. wartość Hello jest [XML "Typ danych Duration."](http://www.w3schools.com/schema/schema_dtypes_date.asp)


## <a name="diagnosticsconfiguration-element"></a>DiagnosticsConfiguration Element  
 *Drzewa: Główny - DiagnosticsConfiguration*

Dodany w wersji 1.3.  

element najwyższego poziomu Hello pliku konfiguracyjnego hello diagnostyki.  

**Atrybut** xmlns — Witaj przestrzeni nazw XML dla pliku konfiguracji diagnostyki hello jest:  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  


|Elementy podrzędne|Opis|  
|--------------------|-----------------|  
|**PublicConfig**|Wymagany. Zobacz opis w innym miejscu na tej stronie.|  
|**PrivateConfig**|Opcjonalny. Zobacz opis w innym miejscu na tej stronie.|  
|**IsEnabled**|Wartość logiczna. Zobacz opis w innym miejscu na tej stronie.|  

## <a name="publicconfig-element"></a>PublicConfig Element  
 *Drzewa: PublicConfig - DiagnosticsConfiguration - katalogu głównego*

 W tym artykule opisano hello diagnostyki publicznego konfiguracji.  

|Elementy podrzędne|Opis|  
|--------------------|-----------------|  
|**WadCfg**|Wymagany. Zobacz opis w innym miejscu na tej stronie.|  
|**Konto magazynu**|Nazwa Hello danych konta usługi Azure Storage hello hello toostore w. Można także określić jako parametr podczas wykonywania polecenia cmdlet hello AzureServiceDiagnosticsExtension zestawu.|  
|**StorageType**|Może być *tabeli*, *obiektu Blob*, lub *TableAndBlob*. Tabela jest domyślny. Po wybraniu TableAndBlob danych diagnostycznych są zapisywane dwukrotnie — raz tooeach typu.|  
|**LocalResourceDirectory**|katalog Hello na maszynie wirtualnej hello której hello agenta monitorowania przechowuje dane zdarzenia. Jeśli nie ustawiono, używane jest hello domyślny katalog:<br /><br /> Dla roli proces roboczy/sieci web:`C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> Dla maszyny wirtualnej:`C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> Atrybuty wymagane są:<br /><br /> - **ścieżka** — Witaj katalogu na powitania toobe systemu używany przez diagnostyki Azure.<br /><br /> - **expandEnvironment** — Określa, czy w nazwie ścieżki hello są rozwinięte zmiennych środowiskowych.|  

## <a name="wadcfg-element"></a>WadCFG Element  
 *Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG katalogu głównego*
 
 Identyfikuje i konfiguruje toobe danych telemetrycznych hello zbierane.  


## <a name="diagnosticmonitorconfiguration-element"></a>DiagnosticMonitorConfiguration Element 
 *Drzewa: DiagnosticMonitorConfiguration PublicConfig - WadCFG - głównego - DiagnosticsConfiguration-*

 Wymagane 

|Atrybuty|Opis|  
|----------------|-----------------|  
| **overallQuotaInMB** | Maksymalna ilość miejsca na dysku lokalnym, które może być zużyte przez hello Hello różnego typu dane diagnostyczne zebrane przez diagnostyki Azure. Witaj domyślne ustawienie to 5120 MB.<br />
|**useProxyServer** | Skonfiguruj ustawienia serwera proxy hello toouse diagnostyki Azure zgodnie z ustawieniami w ustawieniach programu Internet Explorer.|  

<br /> <br />

|Elementy podrzędne|Opis|  
|--------------------|-----------------|  
|**Zrzutów awaryjnych**|Zobacz opis w innym miejscu na tej stronie.|  
|**DiagnosticInfrastructureLogs**|Włącz zbieranie dzienników generowanych przez diagnostyki Azure. dzienniki diagnostyczne infrastruktury Hello są przydatne podczas rozwiązywania problemów sam system diagnostyki hello. Opcjonalne atrybuty:<br /><br /> - **scheduledTransferLogLevelFilter** — konfiguruje hello minimalny poziom ważności dzienników hello zbierane.<br /><br /> - **scheduledTransferPeriod** — interwał powitania między toostorage zaplanowane transferów zaokrąglona w górę toohello najbliższej minutę. wartość Hello jest [XML "Typ danych Duration."](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**Katalogi**|Zobacz opis w innym miejscu na tej stronie.|  
|**EtwProviders**|Zobacz opis w innym miejscu na tej stronie.|  
|**Metryki**|Zobacz opis w innym miejscu na tej stronie.|  
|**Liczniki wydajności**|Zobacz opis w innym miejscu na tej stronie.|  
|**WindowsEventLog**|Zobacz opis w innym miejscu na tej stronie.| 
|**DockerSources**|Zobacz opis w innym miejscu na tej stronie. | 



## <a name="crashdumps-element"></a>Element zrzutów awaryjnych  
 *Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - zrzutów awaryjnych w katalogu głównego*
 
 Włącz kolekcję hello zrzuty awaryjne.  

|Atrybuty|Opis|  
|----------------|-----------------|  
|**Właściwość containerName**|Opcjonalny. zrzuty awaryjne toostore używana nazwa Hello hello kontenera obiektów blob w toobe konta użytkownika usługi Azure Storage.|  
|**crashDumpType**|Opcjonalny.  Konfiguruje zrzuty awaryjne mini lub pełnego toocollect diagnostyki Azure.|  
|**directoryQuotaPercentage**|Opcjonalny.  Umożliwia skonfigurowanie wartości procentowej hello **overallQuotaInMB** toobe zarezerwowane zrzuty awaryjne na powitania maszyny Wirtualnej.|  

|Elementy podrzędne|Opis|  
|--------------------|-----------------|  
|**CrashDumpConfiguration**|Wymagany. Definiuje wartości konfiguracji dla każdego procesu.<br /><br /> wymagane jest również Hello następującego atrybutu:<br /><br /> **Parametr** — Witaj nazwa procesu hello ma toocollect diagnostyki Azure dla zrzutu awaryjnego.|  

## <a name="directories-element"></a>Element katalogów 
 *Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - katalogów katalogu głównego*

 Umożliwia hello kolekcji hello zawartości katalogu, usługi IIS nie powiodło się, dzienniki żądania dostępu i/lub dzienniki programu IIS.  

 Opcjonalne **scheduledTransferPeriod** atrybutu. Zawiera wyjaśnienie wcześniej.  

|Elementy podrzędne|Opis|  
|--------------------|-----------------|  
|**IISLogs**|W tym ten element w konfiguracji hello umożliwia hello zbieranie dzienników usług IIS:<br /><br /> **Właściwość containerName** — dzienniki programu IIS hello toostore używana nazwa hello hello kontenera obiektów blob w toobe konta użytkownika usługi Azure Storage.|   
|**FailedRequestLogs**|W tym ten element w konfiguracji hello umożliwia zbieranie dzienników dotyczące żądań zakończonych niepowodzeniem tooan IIS witryny lub aplikacji. Należy też włączyć śledzenie opcje w obszarze **systemu. Serwer sieci Web** w **Web.config**.|  
|**Źródła danych**|Lista katalogów toomonitor.| 




## <a name="datasources-element"></a>Element źródeł danych  
 *Drzewa: Źródła danych PublicConfig - WadCFG - DiagnosticMonitorConfiguration - katalogów - głównego - DiagnosticsConfiguration-*

 Lista katalogów toomonitor.  

|Elementy podrzędne|Opis|  
|--------------------|-----------------|  
|**DirectoryConfiguration**|Wymagany. Wymagany atrybut:<br /><br /> **Właściwość containerName** — Witaj nazwa hello kontenera obiektów blob na koncie magazynu Azure, w tym toobe używane pliki dziennika hello toostore.|  





## <a name="directoryconfiguration-element"></a>DirectoryConfiguration Element  
 *Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - katalogów - DataSources — DirectoryConfiguration katalogu głównego*

 Mogą one obejmować albo hello **bezwzględną** lub **LocalResource** elementu, ale nie oba.  

|Elementy podrzędne|Opis|  
|--------------------|-----------------|  
|**Bezwzględne**|Witaj toomonitor katalogu toohello ścieżkę bezwzględną. Witaj następujące atrybuty są wymagane:<br /><br /> - **Ścieżka** — Witaj toomonitor katalogu toohello ścieżkę bezwzględną.<br /><br /> - **expandEnvironment** — Określa, czy są rozwinięte zmiennych środowiskowych w ścieżce.|  
|**LocalResource**|Witaj toomonitor zasobu lokalnego tooa względną ścieżkę. Atrybuty wymagane są:<br /><br /> - **Nazwa** — Witaj zasób lokalny, który zawiera toomonitor katalogu hello<br /><br /> - **relativePath** — Witaj tooName względną ścieżkę zawierającą hello toomonitor katalogu|  



## <a name="etwproviders-element"></a>EtwProviders Element  
 *Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders katalogu głównego*

 Zbieranie zdarzeń ETW z EventSource konfiguruje i/lub ETW manifestu na podstawie dostawców.  

|Elementy podrzędne|Opis|  
|--------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|Konfiguruje zbierania zdarzeń generowanych przez [EventSource — klasa](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Wymagany atrybut:<br /><br /> **Dostawca** — Nazwa klasy hello hello EventSource zdarzenia.<br /><br /> Opcjonalne atrybuty:<br /><br /> - **scheduledTransferLogLevelFilter** — Witaj konta magazynu tooyour tootransfer poziomu ważności minimalnej.<br /><br /> - **scheduledTransferPeriod** — interwał powitania między toostorage zaplanowane transferów zaokrąglona w górę toohello najbliższej minutę. wartość Hello jest [XML "Typ danych Duration."](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**EtwManifestProviderConfiguration**|Wymagany atrybut:<br /><br /> **Dostawca** — Witaj GUID hello Dostawca zdarzeń<br /><br /> Opcjonalne atrybuty:<br /><br /> - **scheduledTransferLogLevelFilter** — Witaj konta magazynu tooyour tootransfer poziomu ważności minimalnej.<br /><br /> - **scheduledTransferPeriod** — interwał powitania między toostorage zaplanowane transferów zaokrąglona w górę toohello najbliższej minutę. wartość Hello jest [XML "Typ danych Duration."](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="etweventsourceproviderconfiguration-element"></a>EtwEventSourceProviderConfiguration Element  
 *Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwEventSourceProviderConfiguration katalogu głównego*

 Konfiguruje zbierania zdarzeń generowanych przez [EventSource — klasa](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).  

|Elementy podrzędne|Opis|  
|--------------------|-----------------|  
|**DefaultEvents**|Atrybut opcjonalny:<br/><br/> **eventDestination** — Witaj nazwa hello tabeli toostore hello zdarzeń w|  
|**Zdarzenie**|Wymagany atrybut:<br /><br /> **Identyfikator** — identyfikator hello hello zdarzenia.<br /><br /> Atrybut opcjonalny:<br /><br /> **eventDestination** — Witaj nazwa hello tabeli toostore hello zdarzeń w|  



## <a name="etwmanifestproviderconfiguration-element"></a>EtwManifestProviderConfiguration Element  
 *Drzewa: EtwManifestProviderConfiguration PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - głównego - DiagnosticsConfiguration-*

|Elementy podrzędne|Opis|  
|--------------------|-----------------|  
|**DefaultEvents**|Atrybut opcjonalny:<br /><br /> **eventDestination** — Witaj nazwa hello tabeli toostore hello zdarzeń w|  
|**Zdarzenie**|Wymagany atrybut:<br /><br /> **Identyfikator** — identyfikator hello hello zdarzenia.<br /><br /> Atrybut opcjonalny:<br /><br /> **eventDestination** — Witaj nazwa hello tabeli toostore hello zdarzeń w|  



## <a name="metrics-element"></a>Element metryk  
 *Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - metryki katalogu głównego*

 Umożliwia toogenerate tabeli licznika wydajności, która jest zoptymalizowana pod kątem szybkiego zapytania. Każdego licznika wydajności, który jest zdefiniowany w hello **liczniki wydajności** elementu są przechowywane w tabeli metryki hello tabeli dodanie toohello licznika wydajności.  

 Witaj **resourceId** atrybut jest wymagany.  Identyfikator zasobu Hello hello wdrażasz diagnostyki Azure do maszyny wirtualnej. Pobierz hello **resourceID** z hello [portalu Azure](https://portal.azure.com). Wybierz **Przeglądaj** -> **grup zasobów** -> **< nazwa\>**. Kliknij przycisk hello **właściwości** Kafelek i skopiuj wartość hello z hello **identyfikator** pola.  

|Elementy podrzędne|Opis|  
|--------------------|-----------------|  
|**MetricAggregation**|Wymagany atrybut:<br /><br /> **scheduledTransferPeriod** — interwał powitania między toostorage zaplanowane transferów zaokrąglona w górę toohello najbliższej minutę. wartość Hello jest [XML "Typ danych Duration."](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="performancecounters-element"></a>PerformanceCounters — Element  
 *Drzewa: DiagnosticMonitorConfiguration PublicConfig - WadCFG - głównego - DiagnosticsConfiguration - - liczniki wydajności*

 Umożliwia zbieranie hello liczników wydajności.  

 Atrybut opcjonalny:  

 Opcjonalne **scheduledTransferPeriod** atrybutu. Zawiera wyjaśnienie wcześniej.

|Element podrzędny|Opis|  
|-------------------|-----------------|  
|**PerformanceCounterConfiguration**|Witaj następujące atrybuty są wymagane:<br /><br /> - **counterSpecifier** — Witaj nazwa hello licznika wydajności. Na przykład `\Processor(_Total)\% Processor Time`. tooget listę wydajności liczniki na hoście, uruchom polecenie hello `typeperf`.<br /><br /> - **sampleRate** -częstotliwość hello licznika powinny być pobrane.<br /><br /> Atrybut opcjonalny:<br /><br /> **Jednostka** -hello jednostka miary hello licznika.|  




## <a name="windowseventlog-element"></a>WindowsEventLog Element
 *Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog katalogu głównego*
 
 Umożliwia zbieranie hello dzienniki zdarzeń systemu Windows.  

 Opcjonalne **scheduledTransferPeriod** atrybutu. Zawiera wyjaśnienie wcześniej.  

|Element podrzędny|Opis|  
|-------------------|-----------------|  
|**Źródło danych**|Witaj toocollect dzienniki zdarzeń systemu Windows. Wymagany atrybut:<br /><br /> **Nazwa** -Kwerenda XPath hello opisujące toobe zdarzeń systemu windows hello zbierane. Na przykład:<br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> Określ wszystkie zdarzenia toocollect "*"|  




## <a name="logs-element"></a>Element dzienników  
 *Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - dzienniki katalogu głównego*

 Przedstawia w wersji 1.0, 1.1. Brak w 1.2. Dodane ponownie w 1.3.  

 Definiuje konfigurację buforu hello podstawowe dzienników Azure.  

|Atrybut|Typ|Opis|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|**unsignedInt**|Opcjonalny. Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla hello określony hello danych.<br /><br /> Witaj domyślna to 0.|  
|**scheduledTransferLogLevelFilterr**|**ciąg**|Opcjonalny. Określa hello minimalny poziom ważności wpisy dziennika, które są przenoszone. Witaj, wartość domyślna to **niezdefiniowane**, który przesyła wszystkie dzienniki. Inne możliwe wartości (w kolejności większość informacji tooleast) to **pełne**, **informacji**, **ostrzeżenie**, **błąd**i **Krytyczne**.|  
|**scheduledTransferPeriod**|**czas trwania**|Opcjonalny. Określa interwał hello między zaplanowane transferów danych, zaokrąglona w górę toohello najbliższej minutę.<br /><br /> Domyślnie Hello jest PT0S.|  
|**wychwytywanie** dodane w wersji 1.5|**ciąg**|Opcjonalny. Punkty tooa zbiornika lokalizacji tooalso Wyślij dane diagnostyczne. Na przykład usługi Application Insights.|  

## <a name="dockersources"></a>DockerSources
 *Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources katalogu głównego*

 Dodane w 1.9.

|Nazwa elementu|Opis|  
|------------------|-----------------|  
|**Statystyka**|Informuje hello system toocollect Statystyka kontenery Docker|  

## <a name="sinksconfig-element"></a>SinksConfig Element  
 *Drzewa: SinksConfig PublicConfig - WadCFG - głównego - DiagnosticsConfiguration-*

 Lista lokalizacji toosend diagnostyki danych tooand hello konfiguracji skojarzone z tych lokalizacjach.  

|Nazwa elementu|Opis|  
|------------------|-----------------|  
|**Obiekt sink**|Zobacz opis w innym miejscu na tej stronie.|  

## <a name="sink-element"></a>Sink — Element
 *Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - zbiornika katalogu głównego*

 Dodane w wersji 1.5.  

 Definiuje danych diagnostycznych toosend dla lokalizacji. Na przykład hello usługa Application Insights.  

|Atrybut|Typ|Opis|  
|---------------|----------|-----------------|  
|**Nazwa**|Ciąg|Ciąg identyfikacyjny hello sinkname.|  

|Element|Typ|Opis|  
|-------------|----------|-----------------|  
|**Usługa Application Insights**|Ciąg|Używana tylko w przypadku wysyłania danych tooApplication szczegółowych informacji. Zawierają hello klucza instrumentacji dla aktywnego konta usługi Application Insights, czy masz dostęp do.|  
|**Kanały**|Ciąg|Po jednej dla każdego dodatkowego filtrowania strumienia, który|  

## <a name="channels-element"></a>Element kanałów  
 *Drzewa: Kanały SinksConfig - zbiornika - głównego - DiagnosticsConfiguration - PublicConfig - WadCFG-*

 Dodane w wersji 1.5.  

 Definiuje filtry dla strumieni danych dziennika przechodzącej przez zbiorniku.  

|Element|Typ|Opis|  
|-------------|----------|-----------------|  
|**Kanał**|Ciąg|Zobacz opis w innym miejscu na tej stronie.|  

## <a name="channel-element"></a>Element kanału
 *Drzewa: Kanały SinksConfig - zbiornika - głównego - DiagnosticsConfiguration - PublicConfig - WadCFG - — kanału*

 Dodane w wersji 1.5.  

 Definiuje danych diagnostycznych toosend dla lokalizacji. Na przykład hello usługa Application Insights.  

|Atrybuty|Typ|Opis|  
|----------------|----------|-----------------|  
|**logLevel**|**ciąg**|Określa hello minimalny poziom ważności wpisy dziennika, które są przenoszone. Witaj, wartość domyślna to **niezdefiniowane**, który przesyła wszystkie dzienniki. Inne możliwe wartości (w kolejności większość informacji tooleast) to **pełne**, **informacji**, **ostrzeżenie**, **błąd**i **Krytyczne**.|  
|**Nazwa**|**ciąg**|Unikatowa nazwa hello toorefer kanału do|  


## <a name="privateconfig-element"></a>PrivateConfig Element 
 *Drzewa: PrivateConfig - DiagnosticsConfiguration - katalogu głównego*

 Dodany w wersji 1.3.  

 Optional (Opcjonalność)  

 Przechowuje prywatne informacje szczegółowe hello hello konta magazynu (nazwa, klucz i końcowy). Te informacje są wysyłane toohello maszyny wirtualnej, ale nie można pobrać z niego.  

|Elementy podrzędne|Opis|  
|--------------------|-----------------|  
|**Konto magazynu**|Witaj toouse konta magazynu. Witaj następujące atrybuty są wymagane<br /><br /> - **Nazwa** — Witaj nazwa konta magazynu hello.<br /><br /> - **klucz** — Witaj klucza toohello konta magazynu.<br /><br /> - **punkt końcowy** -tooaccess punktu końcowego hello hello konta magazynu. <br /><br /> -**sasToken** (1.8.1)-tokenu sygnatury dostępu Współdzielonego, zamiast klucz konta magazynu można określić w pliku konfiguracyjnym prywatnego hello dodane. Podany klucz konta magazynu hello jest ignorowana. <br />Wymagania dotyczące hello tokenu sygnatury dostępu Współdzielonego: <br />— Obsługuje tylko tokenu sygnatury dostępu Współdzielonego konta <br />- *b*, *t* typów usług są wymagane. <br /> - **, *c*, *u*, *w* uprawnienia są wymagane. <br /> - *c*, *o* typów zasobów są wymagane. <br /> — Obsługuje tylko protokół HTTPS hello <br /> -Start i czas wygaśnięcia musi być prawidłowy.|  


## <a name="isenabled-element"></a>IsEnabled Element  
 *Drzewa: IsEnabled - DiagnosticsConfiguration - katalogu głównego*

 Wartość logiczna. Użyj `true` tooenable hello diagnostyki lub `false` toodisable hello diagnostyki.
