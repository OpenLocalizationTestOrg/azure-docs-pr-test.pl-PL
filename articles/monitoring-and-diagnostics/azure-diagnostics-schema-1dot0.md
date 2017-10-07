---
title: Schemat konfiguracji 1.0 diagnostyki aaaAzure | Dokumentacja firmy Microsoft
description: "TYLKO odpowiednie Jeśli używasz 2.4 zestawu SDK platformy Azure i poniżej z maszyn wirtualnych platformy Azure, zestawy skalowania maszyn wirtualnych, sieci szkieletowej usług lub usługi w chmurze."
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
ms.openlocfilehash: bdd2b26217d6ea28f19e651ab429e7e7401ff57b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a>Schemat konfiguracji diagnostyki Azure 1.0
> [!NOTE]
> Diagnostyka Azure to liczniki wydajności toocollect używany składnik hello i innych danych statystycznych z maszyn wirtualnych platformy Azure, zestawy skalowania maszyn wirtualnych, sieci szkieletowej usług i usługi w chmurze.  Ta strona jest tylko istotne, jeśli używasz tych usług.
>

Diagnostyka Azure jest używana z innymi produktami firmy Microsoft diagnostyki, takich jak Azure monitora, usługi Application Insights i analizy dzienników.

plik konfiguracji diagnostyki Azure Hello definiuje wartości, które są używane tooinitialize hello Monitor diagnostyki. Ten plik jest tooinitialize używanych ustawień diagnostycznych konfiguracji diagnostyki hello monitorujący uruchamia.  

 Domyślnie plik schematu konfiguracji diagnostyki Azure hello jest zainstalowana toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` katalogu. Zastąp `<version>` z hello zainstalowana wersja hello [zestawu Azure SDK](http://www.windowsazure.com/develop/downloads/).  

> [!NOTE]
>  plik konfiguracji diagnostyki Hello są zwykle stosowane z uruchomienia zadania, które wymagają toobe danych diagnostycznych zebranych wcześniej w procesie uruchamiania hello. Aby uzyskać więcej informacji o korzystaniu z diagnostyki Azure, zobacz [zbierania danych rejestrowania za pomocą diagnostyki Azure](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Przykładowy plik konfiguracji diagnostyki hello  
 Hello poniższy przykład przedstawia plik diagnostyki typowych konfiguracji:  

```xml  
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"  
      configurationChangePollInterval="PT1M"  
      overallQuotaInMB="4096">  
   <DiagnosticInfrastructureLogs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  
   <Logs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  

   <Directories bufferQuotaInMB="1024"   
      scheduledTransferPeriod="PT1M">  

      <!-- These three elements specify hello special directories   
           that are set up for hello log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories hello DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative tooa local   
                 resource defined in hello service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- hello counter specifier is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- hello event log name is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a>Namespace DiagnosticsConfiguration  
 przestrzeń nazw XML Hello pliku konfiguracji diagnostyki hello jest:  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a>Elementy schematu  
 plik konfiguracji diagnostyki Hello obejmuje hello następujące elementy.


## <a name="diagnosticmonitorconfiguration-element"></a>DiagnosticMonitorConfiguration Element  
element najwyższego poziomu Hello pliku konfiguracyjnego hello diagnostyki.  

Atrybuty:

|Atrybut  |Typ   |Wymagane| Domyślne | Opis|  
|-----------|-------|--------|---------|------------|  
|**configurationChangePollInterval**|Czas trwania|Optional (Opcjonalność) | PT1M| Określa interwał hello, w których sond diagnostycznych monitor hello zmian konfiguracji diagnostyki.|  
|**overallQuotaInMB**|unsignedInt|Optional (Opcjonalność)| 4000 MB. Jeżeli określona wartość nie może przekraczać tę wartość |Witaj łączną ilość przydzielonego na wszystkie bufory rejestrowania magazyn systemu plików.|  

## <a name="diagnosticinfrastructurelogs-element"></a>DiagnosticInfrastructureLogs Element  
Definiuje konfigurację buforu hello hello dzienników, które są generowane przez hello podstawowej infrastruktury diagnostyki.

Element nadrzędny: [DiagnosticMonitorConfiguration elementu](#DiagnosticMonitorConfiguration).  

Atrybuty:

|Atrybut|Typ|Opis|  
|---------|----|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Opcjonalny. Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla hello określony hello danych.<br /><br /> Witaj domyślna to 0.|  
|**scheduledTransferLogLevelFilter**|Ciąg|Opcjonalny. Określa hello minimalny poziom ważności wpisy dziennika, które są przenoszone. Witaj, wartość domyślna to **niezdefiniowane**. Inne możliwe wartości to **pełne**, **informacji**, **ostrzeżenie**, **błąd**, i **krytyczny**.|  
|**scheduledTransferPeriod**|Czas trwania|Opcjonalny. Określa interwał hello między zaplanowane transferów danych, zaokrąglona w górę toohello najbliższej minutę.<br /><br /> Domyślnie Hello jest PT0S.|  

## <a name="logs-element"></a>Element dzienników  
 Definiuje konfigurację buforu hello podstawowe dzienników Azure.

 Element nadrzędny: [DiagnosticMonitorConfiguration elementu](#DiagnosticMonitorConfiguration).  

Atrybuty:  

|Atrybut|Typ|Opis|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Opcjonalny. Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla hello określony hello danych.<br /><br /> Witaj domyślna to 0.|  
|**scheduledTransferLogLevelFilter**|Ciąg|Opcjonalny. Określa hello minimalny poziom ważności wpisy dziennika, które są przenoszone. Witaj, wartość domyślna to **niezdefiniowane**. Inne możliwe wartości to **pełne**, **informacji**, **ostrzeżenie**, **błąd**, i **krytyczny**.|  
|**scheduledTransferPeriod**|Czas trwania|Opcjonalny. Określa interwał hello między zaplanowane transferów danych, zaokrąglona w górę toohello najbliższej minutę.<br /><br /> Domyślnie Hello jest PT0S.|  

## <a name="directories-element"></a>Element katalogów  
Definiuje konfigurację buforu hello opartych na plikach dzienników zdefiniowanych przez użytkownika.

Element nadrzędny: [DiagnosticMonitorConfiguration elementu](#DiagnosticMonitorConfiguration).  


Atrybuty:  

|Atrybut|Typ|Opis|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Opcjonalny. Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla hello określony hello danych.<br /><br /> Witaj domyślna to 0.|  
|**scheduledTransferPeriod**|Czas trwania|Opcjonalny. Określa interwał hello między zaplanowane transferów danych, zaokrąglona w górę toohello najbliższej minutę.<br /><br /> Domyślnie Hello jest PT0S.|  

## <a name="crashdumps-element"></a>Element zrzutów awaryjnych  
 Określa katalog zrzuty awaryjne hello.

 Element nadrzędny: [Element katalogów](#Directories).  

Atrybuty:  

|Atrybut|Typ|Opis|  
|---------------|----------|-----------------|  
|**kontener**|Ciąg|Nazwa Hello kontenera hello gdzie hello zawartość katalogu hello jest toobe transferu.|  
|**directoryQuotaInMB**|unsignedInt|Opcjonalny. Określa maksymalny rozmiar katalogu hello hello w megabajtach.<br /><br /> Witaj domyślna to 0.|  

## <a name="failedrequestlogs-element"></a>FailedRequestLogs Element  
 Określa katalog dziennika nie powiodło się Żądanie hello.

 Element nadrzędny elementu [Element katalogów](#Directories).  

Atrybuty:  

|Atrybut|Typ|Opis|  
|---------------|----------|-----------------|  
|**kontener**|Ciąg|Nazwa Hello kontenera hello gdzie hello zawartość katalogu hello jest toobe transferu.|  
|**directoryQuotaInMB**|unsignedInt|Opcjonalny. Określa maksymalny rozmiar katalogu hello hello w megabajtach.<br /><br /> Witaj domyślna to 0.|  

##  <a name="iislogs-element"></a>IISLogs Element  
 Określa katalog dziennika usług IIS hello.

 Element nadrzędny elementu [Element katalogów](#Directories).  

Atrybuty:  

|Atrybut|Typ|Opis|  
|---------------|----------|-----------------|  
|**kontener**|Ciąg|Nazwa Hello kontenera hello gdzie hello zawartość katalogu hello jest toobe transferu.|  
|**directoryQuotaInMB**|unsignedInt|Opcjonalny. Określa maksymalny rozmiar katalogu hello hello w megabajtach.<br /><br /> Witaj domyślna to 0.|  

## <a name="datasources-element"></a>Element źródeł danych  
 Definiuje zero lub więcej katalogów dodatkowe dziennika.

 Element nadrzędny: [Element katalogów](#Directories).

## <a name="directoryconfiguration-element"></a>DirectoryConfiguration Element  
 Określa katalog hello toomonitor plików dziennika.

 Element nadrzędny: [źródeł danych elementu](#DataSources).

Atrybuty:

|Atrybut|Typ|Opis|  
|---------------|----------|-----------------|  
|**kontener**|Ciąg|Nazwa Hello kontenera hello gdzie hello zawartość katalogu hello jest toobe transferu.|  
|**directoryQuotaInMB**|unsignedInt|Opcjonalny. Określa maksymalny rozmiar katalogu hello hello w megabajtach.<br /><br /> Witaj domyślna to 0.|  

## <a name="absolute-element"></a>Element bezwzględne  
 Określa ścieżkę bezwzględną hello toomonitor katalogu o rozszerzeniu środowiska opcjonalne.

 Element nadrzędny: [DirectoryConfiguration elementu](#DirectoryConfiguration).  

Atrybuty:  

|Atrybut|Typ|Opis|  
|---------------|----------|-----------------|  
|**Ścieżka**|Ciąg|Wymagany. Witaj toomonitor katalogu toohello ścieżkę bezwzględną.|  
|**expandEnvironment**|Wartość logiczna|Wymagany. Jeśli ustawiona zbyt**true**, zmiennych środowiskowych w ścieżce hello są rozwinięte.|  

## <a name="localresource-element"></a>LocalResource Element  
 Określa ścieżkę względną tooa zasób lokalny, określona w definicji usługi hello.

 Element nadrzędny: [DirectoryConfiguration elementu](#DirectoryConfiguration).  

Atrybuty:  

|Atrybut|Typ|Opis|  
|---------------|----------|-----------------|  
|**Nazwa**|Ciąg|Wymagany. Nazwa Hello hello zasób lokalny, który zawiera toomonitor katalogu hello.|  
|**relativePath**|Ciąg|Wymagany. Witaj toomonitor zasobu lokalnego toohello względną ścieżkę.|  

## <a name="performancecounters-element"></a>PerformanceCounters — Element  
 Definiuje hello ścieżki toohello wydajności licznika toocollect.

 Element nadrzędny: [DiagnosticMonitorConfiguration elementu](#DiagnosticMonitorConfiguration).


 Atrybuty:  

|Atrybut|Typ|Opis|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Opcjonalny. Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla hello określony hello danych.<br /><br /> Witaj domyślna to 0.|  
|**scheduledTransferPeriod**|Czas trwania|Opcjonalny. Określa interwał hello między zaplanowane transferów danych, zaokrąglona w górę toohello najbliższej minutę.<br /><br /> Domyślnie Hello jest PT0S.|  

## <a name="performancecounterconfiguration-element"></a>PerformanceCounterConfiguration Element  
 Definiuje toocollect licznika wydajności hello.

 Element nadrzędny: [PerformanceCounters — Element](#PerformanceCounters).  

 Atrybuty:  

|Atrybut|Typ|Opis|  
|---------------|----------|-----------------|  
|**counterSpecifier**|Ciąg|Wymagany. Witaj toocollect licznika wydajności toohello ścieżki.|  
|**sampleRate**|Czas trwania|Wymagany. częstotliwość Hello, w których hello powinny być gromadzone dane licznika wydajności.|  

## <a name="windowseventlog-element"></a>WindowsEventLog Element  
 Definiuje hello toomonitor dzienniki zdarzeń.

 Element nadrzędny: [DiagnosticMonitorConfiguration elementu](#DiagnosticMonitorConfiguration).

  Atrybuty:

|Atrybut|Typ|Opis|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Opcjonalny. Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla hello określony hello danych.<br /><br /> Witaj domyślna to 0.|  
|**scheduledTransferLogLevelFilter**|Ciąg|Opcjonalny. Określa hello minimalny poziom ważności wpisy dziennika, które są przenoszone. Witaj, wartość domyślna to **niezdefiniowane**. Inne możliwe wartości to **pełne**, **informacji**, **ostrzeżenie**, **błąd**, i **krytyczny**.|  
|**scheduledTransferPeriod**|Czas trwania|Opcjonalny. Określa interwał hello między zaplanowane transferów danych, zaokrąglona w górę toohello najbliższej minutę.<br /><br /> Domyślnie Hello jest PT0S.|  

## <a name="datasource-element"></a>DataSource Element  
 Definiuje hello toomonitor dziennika zdarzeń.

 Element nadrzędny: [WindowsEventLog elementu](#windowsEventLog).  

 Atrybuty:

|Atrybut|Typ|Opis|  
|---------------|----------|-----------------|  
|**Nazwa**|Ciąg|Wymagany. Wyrażenie XPath, określając hello toocollect dziennika.|  
