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
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="0f57f-103">1.3 diagnostyki Azure i nowszym schemat konfiguracji</span><span class="sxs-lookup"><span data-stu-id="0f57f-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="0f57f-104">Hello rozszerzenie Azure Diagnostics jest składnik hello używany toocollect liczniki wydajności i innych danych statystycznych z:</span><span class="sxs-lookup"><span data-stu-id="0f57f-104">hello Azure Diagnostics extension is hello component used toocollect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="0f57f-105">Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="0f57f-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="0f57f-106">Zestawy skali maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="0f57f-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="0f57f-107">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0f57f-107">Service Fabric</span></span> 
> - <span data-ttu-id="0f57f-108">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="0f57f-108">Cloud Services</span></span> 
> - <span data-ttu-id="0f57f-109">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="0f57f-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="0f57f-110">Ta strona jest tylko istotne, jeśli używasz tych usług.</span><span class="sxs-lookup"><span data-stu-id="0f57f-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="0f57f-111">Ta strona jest nieprawidłowa dla wersji 1.3 i nowsze (Azure SDK 2.4 i nowszych).</span><span class="sxs-lookup"><span data-stu-id="0f57f-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="0f57f-112">Nowsze sekcji konfiguracji są tooshow komentarze, w jakiej wersji zostały one dodane.</span><span class="sxs-lookup"><span data-stu-id="0f57f-112">Newer configuration sections are commented tooshow in what version they were added.</span></span>  

<span data-ttu-id="0f57f-113">Plik konfiguracyjny Hello opisane w tym miejscu jest tooset używanych ustawień diagnostycznych konfiguracji rozpoczyna monitorowanie hello diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="0f57f-113">hello configuration file described here is used tooset diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

<span data-ttu-id="0f57f-114">rozszerzenie Hello jest używany w połączeniu z innymi produktami firmy Microsoft diagnostyki, takich jak Azure monitora, usługi Application Insights i analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="0f57f-114">hello extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="0f57f-115">Pobierz definicję schematu pliku konfiguracji publicznego hello, wykonując następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="0f57f-115">Download hello public configuration file schema definition by executing hello following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="0f57f-116">Aby uzyskać więcej informacji o korzystaniu z diagnostyki Azure, zobacz [rozszerzenia diagnostyki Azure](azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="0f57f-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="0f57f-117">Przykładowy plik konfiguracji diagnostyki hello</span><span class="sxs-lookup"><span data-stu-id="0f57f-117">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="0f57f-118">Hello poniższy przykład przedstawia plik diagnostyki typowych konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="0f57f-118">hello following example shows a typical diagnostics configuration file:</span></span>  

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

<span data-ttu-id="0f57f-119">Odpowiednik JSON hello poprzedniego pliku konfiguracyjnego XML.</span><span class="sxs-lookup"><span data-stu-id="0f57f-119">JSON equivalent of hello previous XML configuration file.</span></span> 

<span data-ttu-id="0f57f-120">Hello PublicConfig i PrivateConfig są rozdzielone, ponieważ w większości przypadków użycia json, są przekazywane jako różne zmienne.</span><span class="sxs-lookup"><span data-stu-id="0f57f-120">hello PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="0f57f-121">Tych przypadkach obejmują szablony Menedżera zasobów, zestawu skalowania maszyn wirtualnych programu PowerShell i programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f57f-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

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

## <a name="reading-this-page"></a><span data-ttu-id="0f57f-122">Odczytywanie tej strony</span><span class="sxs-lookup"><span data-stu-id="0f57f-122">Reading this page</span></span>  
 <span data-ttu-id="0f57f-123">Hello tagi po są mniej więcej w kolejności przedstawionej w hello poprzedzających przykład.</span><span class="sxs-lookup"><span data-stu-id="0f57f-123">hello tags following are roughly in order shown in hello preceding example.</span></span>  <span data-ttu-id="0f57f-124">Jeśli widzisz pełny opis, których można oczekiwać, wyszukaj strony hello hello elementu lub atrybutu.</span><span class="sxs-lookup"><span data-stu-id="0f57f-124">If you don't see a full description where you expect it, search hello page for hello element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="0f57f-125">Popularne typy atrybutów</span><span class="sxs-lookup"><span data-stu-id="0f57f-125">Common Attribute Types</span></span>  
 <span data-ttu-id="0f57f-126">**scheduledTransferPeriod** atrybutu pojawia się w kilku elementów.</span><span class="sxs-lookup"><span data-stu-id="0f57f-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="0f57f-127">Jest hello odstęp między toostorage zaplanowane transferów zaokrąglona w górę toohello najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="0f57f-127">It is hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="0f57f-128">wartość Hello jest [XML "Typ danych Duration."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="0f57f-128">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="0f57f-129">DiagnosticsConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="0f57f-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="0f57f-130">*Drzewa: Główny - DiagnosticsConfiguration*</span><span class="sxs-lookup"><span data-stu-id="0f57f-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="0f57f-131">Dodany w wersji 1.3.</span><span class="sxs-lookup"><span data-stu-id="0f57f-131">Added in version 1.3.</span></span>  

<span data-ttu-id="0f57f-132">element najwyższego poziomu Hello pliku konfiguracyjnego hello diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="0f57f-132">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="0f57f-133">**Atrybut** xmlns — Witaj przestrzeni nazw XML dla pliku konfiguracji diagnostyki hello jest:</span><span class="sxs-lookup"><span data-stu-id="0f57f-133">**Attribute**  xmlns - hello XML namespace for hello diagnostics configuration file is:</span></span>  
<span data-ttu-id="0f57f-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="0f57f-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="0f57f-135">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="0f57f-135">Child Elements</span></span>|<span data-ttu-id="0f57f-136">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0f57f-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="0f57f-137">**PublicConfig**</span></span>|<span data-ttu-id="0f57f-138">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="0f57f-138">Required.</span></span> <span data-ttu-id="0f57f-139">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="0f57f-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0f57f-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="0f57f-140">**PrivateConfig**</span></span>|<span data-ttu-id="0f57f-141">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0f57f-141">Optional.</span></span> <span data-ttu-id="0f57f-142">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="0f57f-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0f57f-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="0f57f-143">**IsEnabled**</span></span>|<span data-ttu-id="0f57f-144">Wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="0f57f-144">Boolean.</span></span> <span data-ttu-id="0f57f-145">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="0f57f-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="0f57f-146">PublicConfig Element</span><span class="sxs-lookup"><span data-stu-id="0f57f-146">PublicConfig Element</span></span>  
 <span data-ttu-id="0f57f-147">*Drzewa: PublicConfig - DiagnosticsConfiguration - katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="0f57f-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="0f57f-148">W tym artykule opisano hello diagnostyki publicznego konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0f57f-148">Describes hello public diagnostics configuration.</span></span>  

|<span data-ttu-id="0f57f-149">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="0f57f-149">Child Elements</span></span>|<span data-ttu-id="0f57f-150">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0f57f-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="0f57f-151">**WadCfg**</span></span>|<span data-ttu-id="0f57f-152">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="0f57f-152">Required.</span></span> <span data-ttu-id="0f57f-153">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="0f57f-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0f57f-154">**Konto magazynu**</span><span class="sxs-lookup"><span data-stu-id="0f57f-154">**StorageAccount**</span></span>|<span data-ttu-id="0f57f-155">Nazwa Hello danych konta usługi Azure Storage hello hello toostore w.</span><span class="sxs-lookup"><span data-stu-id="0f57f-155">hello name of hello Azure Storage account toostore hello data in.</span></span> <span data-ttu-id="0f57f-156">Można także określić jako parametr podczas wykonywania polecenia cmdlet hello AzureServiceDiagnosticsExtension zestawu.</span><span class="sxs-lookup"><span data-stu-id="0f57f-156">May also be specified as a parameter when executing hello Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="0f57f-157">**StorageType**</span><span class="sxs-lookup"><span data-stu-id="0f57f-157">**StorageType**</span></span>|<span data-ttu-id="0f57f-158">Może być *tabeli*, *obiektu Blob*, lub *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="0f57f-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="0f57f-159">Tabela jest domyślny.</span><span class="sxs-lookup"><span data-stu-id="0f57f-159">Table is default.</span></span> <span data-ttu-id="0f57f-160">Po wybraniu TableAndBlob danych diagnostycznych są zapisywane dwukrotnie — raz tooeach typu.</span><span class="sxs-lookup"><span data-stu-id="0f57f-160">When TableAndBlob is chosen, diagnostic data is written twice -- once tooeach type.</span></span>|  
|<span data-ttu-id="0f57f-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="0f57f-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="0f57f-162">katalog Hello na maszynie wirtualnej hello której hello agenta monitorowania przechowuje dane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="0f57f-162">hello directory on hello virtual machine where hello Monitoring Agent stores event data.</span></span> <span data-ttu-id="0f57f-163">Jeśli nie ustawiono, używane jest hello domyślny katalog:</span><span class="sxs-lookup"><span data-stu-id="0f57f-163">If not, set, hello default directory is used:</span></span><br /><br /> <span data-ttu-id="0f57f-164">Dla roli proces roboczy/sieci web:`C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="0f57f-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="0f57f-165">Dla maszyny wirtualnej:`C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="0f57f-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="0f57f-166">Atrybuty wymagane są:</span><span class="sxs-lookup"><span data-stu-id="0f57f-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="0f57f-167">- **ścieżka** — Witaj katalogu na powitania toobe systemu używany przez diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="0f57f-167">- **path** - hello directory on hello system toobe used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="0f57f-168">- **expandEnvironment** — Określa, czy w nazwie ścieżki hello są rozwinięte zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="0f57f-168">- **expandEnvironment** - Controls whether environment variables are expanded in hello path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="0f57f-169">WadCFG Element</span><span class="sxs-lookup"><span data-stu-id="0f57f-169">WadCFG Element</span></span>  
 <span data-ttu-id="0f57f-170">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="0f57f-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="0f57f-171">Identyfikuje i konfiguruje toobe danych telemetrycznych hello zbierane.</span><span class="sxs-lookup"><span data-stu-id="0f57f-171">Identifies and configures hello telemetry data toobe collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="0f57f-172">DiagnosticMonitorConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="0f57f-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="0f57f-173">*Drzewa: DiagnosticMonitorConfiguration PublicConfig - WadCFG - głównego - DiagnosticsConfiguration-*</span><span class="sxs-lookup"><span data-stu-id="0f57f-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="0f57f-174">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0f57f-174">Required</span></span> 

|<span data-ttu-id="0f57f-175">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="0f57f-175">Attributes</span></span>|<span data-ttu-id="0f57f-176">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="0f57f-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="0f57f-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="0f57f-178">Maksymalna ilość miejsca na dysku lokalnym, które może być zużyte przez hello Hello różnego typu dane diagnostyczne zebrane przez diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="0f57f-178">hello maximum amount of local disk space that may be consumed by hello various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="0f57f-179">Witaj domyślne ustawienie to 5120 MB.</span><span class="sxs-lookup"><span data-stu-id="0f57f-179">hello default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="0f57f-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="0f57f-180">**useProxyServer**</span></span> | <span data-ttu-id="0f57f-181">Skonfiguruj ustawienia serwera proxy hello toouse diagnostyki Azure zgodnie z ustawieniami w ustawieniach programu Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="0f57f-181">Configure Azure Diagnostics toouse hello proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="0f57f-182">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="0f57f-182">Child Elements</span></span>|<span data-ttu-id="0f57f-183">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0f57f-184">**Zrzutów awaryjnych**</span><span class="sxs-lookup"><span data-stu-id="0f57f-184">**CrashDumps**</span></span>|<span data-ttu-id="0f57f-185">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="0f57f-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0f57f-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="0f57f-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="0f57f-187">Włącz zbieranie dzienników generowanych przez diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="0f57f-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="0f57f-188">dzienniki diagnostyczne infrastruktury Hello są przydatne podczas rozwiązywania problemów sam system diagnostyki hello.</span><span class="sxs-lookup"><span data-stu-id="0f57f-188">hello diagnostic infrastructure logs are useful for troubleshooting hello diagnostics system itself.</span></span> <span data-ttu-id="0f57f-189">Opcjonalne atrybuty:</span><span class="sxs-lookup"><span data-stu-id="0f57f-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="0f57f-190">- **scheduledTransferLogLevelFilter** — konfiguruje hello minimalny poziom ważności dzienników hello zbierane.</span><span class="sxs-lookup"><span data-stu-id="0f57f-190">- **scheduledTransferLogLevelFilter** - Configures hello minimum severity level of hello logs collected.</span></span><br /><br /> <span data-ttu-id="0f57f-191">- **scheduledTransferPeriod** — interwał powitania między toostorage zaplanowane transferów zaokrąglona w górę toohello najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="0f57f-191">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="0f57f-192">wartość Hello jest [XML "Typ danych Duration."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="0f57f-192">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="0f57f-193">**Katalogi**</span><span class="sxs-lookup"><span data-stu-id="0f57f-193">**Directories**</span></span>|<span data-ttu-id="0f57f-194">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="0f57f-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0f57f-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="0f57f-195">**EtwProviders**</span></span>|<span data-ttu-id="0f57f-196">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="0f57f-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0f57f-197">**Metryki**</span><span class="sxs-lookup"><span data-stu-id="0f57f-197">**Metrics**</span></span>|<span data-ttu-id="0f57f-198">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="0f57f-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0f57f-199">**Liczniki wydajności**</span><span class="sxs-lookup"><span data-stu-id="0f57f-199">**PerformanceCounters**</span></span>|<span data-ttu-id="0f57f-200">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="0f57f-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0f57f-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="0f57f-201">**WindowsEventLog**</span></span>|<span data-ttu-id="0f57f-202">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="0f57f-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="0f57f-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="0f57f-203">**DockerSources**</span></span>|<span data-ttu-id="0f57f-204">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="0f57f-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="0f57f-205">Element zrzutów awaryjnych</span><span class="sxs-lookup"><span data-stu-id="0f57f-205">CrashDumps Element</span></span>  
 <span data-ttu-id="0f57f-206">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - zrzutów awaryjnych w katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="0f57f-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="0f57f-207">Włącz kolekcję hello zrzuty awaryjne.</span><span class="sxs-lookup"><span data-stu-id="0f57f-207">Enable hello collection of crash dumps.</span></span>  

|<span data-ttu-id="0f57f-208">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="0f57f-208">Attributes</span></span>|<span data-ttu-id="0f57f-209">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="0f57f-210">**Właściwość containerName**</span><span class="sxs-lookup"><span data-stu-id="0f57f-210">**containerName**</span></span>|<span data-ttu-id="0f57f-211">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0f57f-211">Optional.</span></span> <span data-ttu-id="0f57f-212">zrzuty awaryjne toostore używana nazwa Hello hello kontenera obiektów blob w toobe konta użytkownika usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0f57f-212">hello name of hello blob container in your Azure Storage account toobe used toostore crash dumps.</span></span>|  
|<span data-ttu-id="0f57f-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="0f57f-213">**crashDumpType**</span></span>|<span data-ttu-id="0f57f-214">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0f57f-214">Optional.</span></span>  <span data-ttu-id="0f57f-215">Konfiguruje zrzuty awaryjne mini lub pełnego toocollect diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="0f57f-215">Configures Azure Diagnostics toocollect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="0f57f-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="0f57f-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="0f57f-217">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0f57f-217">Optional.</span></span>  <span data-ttu-id="0f57f-218">Umożliwia skonfigurowanie wartości procentowej hello **overallQuotaInMB** toobe zarezerwowane zrzuty awaryjne na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0f57f-218">Configures hello percentage of **overallQuotaInMB** toobe reserved for crash dumps on hello VM.</span></span>|  

|<span data-ttu-id="0f57f-219">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="0f57f-219">Child Elements</span></span>|<span data-ttu-id="0f57f-220">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0f57f-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="0f57f-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="0f57f-222">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="0f57f-222">Required.</span></span> <span data-ttu-id="0f57f-223">Definiuje wartości konfiguracji dla każdego procesu.</span><span class="sxs-lookup"><span data-stu-id="0f57f-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="0f57f-224">wymagane jest również Hello następującego atrybutu:</span><span class="sxs-lookup"><span data-stu-id="0f57f-224">hello following attribute is also required:</span></span><br /><br /> <span data-ttu-id="0f57f-225">**Parametr** — Witaj nazwa procesu hello ma toocollect diagnostyki Azure dla zrzutu awaryjnego.</span><span class="sxs-lookup"><span data-stu-id="0f57f-225">**processName** - hello name of hello process you want Azure Diagnostics toocollect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="0f57f-226">Element katalogów</span><span class="sxs-lookup"><span data-stu-id="0f57f-226">Directories Element</span></span> 
 <span data-ttu-id="0f57f-227">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - katalogów katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="0f57f-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="0f57f-228">Umożliwia hello kolekcji hello zawartości katalogu, usługi IIS nie powiodło się, dzienniki żądania dostępu i/lub dzienniki programu IIS.</span><span class="sxs-lookup"><span data-stu-id="0f57f-228">Enables hello collection of hello contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="0f57f-229">Opcjonalne **scheduledTransferPeriod** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="0f57f-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="0f57f-230">Zawiera wyjaśnienie wcześniej.</span><span class="sxs-lookup"><span data-stu-id="0f57f-230">See explanation earlier.</span></span>  

|<span data-ttu-id="0f57f-231">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="0f57f-231">Child Elements</span></span>|<span data-ttu-id="0f57f-232">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0f57f-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="0f57f-233">**IISLogs**</span></span>|<span data-ttu-id="0f57f-234">W tym ten element w konfiguracji hello umożliwia hello zbieranie dzienników usług IIS:</span><span class="sxs-lookup"><span data-stu-id="0f57f-234">Including this element in hello configuration enables hello collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="0f57f-235">**Właściwość containerName** — dzienniki programu IIS hello toostore używana nazwa hello hello kontenera obiektów blob w toobe konta użytkownika usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0f57f-235">**containerName** - hello name of hello blob container in your Azure Storage account toobe used toostore hello IIS logs.</span></span>|   
|<span data-ttu-id="0f57f-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="0f57f-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="0f57f-237">W tym ten element w konfiguracji hello umożliwia zbieranie dzienników dotyczące żądań zakończonych niepowodzeniem tooan IIS witryny lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0f57f-237">Including this element in hello configuration enables collection of logs about failed requests tooan IIS site or application.</span></span> <span data-ttu-id="0f57f-238">Należy też włączyć śledzenie opcje w obszarze **systemu. Serwer sieci Web** w **Web.config**.</span><span class="sxs-lookup"><span data-stu-id="0f57f-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="0f57f-239">**Źródła danych**</span><span class="sxs-lookup"><span data-stu-id="0f57f-239">**DataSources**</span></span>|<span data-ttu-id="0f57f-240">Lista katalogów toomonitor.</span><span class="sxs-lookup"><span data-stu-id="0f57f-240">A list of directories toomonitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="0f57f-241">Element źródeł danych</span><span class="sxs-lookup"><span data-stu-id="0f57f-241">DataSources Element</span></span>  
 <span data-ttu-id="0f57f-242">*Drzewa: Źródła danych PublicConfig - WadCFG - DiagnosticMonitorConfiguration - katalogów - głównego - DiagnosticsConfiguration-*</span><span class="sxs-lookup"><span data-stu-id="0f57f-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="0f57f-243">Lista katalogów toomonitor.</span><span class="sxs-lookup"><span data-stu-id="0f57f-243">A list of directories toomonitor.</span></span>  

|<span data-ttu-id="0f57f-244">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="0f57f-244">Child Elements</span></span>|<span data-ttu-id="0f57f-245">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0f57f-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="0f57f-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="0f57f-247">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="0f57f-247">Required.</span></span> <span data-ttu-id="0f57f-248">Wymagany atrybut:</span><span class="sxs-lookup"><span data-stu-id="0f57f-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="0f57f-249">**Właściwość containerName** — Witaj nazwa hello kontenera obiektów blob na koncie magazynu Azure, w tym toobe używane pliki dziennika hello toostore.</span><span class="sxs-lookup"><span data-stu-id="0f57f-249">**containerName** - hello name of hello blob container in your Azure Storage account that toobe used toostore hello log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="0f57f-250">DirectoryConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="0f57f-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="0f57f-251">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - katalogów - DataSources — DirectoryConfiguration katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="0f57f-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="0f57f-252">Mogą one obejmować albo hello **bezwzględną** lub **LocalResource** elementu, ale nie oba.</span><span class="sxs-lookup"><span data-stu-id="0f57f-252">May include either hello **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="0f57f-253">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="0f57f-253">Child Elements</span></span>|<span data-ttu-id="0f57f-254">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0f57f-255">**Bezwzględne**</span><span class="sxs-lookup"><span data-stu-id="0f57f-255">**Absolute**</span></span>|<span data-ttu-id="0f57f-256">Witaj toomonitor katalogu toohello ścieżkę bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="0f57f-256">hello absolute path toohello directory toomonitor.</span></span> <span data-ttu-id="0f57f-257">Witaj następujące atrybuty są wymagane:</span><span class="sxs-lookup"><span data-stu-id="0f57f-257">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="0f57f-258">- **Ścieżka** — Witaj toomonitor katalogu toohello ścieżkę bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="0f57f-258">- **Path** - hello absolute path toohello directory toomonitor.</span></span><br /><br /> <span data-ttu-id="0f57f-259">- **expandEnvironment** — Określa, czy są rozwinięte zmiennych środowiskowych w ścieżce.</span><span class="sxs-lookup"><span data-stu-id="0f57f-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="0f57f-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="0f57f-260">**LocalResource**</span></span>|<span data-ttu-id="0f57f-261">Witaj toomonitor zasobu lokalnego tooa względną ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="0f57f-261">hello path relative tooa local resource toomonitor.</span></span> <span data-ttu-id="0f57f-262">Atrybuty wymagane są:</span><span class="sxs-lookup"><span data-stu-id="0f57f-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="0f57f-263">- **Nazwa** — Witaj zasób lokalny, który zawiera toomonitor katalogu hello</span><span class="sxs-lookup"><span data-stu-id="0f57f-263">- **Name** - hello local resource that contains hello directory toomonitor</span></span><br /><br /> <span data-ttu-id="0f57f-264">- **relativePath** — Witaj tooName względną ścieżkę zawierającą hello toomonitor katalogu</span><span class="sxs-lookup"><span data-stu-id="0f57f-264">- **relativePath** - hello path relative tooName that contains hello directory toomonitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="0f57f-265">EtwProviders Element</span><span class="sxs-lookup"><span data-stu-id="0f57f-265">EtwProviders Element</span></span>  
 <span data-ttu-id="0f57f-266">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="0f57f-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="0f57f-267">Zbieranie zdarzeń ETW z EventSource konfiguruje i/lub ETW manifestu na podstawie dostawców.</span><span class="sxs-lookup"><span data-stu-id="0f57f-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="0f57f-268">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="0f57f-268">Child Elements</span></span>|<span data-ttu-id="0f57f-269">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0f57f-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="0f57f-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="0f57f-271">Konfiguruje zbierania zdarzeń generowanych przez [EventSource — klasa](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="0f57f-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="0f57f-272">Wymagany atrybut:</span><span class="sxs-lookup"><span data-stu-id="0f57f-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="0f57f-273">**Dostawca** — Nazwa klasy hello hello EventSource zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="0f57f-273">**provider** - hello class name of hello EventSource event.</span></span><br /><br /> <span data-ttu-id="0f57f-274">Opcjonalne atrybuty:</span><span class="sxs-lookup"><span data-stu-id="0f57f-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="0f57f-275">- **scheduledTransferLogLevelFilter** — Witaj konta magazynu tooyour tootransfer poziomu ważności minimalnej.</span><span class="sxs-lookup"><span data-stu-id="0f57f-275">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="0f57f-276">- **scheduledTransferPeriod** — interwał powitania między toostorage zaplanowane transferów zaokrąglona w górę toohello najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="0f57f-276">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="0f57f-277">wartość Hello jest [XML "Typ danych Duration."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="0f57f-277">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="0f57f-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="0f57f-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="0f57f-279">Wymagany atrybut:</span><span class="sxs-lookup"><span data-stu-id="0f57f-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="0f57f-280">**Dostawca** — Witaj GUID hello Dostawca zdarzeń</span><span class="sxs-lookup"><span data-stu-id="0f57f-280">**provider** - hello GUID of hello event provider</span></span><br /><br /> <span data-ttu-id="0f57f-281">Opcjonalne atrybuty:</span><span class="sxs-lookup"><span data-stu-id="0f57f-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="0f57f-282">- **scheduledTransferLogLevelFilter** — Witaj konta magazynu tooyour tootransfer poziomu ważności minimalnej.</span><span class="sxs-lookup"><span data-stu-id="0f57f-282">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="0f57f-283">- **scheduledTransferPeriod** — interwał powitania między toostorage zaplanowane transferów zaokrąglona w górę toohello najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="0f57f-283">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="0f57f-284">wartość Hello jest [XML "Typ danych Duration."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="0f57f-284">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="0f57f-285">EtwEventSourceProviderConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="0f57f-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="0f57f-286">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwEventSourceProviderConfiguration katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="0f57f-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="0f57f-287">Konfiguruje zbierania zdarzeń generowanych przez [EventSource — klasa](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="0f57f-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="0f57f-288">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="0f57f-288">Child Elements</span></span>|<span data-ttu-id="0f57f-289">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0f57f-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="0f57f-290">**DefaultEvents**</span></span>|<span data-ttu-id="0f57f-291">Atrybut opcjonalny:</span><span class="sxs-lookup"><span data-stu-id="0f57f-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="0f57f-292">**eventDestination** — Witaj nazwa hello tabeli toostore hello zdarzeń w</span><span class="sxs-lookup"><span data-stu-id="0f57f-292">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="0f57f-293">**Zdarzenie**</span><span class="sxs-lookup"><span data-stu-id="0f57f-293">**Event**</span></span>|<span data-ttu-id="0f57f-294">Wymagany atrybut:</span><span class="sxs-lookup"><span data-stu-id="0f57f-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="0f57f-295">**Identyfikator** — identyfikator hello hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="0f57f-295">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="0f57f-296">Atrybut opcjonalny:</span><span class="sxs-lookup"><span data-stu-id="0f57f-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="0f57f-297">**eventDestination** — Witaj nazwa hello tabeli toostore hello zdarzeń w</span><span class="sxs-lookup"><span data-stu-id="0f57f-297">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="0f57f-298">EtwManifestProviderConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="0f57f-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="0f57f-299">*Drzewa: EtwManifestProviderConfiguration PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - głównego - DiagnosticsConfiguration-*</span><span class="sxs-lookup"><span data-stu-id="0f57f-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="0f57f-300">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="0f57f-300">Child Elements</span></span>|<span data-ttu-id="0f57f-301">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0f57f-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="0f57f-302">**DefaultEvents**</span></span>|<span data-ttu-id="0f57f-303">Atrybut opcjonalny:</span><span class="sxs-lookup"><span data-stu-id="0f57f-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="0f57f-304">**eventDestination** — Witaj nazwa hello tabeli toostore hello zdarzeń w</span><span class="sxs-lookup"><span data-stu-id="0f57f-304">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="0f57f-305">**Zdarzenie**</span><span class="sxs-lookup"><span data-stu-id="0f57f-305">**Event**</span></span>|<span data-ttu-id="0f57f-306">Wymagany atrybut:</span><span class="sxs-lookup"><span data-stu-id="0f57f-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="0f57f-307">**Identyfikator** — identyfikator hello hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="0f57f-307">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="0f57f-308">Atrybut opcjonalny:</span><span class="sxs-lookup"><span data-stu-id="0f57f-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="0f57f-309">**eventDestination** — Witaj nazwa hello tabeli toostore hello zdarzeń w</span><span class="sxs-lookup"><span data-stu-id="0f57f-309">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="0f57f-310">Element metryk</span><span class="sxs-lookup"><span data-stu-id="0f57f-310">Metrics Element</span></span>  
 <span data-ttu-id="0f57f-311">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - metryki katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="0f57f-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="0f57f-312">Umożliwia toogenerate tabeli licznika wydajności, która jest zoptymalizowana pod kątem szybkiego zapytania.</span><span class="sxs-lookup"><span data-stu-id="0f57f-312">Enables you toogenerate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="0f57f-313">Każdego licznika wydajności, który jest zdefiniowany w hello **liczniki wydajności** elementu są przechowywane w tabeli metryki hello tabeli dodanie toohello licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="0f57f-313">Each performance counter that is defined in hello **PerformanceCounters** element is stored in hello Metrics table in addition toohello Performance Counter table.</span></span>  

 <span data-ttu-id="0f57f-314">Witaj **resourceId** atrybut jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="0f57f-314">hello **resourceId** attribute is required.</span></span>  <span data-ttu-id="0f57f-315">Identyfikator zasobu Hello hello wdrażasz diagnostyki Azure do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0f57f-315">hello resource ID of hello Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="0f57f-316">Pobierz hello **resourceID** z hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f57f-316">Get hello **resourceID** from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0f57f-317">Wybierz **Przeglądaj** -> **grup zasobów** -> **< nazwa\>**.</span><span class="sxs-lookup"><span data-stu-id="0f57f-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="0f57f-318">Kliknij przycisk hello **właściwości** Kafelek i skopiuj wartość hello z hello **identyfikator** pola.</span><span class="sxs-lookup"><span data-stu-id="0f57f-318">Click hello **Properties** tile and copy hello value from hello **ID** field.</span></span>  

|<span data-ttu-id="0f57f-319">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="0f57f-319">Child Elements</span></span>|<span data-ttu-id="0f57f-320">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0f57f-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="0f57f-321">**MetricAggregation**</span></span>|<span data-ttu-id="0f57f-322">Wymagany atrybut:</span><span class="sxs-lookup"><span data-stu-id="0f57f-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="0f57f-323">**scheduledTransferPeriod** — interwał powitania między toostorage zaplanowane transferów zaokrąglona w górę toohello najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="0f57f-323">**scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="0f57f-324">wartość Hello jest [XML "Typ danych Duration."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="0f57f-324">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="0f57f-325">PerformanceCounters — Element</span><span class="sxs-lookup"><span data-stu-id="0f57f-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="0f57f-326">*Drzewa: DiagnosticMonitorConfiguration PublicConfig - WadCFG - głównego - DiagnosticsConfiguration - - liczniki wydajności*</span><span class="sxs-lookup"><span data-stu-id="0f57f-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="0f57f-327">Umożliwia zbieranie hello liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="0f57f-327">Enables hello collection of performance counters.</span></span>  

 <span data-ttu-id="0f57f-328">Atrybut opcjonalny:</span><span class="sxs-lookup"><span data-stu-id="0f57f-328">Optional attribute:</span></span>  

 <span data-ttu-id="0f57f-329">Opcjonalne **scheduledTransferPeriod** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="0f57f-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="0f57f-330">Zawiera wyjaśnienie wcześniej.</span><span class="sxs-lookup"><span data-stu-id="0f57f-330">See explanation earlier.</span></span>

|<span data-ttu-id="0f57f-331">Element podrzędny</span><span class="sxs-lookup"><span data-stu-id="0f57f-331">Child Element</span></span>|<span data-ttu-id="0f57f-332">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="0f57f-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="0f57f-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="0f57f-334">Witaj następujące atrybuty są wymagane:</span><span class="sxs-lookup"><span data-stu-id="0f57f-334">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="0f57f-335">- **counterSpecifier** — Witaj nazwa hello licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="0f57f-335">- **counterSpecifier** - hello name of hello performance counter.</span></span> <span data-ttu-id="0f57f-336">Na przykład `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="0f57f-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="0f57f-337">tooget listę wydajności liczniki na hoście, uruchom polecenie hello `typeperf`.</span><span class="sxs-lookup"><span data-stu-id="0f57f-337">tooget a list of performance counters on your host, run hello command `typeperf`.</span></span><br /><br /> <span data-ttu-id="0f57f-338">- **sampleRate** -częstotliwość hello licznika powinny być pobrane.</span><span class="sxs-lookup"><span data-stu-id="0f57f-338">- **sampleRate** - How often hello counter should be sampled.</span></span><br /><br /> <span data-ttu-id="0f57f-339">Atrybut opcjonalny:</span><span class="sxs-lookup"><span data-stu-id="0f57f-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="0f57f-340">**Jednostka** -hello jednostka miary hello licznika.</span><span class="sxs-lookup"><span data-stu-id="0f57f-340">**unit** - hello unit of measure of hello counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="0f57f-341">WindowsEventLog Element</span><span class="sxs-lookup"><span data-stu-id="0f57f-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="0f57f-342">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="0f57f-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="0f57f-343">Umożliwia zbieranie hello dzienniki zdarzeń systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="0f57f-343">Enables hello collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="0f57f-344">Opcjonalne **scheduledTransferPeriod** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="0f57f-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="0f57f-345">Zawiera wyjaśnienie wcześniej.</span><span class="sxs-lookup"><span data-stu-id="0f57f-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="0f57f-346">Element podrzędny</span><span class="sxs-lookup"><span data-stu-id="0f57f-346">Child Element</span></span>|<span data-ttu-id="0f57f-347">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="0f57f-348">**Źródło danych**</span><span class="sxs-lookup"><span data-stu-id="0f57f-348">**DataSource**</span></span>|<span data-ttu-id="0f57f-349">Witaj toocollect dzienniki zdarzeń systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="0f57f-349">hello Windows Event logs toocollect.</span></span> <span data-ttu-id="0f57f-350">Wymagany atrybut:</span><span class="sxs-lookup"><span data-stu-id="0f57f-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="0f57f-351">**Nazwa** -Kwerenda XPath hello opisujące toobe zdarzeń systemu windows hello zbierane.</span><span class="sxs-lookup"><span data-stu-id="0f57f-351">**name** - hello XPath query describing hello windows events toobe collected.</span></span> <span data-ttu-id="0f57f-352">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0f57f-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="0f57f-353">Określ wszystkie zdarzenia toocollect "*"</span><span class="sxs-lookup"><span data-stu-id="0f57f-353">toocollect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="0f57f-354">Element dzienników</span><span class="sxs-lookup"><span data-stu-id="0f57f-354">Logs Element</span></span>  
 <span data-ttu-id="0f57f-355">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - dzienniki katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="0f57f-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="0f57f-356">Przedstawia w wersji 1.0, 1.1.</span><span class="sxs-lookup"><span data-stu-id="0f57f-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="0f57f-357">Brak w 1.2.</span><span class="sxs-lookup"><span data-stu-id="0f57f-357">Missing in 1.2.</span></span> <span data-ttu-id="0f57f-358">Dodane ponownie w 1.3.</span><span class="sxs-lookup"><span data-stu-id="0f57f-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="0f57f-359">Definiuje konfigurację buforu hello podstawowe dzienników Azure.</span><span class="sxs-lookup"><span data-stu-id="0f57f-359">Defines hello buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="0f57f-360">Atrybut</span><span class="sxs-lookup"><span data-stu-id="0f57f-360">Attribute</span></span>|<span data-ttu-id="0f57f-361">Typ</span><span class="sxs-lookup"><span data-stu-id="0f57f-361">Type</span></span>|<span data-ttu-id="0f57f-362">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0f57f-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="0f57f-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="0f57f-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="0f57f-364">**unsignedInt**</span></span>|<span data-ttu-id="0f57f-365">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0f57f-365">Optional.</span></span> <span data-ttu-id="0f57f-366">Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla hello określony hello danych.</span><span class="sxs-lookup"><span data-stu-id="0f57f-366">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="0f57f-367">Witaj domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="0f57f-367">hello default is 0.</span></span>|  
|<span data-ttu-id="0f57f-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="0f57f-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="0f57f-369">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="0f57f-369">**string**</span></span>|<span data-ttu-id="0f57f-370">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0f57f-370">Optional.</span></span> <span data-ttu-id="0f57f-371">Określa hello minimalny poziom ważności wpisy dziennika, które są przenoszone.</span><span class="sxs-lookup"><span data-stu-id="0f57f-371">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="0f57f-372">Witaj, wartość domyślna to **niezdefiniowane**, który przesyła wszystkie dzienniki.</span><span class="sxs-lookup"><span data-stu-id="0f57f-372">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="0f57f-373">Inne możliwe wartości (w kolejności większość informacji tooleast) to **pełne**, **informacji**, **ostrzeżenie**, **błąd**i **Krytyczne**.</span><span class="sxs-lookup"><span data-stu-id="0f57f-373">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="0f57f-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="0f57f-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="0f57f-375">**czas trwania**</span><span class="sxs-lookup"><span data-stu-id="0f57f-375">**duration**</span></span>|<span data-ttu-id="0f57f-376">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0f57f-376">Optional.</span></span> <span data-ttu-id="0f57f-377">Określa interwał hello między zaplanowane transferów danych, zaokrąglona w górę toohello najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="0f57f-377">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="0f57f-378">Domyślnie Hello jest PT0S.</span><span class="sxs-lookup"><span data-stu-id="0f57f-378">hello default is PT0S.</span></span>|  
|<span data-ttu-id="0f57f-379">**wychwytywanie** dodane w wersji 1.5</span><span class="sxs-lookup"><span data-stu-id="0f57f-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="0f57f-380">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="0f57f-380">**string**</span></span>|<span data-ttu-id="0f57f-381">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0f57f-381">Optional.</span></span> <span data-ttu-id="0f57f-382">Punkty tooa zbiornika lokalizacji tooalso Wyślij dane diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="0f57f-382">Points tooa sink location tooalso send diagnostic data.</span></span> <span data-ttu-id="0f57f-383">Na przykład usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0f57f-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="0f57f-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="0f57f-384">DockerSources</span></span>
 <span data-ttu-id="0f57f-385">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="0f57f-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="0f57f-386">Dodane w 1.9.</span><span class="sxs-lookup"><span data-stu-id="0f57f-386">Added in 1.9.</span></span>

|<span data-ttu-id="0f57f-387">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="0f57f-387">Element Name</span></span>|<span data-ttu-id="0f57f-388">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="0f57f-389">**Statystyka**</span><span class="sxs-lookup"><span data-stu-id="0f57f-389">**Stats**</span></span>|<span data-ttu-id="0f57f-390">Informuje hello system toocollect Statystyka kontenery Docker</span><span class="sxs-lookup"><span data-stu-id="0f57f-390">Tells hello system toocollect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="0f57f-391">SinksConfig Element</span><span class="sxs-lookup"><span data-stu-id="0f57f-391">SinksConfig Element</span></span>  
 <span data-ttu-id="0f57f-392">*Drzewa: SinksConfig PublicConfig - WadCFG - głównego - DiagnosticsConfiguration-*</span><span class="sxs-lookup"><span data-stu-id="0f57f-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="0f57f-393">Lista lokalizacji toosend diagnostyki danych tooand hello konfiguracji skojarzone z tych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="0f57f-393">A list of locations toosend diagnostics data tooand hello configuration associated with those locations.</span></span>  

|<span data-ttu-id="0f57f-394">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="0f57f-394">Element Name</span></span>|<span data-ttu-id="0f57f-395">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="0f57f-396">**Obiekt sink**</span><span class="sxs-lookup"><span data-stu-id="0f57f-396">**Sink**</span></span>|<span data-ttu-id="0f57f-397">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="0f57f-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="0f57f-398">Sink — Element</span><span class="sxs-lookup"><span data-stu-id="0f57f-398">Sink Element</span></span>
 <span data-ttu-id="0f57f-399">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - zbiornika katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="0f57f-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="0f57f-400">Dodane w wersji 1.5.</span><span class="sxs-lookup"><span data-stu-id="0f57f-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="0f57f-401">Definiuje danych diagnostycznych toosend dla lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="0f57f-401">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="0f57f-402">Na przykład hello usługa Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0f57f-402">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="0f57f-403">Atrybut</span><span class="sxs-lookup"><span data-stu-id="0f57f-403">Attribute</span></span>|<span data-ttu-id="0f57f-404">Typ</span><span class="sxs-lookup"><span data-stu-id="0f57f-404">Type</span></span>|<span data-ttu-id="0f57f-405">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0f57f-406">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="0f57f-406">**name**</span></span>|<span data-ttu-id="0f57f-407">Ciąg</span><span class="sxs-lookup"><span data-stu-id="0f57f-407">string</span></span>|<span data-ttu-id="0f57f-408">Ciąg identyfikacyjny hello sinkname.</span><span class="sxs-lookup"><span data-stu-id="0f57f-408">A string identifying hello sinkname.</span></span>|  

|<span data-ttu-id="0f57f-409">Element</span><span class="sxs-lookup"><span data-stu-id="0f57f-409">Element</span></span>|<span data-ttu-id="0f57f-410">Typ</span><span class="sxs-lookup"><span data-stu-id="0f57f-410">Type</span></span>|<span data-ttu-id="0f57f-411">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="0f57f-412">**Usługa Application Insights**</span><span class="sxs-lookup"><span data-stu-id="0f57f-412">**Application Insights**</span></span>|<span data-ttu-id="0f57f-413">Ciąg</span><span class="sxs-lookup"><span data-stu-id="0f57f-413">string</span></span>|<span data-ttu-id="0f57f-414">Używana tylko w przypadku wysyłania danych tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="0f57f-414">Used only when sending data tooApplication Insights.</span></span> <span data-ttu-id="0f57f-415">Zawierają hello klucza instrumentacji dla aktywnego konta usługi Application Insights, czy masz dostęp do.</span><span class="sxs-lookup"><span data-stu-id="0f57f-415">Contain hello Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="0f57f-416">**Kanały**</span><span class="sxs-lookup"><span data-stu-id="0f57f-416">**Channels**</span></span>|<span data-ttu-id="0f57f-417">Ciąg</span><span class="sxs-lookup"><span data-stu-id="0f57f-417">string</span></span>|<span data-ttu-id="0f57f-418">Po jednej dla każdego dodatkowego filtrowania strumienia, który</span><span class="sxs-lookup"><span data-stu-id="0f57f-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="0f57f-419">Element kanałów</span><span class="sxs-lookup"><span data-stu-id="0f57f-419">Channels Element</span></span>  
 <span data-ttu-id="0f57f-420">*Drzewa: Kanały SinksConfig - zbiornika - głównego - DiagnosticsConfiguration - PublicConfig - WadCFG-*</span><span class="sxs-lookup"><span data-stu-id="0f57f-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="0f57f-421">Dodane w wersji 1.5.</span><span class="sxs-lookup"><span data-stu-id="0f57f-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="0f57f-422">Definiuje filtry dla strumieni danych dziennika przechodzącej przez zbiorniku.</span><span class="sxs-lookup"><span data-stu-id="0f57f-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="0f57f-423">Element</span><span class="sxs-lookup"><span data-stu-id="0f57f-423">Element</span></span>|<span data-ttu-id="0f57f-424">Typ</span><span class="sxs-lookup"><span data-stu-id="0f57f-424">Type</span></span>|<span data-ttu-id="0f57f-425">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="0f57f-426">**Kanał**</span><span class="sxs-lookup"><span data-stu-id="0f57f-426">**Channel**</span></span>|<span data-ttu-id="0f57f-427">Ciąg</span><span class="sxs-lookup"><span data-stu-id="0f57f-427">string</span></span>|<span data-ttu-id="0f57f-428">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="0f57f-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="0f57f-429">Element kanału</span><span class="sxs-lookup"><span data-stu-id="0f57f-429">Channel Element</span></span>
 <span data-ttu-id="0f57f-430">*Drzewa: Kanały SinksConfig - zbiornika - głównego - DiagnosticsConfiguration - PublicConfig - WadCFG - — kanału*</span><span class="sxs-lookup"><span data-stu-id="0f57f-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="0f57f-431">Dodane w wersji 1.5.</span><span class="sxs-lookup"><span data-stu-id="0f57f-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="0f57f-432">Definiuje danych diagnostycznych toosend dla lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="0f57f-432">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="0f57f-433">Na przykład hello usługa Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0f57f-433">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="0f57f-434">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="0f57f-434">Attributes</span></span>|<span data-ttu-id="0f57f-435">Typ</span><span class="sxs-lookup"><span data-stu-id="0f57f-435">Type</span></span>|<span data-ttu-id="0f57f-436">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="0f57f-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="0f57f-437">**logLevel**</span></span>|<span data-ttu-id="0f57f-438">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="0f57f-438">**string**</span></span>|<span data-ttu-id="0f57f-439">Określa hello minimalny poziom ważności wpisy dziennika, które są przenoszone.</span><span class="sxs-lookup"><span data-stu-id="0f57f-439">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="0f57f-440">Witaj, wartość domyślna to **niezdefiniowane**, który przesyła wszystkie dzienniki.</span><span class="sxs-lookup"><span data-stu-id="0f57f-440">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="0f57f-441">Inne możliwe wartości (w kolejności większość informacji tooleast) to **pełne**, **informacji**, **ostrzeżenie**, **błąd**i **Krytyczne**.</span><span class="sxs-lookup"><span data-stu-id="0f57f-441">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="0f57f-442">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="0f57f-442">**name**</span></span>|<span data-ttu-id="0f57f-443">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="0f57f-443">**string**</span></span>|<span data-ttu-id="0f57f-444">Unikatowa nazwa hello toorefer kanału do</span><span class="sxs-lookup"><span data-stu-id="0f57f-444">A unique name of hello channel toorefer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="0f57f-445">PrivateConfig Element</span><span class="sxs-lookup"><span data-stu-id="0f57f-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="0f57f-446">*Drzewa: PrivateConfig - DiagnosticsConfiguration - katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="0f57f-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="0f57f-447">Dodany w wersji 1.3.</span><span class="sxs-lookup"><span data-stu-id="0f57f-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="0f57f-448">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="0f57f-448">Optional</span></span>  

 <span data-ttu-id="0f57f-449">Przechowuje prywatne informacje szczegółowe hello hello konta magazynu (nazwa, klucz i końcowy).</span><span class="sxs-lookup"><span data-stu-id="0f57f-449">Stores hello private details of hello storage account (name, key, and endpoint).</span></span> <span data-ttu-id="0f57f-450">Te informacje są wysyłane toohello maszyny wirtualnej, ale nie można pobrać z niego.</span><span class="sxs-lookup"><span data-stu-id="0f57f-450">This information is sent toohello virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="0f57f-451">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="0f57f-451">Child Elements</span></span>|<span data-ttu-id="0f57f-452">Opis</span><span class="sxs-lookup"><span data-stu-id="0f57f-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0f57f-453">**Konto magazynu**</span><span class="sxs-lookup"><span data-stu-id="0f57f-453">**StorageAccount**</span></span>|<span data-ttu-id="0f57f-454">Witaj toouse konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="0f57f-454">hello storage account toouse.</span></span> <span data-ttu-id="0f57f-455">Witaj następujące atrybuty są wymagane</span><span class="sxs-lookup"><span data-stu-id="0f57f-455">hello following attributes are required</span></span><br /><br /> <span data-ttu-id="0f57f-456">- **Nazwa** — Witaj nazwa konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="0f57f-456">- **name** - hello name of hello storage account.</span></span><br /><br /> <span data-ttu-id="0f57f-457">- **klucz** — Witaj klucza toohello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="0f57f-457">- **key** - hello key toohello storage account.</span></span><br /><br /> <span data-ttu-id="0f57f-458">- **punkt końcowy** -tooaccess punktu końcowego hello hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="0f57f-458">- **endpoint** - hello endpoint tooaccess hello storage account.</span></span> <br /><br /> <span data-ttu-id="0f57f-459">-**sasToken** (1.8.1)-tokenu sygnatury dostępu Współdzielonego, zamiast klucz konta magazynu można określić w pliku konfiguracyjnym prywatnego hello dodane. Podany klucz konta magazynu hello jest ignorowana.</span><span class="sxs-lookup"><span data-stu-id="0f57f-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in hello private config. If provided, hello storage account key is ignored.</span></span> <br /><span data-ttu-id="0f57f-460">Wymagania dotyczące hello tokenu sygnatury dostępu Współdzielonego:</span><span class="sxs-lookup"><span data-stu-id="0f57f-460">Requirements for hello SAS Token:</span></span> <br /><span data-ttu-id="0f57f-461">— Obsługuje tylko tokenu sygnatury dostępu Współdzielonego konta</span><span class="sxs-lookup"><span data-stu-id="0f57f-461">- Supports account SAS token only</span></span> <br /><span data-ttu-id="0f57f-462">- *b*, *t* typów usług są wymagane.</span><span class="sxs-lookup"><span data-stu-id="0f57f-462">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="0f57f-463">- **, *c*, *u*, *w* uprawnienia są wymagane.</span><span class="sxs-lookup"><span data-stu-id="0f57f-463">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="0f57f-464">- *c*, *o* typów zasobów są wymagane.</span><span class="sxs-lookup"><span data-stu-id="0f57f-464">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="0f57f-465">— Obsługuje tylko protokół HTTPS hello</span><span class="sxs-lookup"><span data-stu-id="0f57f-465">- Supports hello HTTPS protocol only</span></span> <br /> <span data-ttu-id="0f57f-466">-Start i czas wygaśnięcia musi być prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="0f57f-466">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="0f57f-467">IsEnabled Element</span><span class="sxs-lookup"><span data-stu-id="0f57f-467">IsEnabled Element</span></span>  
 <span data-ttu-id="0f57f-468">*Drzewa: IsEnabled - DiagnosticsConfiguration - katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="0f57f-468">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="0f57f-469">Wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="0f57f-469">Boolean.</span></span> <span data-ttu-id="0f57f-470">Użyj `true` tooenable hello diagnostyki lub `false` toodisable hello diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="0f57f-470">Use `true` tooenable hello diagnostics or `false` toodisable hello diagnostics.</span></span>
