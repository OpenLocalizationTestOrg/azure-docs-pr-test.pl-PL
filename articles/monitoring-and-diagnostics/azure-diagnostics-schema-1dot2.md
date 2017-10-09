---
title: Schemat konfiguracji 1.2 diagnostyki aaaAzure | Dokumentacja firmy Microsoft
description: "Znaczenie tylko wtedy, gdy 2.5 zestawu SDK platformy Azure za pomocą usługi Azure Virtual Machines, zestawy skalowania maszyny wirtualnej, sieci szkieletowej usług lub usługi w chmurze."
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
ms.openlocfilehash: 31559317b696556a64b51b58800b176ade9a4679
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-12-configuration-schema"></a>Schemat konfiguracji 1.2 Diagnostyka Azure
> [!NOTE]
> Diagnostyka Azure to liczniki wydajności toocollect używany składnik hello i innych danych statystycznych z maszyn wirtualnych platformy Azure, zestawy skalowania maszyn wirtualnych, sieci szkieletowej usług i usługi w chmurze.  Ta strona jest tylko istotne, jeśli używasz tych usług.
>

Diagnostyka Azure jest używana z innymi produktami firmy Microsoft diagnostyki, takich jak Azure monitora, usługi Application Insights i analizy dzienników.

Ten schemat definiuje hello możliwe wartości można użyć ustawień diagnostycznych konfiguracji tooinitialize przy uruchomieniu hello diagnostyki monitora.  


 Pobierz definicję schematu pliku konfiguracji publicznego hello, wykonując następujące polecenia programu PowerShell hello:  

```PowerShell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

 Aby uzyskać więcej informacji o korzystaniu z diagnostyki Azure, zobacz [Włączanie diagnostyki w usług Azure Cloud Services](http://azure.microsoft.com/documentation/articles/cloud-services-dotnet-diagnostics/).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Przykładowy plik konfiguracji diagnostyki hello  
 Hello poniższy przykład przedstawia plik diagnostyki typowych konfiguracji:  

```xml
<?xml version="1.0" encoding="utf-8"?>  
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">  
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
        <EtwEventSourceProviderConfiguration provider="MyProviderClass" scheduledTransferPeriod="PT5M">  
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
      <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
        <CrashDumpConfiguration processName="mynewprocess.exe" />  
        <CrashDumpConfiguration processName="badapp.exe"/>  
      </CrashDumps>  
    </DiagnosticMonitorConfiguration>  
  </WadCfg>  
</PublicConfig>  

```  

## <a name="diagnostics-configuration-namespace"></a>Namespace konfiguracji diagnostyki  
 przestrzeń nazw XML Hello pliku konfiguracji diagnostyki hello jest:  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="publicconfig-element"></a>PublicConfig Element  
 Element najwyższego poziomu w pliku konfiguracji hello diagnostyki. Witaj poniższej tabeli opisano elementy hello hello pliku konfiguracji.  

|Nazwa elementu|Opis|  
|------------------|-----------------|  
|**WadCfg**|Wymagany. Ustawienia konfiguracji dla toobe danych telemetrycznych hello zbierane.|  
|**Konto magazynu**|Nazwa Hello danych konta usługi Azure Storage hello hello toostore w. To można także określić jako parametr podczas wykonywania polecenia cmdlet hello AzureServiceDiagnosticsExtension zestawu.|  
|**LocalResourceDirectory**|katalog Hello na powitania maszyny wirtualnej toobe używany przez hello dane zdarzenia toostore Monitoring Agent. Jeśli nie jest używany zestaw, hello domyślny katalog:<br /><br /> Dla roli proces roboczy/sieci web:`C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> Dla maszyny wirtualnej:`C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> Atrybuty wymagane są:<br /><br /> -                      **ścieżka** — Witaj katalogu na powitania toobe systemu używany przez diagnostyki Azure.<br /><br /> -                      **expandEnvironment** — Określa, czy w nazwie ścieżki hello są rozwinięte zmiennych środowiskowych.|  

## <a name="wadcfg-element"></a>WadCFG Element  
Definiuje ustawienia konfiguracji dla toobe danych telemetrycznych hello zbierane. Witaj w poniższej tabeli opisano elementy podrzędne:  

|Nazwa elementu|Opis|  
|------------------|-----------------|  
|**DiagnosticMonitorConfiguration**|Wymagany. Opcjonalne atrybuty:<br /><br /> -                     **overallQuotaInMB** -hello maksymalną ilość miejsca na dysku lokalnym, które może być zużyte przez hello różnego typu dane diagnostyczne zebrane przez diagnostyki Azure. Witaj domyślne ustawienie to 5120MB.<br /><br /> -                     **useProxyServer** -diagnostyki Azure skonfigurować ustawienia serwera proxy hello toouse zgodnie z ustawieniami w ustawieniach programu Internet Explorer.|  
|**Zrzutów awaryjnych**|Włącz zbieranie zrzutów awarii. Opcjonalne atrybuty:<br /><br /> -                     **Właściwość containerName** -zrzuty awaryjne toostore używana nazwa hello hello kontenera obiektów blob w toobe konta użytkownika usługi Azure Storage.<br /><br /> -                     **crashDumpType** -zrzuty toocollect konfiguruje diagnostyki Azure Mini lub pełnego awarii.<br /><br /> -                     **directoryQuotaPercentage**— umożliwia skonfigurowanie wartości procentowej hello **overallQuotaInMB** toobe zarezerwowane zrzuty awaryjne na powitania maszyny Wirtualnej.|  
|**DiagnosticInfrastructureLogs**|Włącz zbieranie dzienników generowanych przez diagnostyki Azure. dzienniki diagnostyczne infrastruktury Hello są przydatne podczas rozwiązywania problemów sam system diagnostyki hello. Opcjonalne atrybuty:<br /><br /> -                     **scheduledTransferLogLevelFilter** — konfiguruje hello minimalny poziom ważności dzienników hello zbierane.<br /><br /> -                     **scheduledTransferPeriod** — interwał powitania między toostorage zaplanowane transferów zaokrąglona w górę toohello najbliższej minutę. wartość Hello jest [XML "Typ danych Duration."](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**Katalogi**|Umożliwia hello kolekcji hello zawartości katalogu, usługi IIS nie powiodło się, dzienniki żądania dostępu i/lub dzienniki programu IIS. Atrybut opcjonalny:<br /><br /> **scheduledTransferPeriod** — interwał powitania między toostorage zaplanowane transferów zaokrąglona w górę toohello najbliższej minutę. wartość Hello jest [XML "Typ danych Duration."](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**EtwProviders**|Zbieranie zdarzeń ETW z EventSource konfiguruje i/lub ETW manifestu na podstawie dostawców.|  
|**Metryki**|Ten element włącza toogenerate tabeli licznika wydajności, która jest zoptymalizowana pod kątem szybkiego zapytania. Każdego licznika wydajności, który jest zdefiniowany w hello **liczniki wydajności** elementu są przechowywane w tabeli metryki hello tabeli dodanie toohello licznika wydajności. Wymagany atrybut:<br /><br /> **resourceId** -to jest identyfikator zasobu hello hello wdrażasz diagnostyki Azure do maszyny wirtualnej. Pobierz hello **resourceID** z hello [portalu Azure](https://portal.azure.com). Wybierz **Przeglądaj** -> **grup zasobów** -> **< nazwa\>**. Kliknij przycisk hello **właściwości** Kafelek i skopiuj wartość hello z hello **identyfikator** pola.|  
|**Liczniki wydajności**|Umożliwia zbieranie hello liczników wydajności. Atrybut opcjonalny:<br /><br /> **scheduledTransferPeriod** — interwał powitania między toostorage zaplanowane transferów zaokrąglona w górę toohello najbliższej minutę. Wartość jest [XML "Czas trwania typu danych".](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**WindowsEventLog**|Umożliwia zbieranie hello dzienniki zdarzeń systemu Windows. Atrybut opcjonalny:<br /><br /> **scheduledTransferPeriod** — interwał powitania między toostorage zaplanowane transferów zaokrąglona w górę toohello najbliższej minutę. Wartość jest [XML "Czas trwania typu danych".](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  

## <a name="crashdumps-element"></a>Element zrzutów awaryjnych  
 Umożliwia zbieranie zrzutów awaryjnych. Witaj w poniższej tabeli opisano elementy podrzędne:  

|Nazwa elementu|Opis|  
|------------------|-----------------|  
|**CrashDumpConfiguration**|Wymagany. Wymagany atrybut:<br /><br /> **Parametr** — Witaj nazwa procesu hello ma toocollect diagnostyki Azure dla zrzutu awaryjnego.|  
|**crashDumpType**|Konfiguruje zrzuty awaryjne mini lub pełnego toocollect diagnostyki Azure.|  
|**directoryQuotaPercentage**|Umożliwia skonfigurowanie wartości procentowej hello **overallQuotaInMB** toobe zarezerwowane zrzuty awaryjne na powitania maszyny Wirtualnej.|  

## <a name="directories-element"></a>Element katalogów  
 Umożliwia hello kolekcji hello zawartości katalogu, usługi IIS nie powiodło się, dzienniki żądania dostępu i/lub dzienniki programu IIS. Witaj w poniższej tabeli opisano elementy podrzędne:  

|Nazwa elementu|Opis|  
|------------------|-----------------|  
|**Źródła danych**|Lista katalogów toomonitor.|  
|**FailedRequestLogs**|W tym ten element w konfiguracji hello umożliwia zbieranie dzienników dotyczące żądań zakończonych niepowodzeniem tooan IIS witryny lub aplikacji. Należy też włączyć śledzenie opcje w obszarze **systemu. Serwer sieci Web** w **Web.config**.|  
|**IISLogs**|W tym ten element w konfiguracji hello umożliwia hello zbieranie dzienników usług IIS:<br /><br /> **Właściwość containerName** — dzienniki programu IIS hello toostore używana nazwa hello hello kontenera obiektów blob w toobe konta użytkownika usługi Azure Storage.|  

## <a name="datasources-element"></a>Element źródeł danych  
 Lista katalogów toomonitor. Witaj w poniższej tabeli opisano elementy podrzędne:  

|Nazwa elementu|Opis|  
|------------------|-----------------|  
|**DirectoryConfiguration**|Wymagany. Wymagany atrybut:<br /><br /> **Właściwość containerName** — nazwa hello hello kontenera obiektów blob w magazynie Azure konta toostore toobe używane hello plików dziennika.|  

## <a name="directoryconfiguration-element"></a>DirectoryConfiguration Element  
 **DirectoryConfiguration** może zawierać albo hello **bezwzględną** lub **LocalResource** elementu, ale nie oba. Witaj w poniższej tabeli opisano elementy podrzędne:  

|Nazwa elementu|Opis|  
|------------------|-----------------|  
|**Bezwzględne**|Witaj toomonitor katalogu toohello ścieżkę bezwzględną. Witaj następujące atrybuty są wymagane:<br /><br /> -                     **Ścieżka** — Witaj toomonitor katalogu toohello ścieżkę bezwzględną.<br /><br /> -                      **expandEnvironment** — Określa, czy są rozwinięte zmiennych środowiskowych w ścieżce.|  
|**LocalResource**|Witaj toomonitor zasobu lokalnego tooa względną ścieżkę. Atrybuty wymagane są:<br /><br /> -                     **Nazwa** — Witaj zasób lokalny, który zawiera toomonitor katalogu hello<br /><br /> -                     **relativePath** — Witaj tooName względną ścieżkę zawierającą hello toomonitor katalogu|  

## <a name="etwproviders-element"></a>EtwProviders Element  
 Zbieranie zdarzeń ETW z EventSource konfiguruje i/lub ETW manifestu na podstawie dostawców. Witaj w poniższej tabeli opisano elementy podrzędne:  

|Nazwa elementu|Opis|  
|------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|Konfiguruje zbierania zdarzeń generowanych przez [EventSource — klasa](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Wymagany atrybut:<br /><br /> **Dostawca** — Nazwa klasy hello hello EventSource zdarzenia.<br /><br /> Opcjonalne atrybuty:<br /><br /> -                     **scheduledTransferLogLevelFilter** — Witaj konta magazynu tooyour tootransfer poziomu ważności minimalnej.<br /><br /> -                     **scheduledTransferPeriod** — interwał powitania między toostorage zaplanowane transferów zaokrąglona w górę toohello najbliższej minutę. Wartość jest [typu danych XML czas trwania](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  
|**EtwManifestProviderConfiguration**|Wymagany atrybut:<br /><br /> **Dostawca** — Witaj GUID hello Dostawca zdarzeń<br /><br /> Opcjonalne atrybuty:<br /><br /> - **scheduledTransferLogLevelFilter** — Witaj konta magazynu tooyour tootransfer poziomu ważności minimalnej.<br /><br /> -                     **scheduledTransferPeriod** — interwał powitania między toostorage zaplanowane transferów zaokrąglona w górę toohello najbliższej minutę. Wartość jest [typu danych XML czas trwania](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="etweventsourceproviderconfiguration-element"></a>EtwEventSourceProviderConfiguration Element  
 Konfiguruje zbierania zdarzeń generowanych przez [EventSource — klasa](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Witaj w poniższej tabeli opisano elementy podrzędne:  

|Nazwa elementu|Opis|  
|------------------|-----------------|  
|**DefaultEvents**|Atrybut opcjonalny:<br /><br /> **eventDestination** — Witaj nazwa hello tabeli toostore hello zdarzeń w|  
|**Zdarzenie**|Wymagany atrybut:<br /><br /> **Identyfikator** — identyfikator hello hello zdarzenia.<br /><br /> Atrybut opcjonalny:<br /><br /> **eventDestination** — Witaj nazwa hello tabeli toostore hello zdarzeń w|  

## <a name="etwmanifestproviderconfiguration-element"></a>EtwManifestProviderConfiguration Element  
 Witaj w poniższej tabeli opisano elementy podrzędne:  

|Nazwa elementu|Opis|  
|------------------|-----------------|  
|**DefaultEvents**|Atrybut opcjonalny:<br /><br /> **eventDestination** — Witaj nazwa hello tabeli toostore hello zdarzeń w|  
|**Zdarzenie**|Wymagany atrybut:<br /><br /> **Identyfikator** — identyfikator hello hello zdarzenia.<br /><br /> Atrybut opcjonalny:<br /><br /> **eventDestination** — Witaj nazwa hello tabeli toostore hello zdarzeń w|  

## <a name="metrics-element"></a>Element metryk  
 Umożliwia toogenerate tabeli licznika wydajności, która jest zoptymalizowana pod kątem szybkiego zapytania. Witaj w poniższej tabeli opisano elementy podrzędne:  

|Nazwa elementu|Opis|  
|------------------|-----------------|  
|**MetricAggregation**|Wymagany atrybut:<br /><br /> **scheduledTransferPeriod** — interwał powitania między toostorage zaplanowane transferów zaokrąglona w górę toohello najbliższej minutę. Wartość jest [typu danych XML czas trwania](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="performancecounters-element"></a>PerformanceCounters — Element  
 Umożliwia zbieranie hello liczników wydajności. Witaj w poniższej tabeli opisano elementy podrzędne:  

|Nazwa elementu|Opis|  
|------------------|-----------------|  
|**PerformanceCounterConfiguration**|Witaj następujące atrybuty są wymagane:<br /><br /> -                     **counterSpecifier** — Witaj nazwa hello licznika wydajności. Na przykład `\Processor(_Total)\% Processor Time`. tooget listę liczników wydajności na hoście Uruchom polecenie hello `typeperf`.<br /><br /> -                     **sampleRate** -częstotliwość hello licznika powinny być pobrane.<br /><br /> Atrybut opcjonalny:<br /><br /> **Jednostka** -hello jednostka miary hello licznika.|  

## <a name="performancecounterconfiguration-element"></a>PerformanceCounterConfiguration Element  
 Witaj w poniższej tabeli opisano elementy podrzędne:  

|Nazwa elementu|Opis|  
|------------------|-----------------|  
|**Adnotacja**|Wymagany atrybut:<br /><br /> **Nazwa wyświetlana** — Nazwa wyświetlana hello licznika hello<br /><br /> Atrybut opcjonalny:<br /><br /> **Ustawienia regionalne** — Witaj toouse ustawień regionalnych, wyświetlając nazwę licznika hello|  

## <a name="windowseventlog-element"></a>WindowsEventLog Element  
 Witaj w poniższej tabeli opisano elementy podrzędne:  

|Nazwa elementu|Opis|  
|------------------|-----------------|  
|**Źródło danych**|Witaj toocollect dzienniki zdarzeń systemu Windows. Wymagany atrybut:<br /><br /> **Nazwa** -Kwerenda XPath hello opisujące toobe zdarzeń systemu windows hello zbierane. Na przykład:<br /><br /> `Application!*[System[(Level >= 3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level >= 3]]`<br /><br /> Określ wszystkie zdarzenia toocollect "*".|
