---
title: Rozszerzenie diagnostyki Azure 1.3 i nowszym schemat konfiguracji | Dokumentacja firmy Microsoft
description: "Wersja schematu 1.3 i nowszym diagnostyki Azure dostarczana jako część 2.4 zestawu SDK programu Microsoft Azure i później."
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
ms.openlocfilehash: 0d814825fb08452238a254ccd30bde230380c74c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="ede70-103">1.3 diagnostyki Azure i nowszym schemat konfiguracji</span><span class="sxs-lookup"><span data-stu-id="ede70-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="ede70-104">Rozszerzenie Azure Diagnostics jest składnik służący do zbierania liczników wydajności i innych danych statystycznych z:</span><span class="sxs-lookup"><span data-stu-id="ede70-104">The Azure Diagnostics extension is the component used to collect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="ede70-105">Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="ede70-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="ede70-106">Zestawy skali maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="ede70-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="ede70-107">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ede70-107">Service Fabric</span></span> 
> - <span data-ttu-id="ede70-108">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="ede70-108">Cloud Services</span></span> 
> - <span data-ttu-id="ede70-109">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="ede70-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="ede70-110">Ta strona jest tylko istotne, jeśli używasz tych usług.</span><span class="sxs-lookup"><span data-stu-id="ede70-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="ede70-111">Ta strona jest nieprawidłowa dla wersji 1.3 i nowsze (Azure SDK 2.4 i nowszych).</span><span class="sxs-lookup"><span data-stu-id="ede70-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="ede70-112">Nowsze sekcji konfiguracji są oznaczone jako do wyświetlenia, w jakiej wersji zostały dodane.</span><span class="sxs-lookup"><span data-stu-id="ede70-112">Newer configuration sections are commented to show in what version they were added.</span></span>  

<span data-ttu-id="ede70-113">Plik konfiguracji opisanych tutaj służy do ustawienia konfiguracji diagnostyczne podczas uruchamiania Monitora diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="ede70-113">The configuration file described here is used to set diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

<span data-ttu-id="ede70-114">Rozszerzenie jest używany w połączeniu z innymi produktami firmy Microsoft diagnostyki, takich jak Azure monitora, usługi Application Insights i analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="ede70-114">The extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="ede70-115">Pobierz definicję schematu pliku konfiguracji publicznego, wykonując następujące polecenie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ede70-115">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="ede70-116">Aby uzyskać więcej informacji o korzystaniu z diagnostyki Azure, zobacz [rozszerzenia diagnostyki Azure](azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="ede70-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="ede70-117">Przykładowy plik konfiguracji diagnostyki</span><span class="sxs-lookup"><span data-stu-id="ede70-117">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="ede70-118">W poniższym przykładzie przedstawiono plik konfiguracji typowych diagnostyki:</span><span class="sxs-lookup"><span data-stu-id="ede70-118">The following example shows a typical diagnostics configuration file:</span></span>  

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

<span data-ttu-id="ede70-119">Wartość równoważna JSON poprzedniego pliku konfiguracyjnego XML.</span><span class="sxs-lookup"><span data-stu-id="ede70-119">JSON equivalent of the previous XML configuration file.</span></span> 

<span data-ttu-id="ede70-120">PublicConfig i PrivateConfig są rozdzielone, ponieważ w większości przypadków użycia json, są przekazywane jako różne zmienne.</span><span class="sxs-lookup"><span data-stu-id="ede70-120">The PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="ede70-121">Tych przypadkach obejmują szablony Menedżera zasobów, zestawu skalowania maszyn wirtualnych programu PowerShell i programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ede70-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

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

## <a name="reading-this-page"></a><span data-ttu-id="ede70-122">Odczytywanie tej strony</span><span class="sxs-lookup"><span data-stu-id="ede70-122">Reading this page</span></span>  
 <span data-ttu-id="ede70-123">Tagi po około znajdują się w kolejności przedstawionej w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="ede70-123">The tags following are roughly in order shown in the preceding example.</span></span>  <span data-ttu-id="ede70-124">Jeśli widzisz pełny opis, których można oczekiwać, wyszukaj strony elementu lub atrybutu.</span><span class="sxs-lookup"><span data-stu-id="ede70-124">If you don't see a full description where you expect it, search the page for the element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="ede70-125">Popularne typy atrybutów</span><span class="sxs-lookup"><span data-stu-id="ede70-125">Common Attribute Types</span></span>  
 <span data-ttu-id="ede70-126">**scheduledTransferPeriod** atrybutu pojawia się w kilku elementów.</span><span class="sxs-lookup"><span data-stu-id="ede70-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="ede70-127">Jest odstęp między zaplanowanego transferu do magazynu zaokrąglona w górę do najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="ede70-127">It is the interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="ede70-128">Wartość jest [XML "Typ danych Duration."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="ede70-128">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="ede70-129">DiagnosticsConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="ede70-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="ede70-130">*Drzewa: Główny - DiagnosticsConfiguration*</span><span class="sxs-lookup"><span data-stu-id="ede70-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="ede70-131">Dodany w wersji 1.3.</span><span class="sxs-lookup"><span data-stu-id="ede70-131">Added in version 1.3.</span></span>  

<span data-ttu-id="ede70-132">Element najwyższego poziomu w pliku konfiguracji diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="ede70-132">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="ede70-133">**Atrybut** xmlns — przestrzeń nazw XML dla pliku konfiguracji diagnostyki jest:</span><span class="sxs-lookup"><span data-stu-id="ede70-133">**Attribute**  xmlns - The XML namespace for the diagnostics configuration file is:</span></span>  
<span data-ttu-id="ede70-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="ede70-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="ede70-135">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="ede70-135">Child Elements</span></span>|<span data-ttu-id="ede70-136">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ede70-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="ede70-137">**PublicConfig**</span></span>|<span data-ttu-id="ede70-138">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="ede70-138">Required.</span></span> <span data-ttu-id="ede70-139">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="ede70-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ede70-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="ede70-140">**PrivateConfig**</span></span>|<span data-ttu-id="ede70-141">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="ede70-141">Optional.</span></span> <span data-ttu-id="ede70-142">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="ede70-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ede70-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="ede70-143">**IsEnabled**</span></span>|<span data-ttu-id="ede70-144">Wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="ede70-144">Boolean.</span></span> <span data-ttu-id="ede70-145">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="ede70-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="ede70-146">PublicConfig Element</span><span class="sxs-lookup"><span data-stu-id="ede70-146">PublicConfig Element</span></span>  
 <span data-ttu-id="ede70-147">*Drzewa: PublicConfig - DiagnosticsConfiguration - katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="ede70-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="ede70-148">Zawiera opis konfiguracji diagnostyki publicznego.</span><span class="sxs-lookup"><span data-stu-id="ede70-148">Describes the public diagnostics configuration.</span></span>  

|<span data-ttu-id="ede70-149">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="ede70-149">Child Elements</span></span>|<span data-ttu-id="ede70-150">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ede70-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="ede70-151">**WadCfg**</span></span>|<span data-ttu-id="ede70-152">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="ede70-152">Required.</span></span> <span data-ttu-id="ede70-153">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="ede70-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ede70-154">**Konto magazynu**</span><span class="sxs-lookup"><span data-stu-id="ede70-154">**StorageAccount**</span></span>|<span data-ttu-id="ede70-155">Nazwa konta magazynu Azure do przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="ede70-155">The name of the Azure Storage account to store the data in.</span></span> <span data-ttu-id="ede70-156">Można także określić jako parametr podczas wykonywania polecenia cmdlet Set-AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="ede70-156">May also be specified as a parameter when executing the Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="ede70-157">**StorageType**</span><span class="sxs-lookup"><span data-stu-id="ede70-157">**StorageType**</span></span>|<span data-ttu-id="ede70-158">Może być *tabeli*, *obiektu Blob*, lub *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="ede70-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="ede70-159">Tabela jest domyślny.</span><span class="sxs-lookup"><span data-stu-id="ede70-159">Table is default.</span></span> <span data-ttu-id="ede70-160">Po wybraniu TableAndBlob danych diagnostycznych są zapisywane dwukrotnie — raz dla każdego typu.</span><span class="sxs-lookup"><span data-stu-id="ede70-160">When TableAndBlob is chosen, diagnostic data is written twice -- once to each type.</span></span>|  
|<span data-ttu-id="ede70-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="ede70-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="ede70-162">Katalog na maszynie wirtualnej, na którym Agent monitorowania przechowuje dane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="ede70-162">The directory on the virtual machine where the Monitoring Agent stores event data.</span></span> <span data-ttu-id="ede70-163">Jeśli nie, ustawić, jest używany domyślny katalog:</span><span class="sxs-lookup"><span data-stu-id="ede70-163">If not, set, the default directory is used:</span></span><br /><br /> <span data-ttu-id="ede70-164">Dla roli proces roboczy/sieci web:`C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="ede70-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="ede70-165">Dla maszyny wirtualnej:`C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="ede70-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="ede70-166">Atrybuty wymagane są:</span><span class="sxs-lookup"><span data-stu-id="ede70-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="ede70-167">- **ścieżka** -katalogu w systemie mają być używane przez diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="ede70-167">- **path** - The directory on the system to be used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="ede70-168">- **expandEnvironment** — Określa, czy zmienne środowiskowe są rozwijane w nazwie ścieżki.</span><span class="sxs-lookup"><span data-stu-id="ede70-168">- **expandEnvironment** - Controls whether environment variables are expanded in the path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="ede70-169">WadCFG Element</span><span class="sxs-lookup"><span data-stu-id="ede70-169">WadCFG Element</span></span>  
 <span data-ttu-id="ede70-170">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="ede70-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="ede70-171">Identyfikuje i konfiguruje dane telemetryczne, które mają być zbierane.</span><span class="sxs-lookup"><span data-stu-id="ede70-171">Identifies and configures the telemetry data to be collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="ede70-172">DiagnosticMonitorConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="ede70-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="ede70-173">*Drzewa: DiagnosticMonitorConfiguration PublicConfig - WadCFG - głównego - DiagnosticsConfiguration-*</span><span class="sxs-lookup"><span data-stu-id="ede70-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="ede70-174">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ede70-174">Required</span></span> 

|<span data-ttu-id="ede70-175">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="ede70-175">Attributes</span></span>|<span data-ttu-id="ede70-176">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="ede70-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="ede70-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="ede70-178">Maksymalna ilość miejsca na dysku lokalnym, które mogą być używane przez różne rodzaje danych diagnostycznych zebranych przez diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="ede70-178">The maximum amount of local disk space that may be consumed by the various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="ede70-179">Ustawienie domyślne to 5120 MB.</span><span class="sxs-lookup"><span data-stu-id="ede70-179">The default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="ede70-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="ede70-180">**useProxyServer**</span></span> | <span data-ttu-id="ede70-181">Skonfiguruj diagnostyki Azure, aby użyć ustawienia serwera proxy zgodnie z ustawieniami w ustawieniach programu Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="ede70-181">Configure Azure Diagnostics to use the proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="ede70-182">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="ede70-182">Child Elements</span></span>|<span data-ttu-id="ede70-183">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ede70-184">**Zrzutów awaryjnych**</span><span class="sxs-lookup"><span data-stu-id="ede70-184">**CrashDumps**</span></span>|<span data-ttu-id="ede70-185">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="ede70-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ede70-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="ede70-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="ede70-187">Włącz zbieranie dzienników generowanych przez diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="ede70-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="ede70-188">Dzienniki diagnostyczne infrastruktury są przydatne podczas rozwiązywania problemów Diagnostyka system.</span><span class="sxs-lookup"><span data-stu-id="ede70-188">The diagnostic infrastructure logs are useful for troubleshooting the diagnostics system itself.</span></span> <span data-ttu-id="ede70-189">Opcjonalne atrybuty:</span><span class="sxs-lookup"><span data-stu-id="ede70-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="ede70-190">- **scheduledTransferLogLevelFilter** — konfiguruje poziom ważności minimalna dzienników zbierane.</span><span class="sxs-lookup"><span data-stu-id="ede70-190">- **scheduledTransferLogLevelFilter** - Configures the minimum severity level of the logs collected.</span></span><br /><br /> <span data-ttu-id="ede70-191">- **scheduledTransferPeriod** — interwał transferu zaplanowane do magazynu zaokrąglona w górę do najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="ede70-191">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="ede70-192">Wartość jest [XML "Typ danych Duration."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="ede70-192">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="ede70-193">**Katalogi**</span><span class="sxs-lookup"><span data-stu-id="ede70-193">**Directories**</span></span>|<span data-ttu-id="ede70-194">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="ede70-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ede70-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="ede70-195">**EtwProviders**</span></span>|<span data-ttu-id="ede70-196">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="ede70-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ede70-197">**Metryki**</span><span class="sxs-lookup"><span data-stu-id="ede70-197">**Metrics**</span></span>|<span data-ttu-id="ede70-198">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="ede70-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ede70-199">**Liczniki wydajności**</span><span class="sxs-lookup"><span data-stu-id="ede70-199">**PerformanceCounters**</span></span>|<span data-ttu-id="ede70-200">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="ede70-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ede70-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="ede70-201">**WindowsEventLog**</span></span>|<span data-ttu-id="ede70-202">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="ede70-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="ede70-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="ede70-203">**DockerSources**</span></span>|<span data-ttu-id="ede70-204">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="ede70-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="ede70-205">Element zrzutów awaryjnych</span><span class="sxs-lookup"><span data-stu-id="ede70-205">CrashDumps Element</span></span>  
 <span data-ttu-id="ede70-206">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - zrzutów awaryjnych w katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="ede70-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="ede70-207">Włącz zbieranie zrzutów awaryjnych.</span><span class="sxs-lookup"><span data-stu-id="ede70-207">Enable the collection of crash dumps.</span></span>  

|<span data-ttu-id="ede70-208">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="ede70-208">Attributes</span></span>|<span data-ttu-id="ede70-209">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="ede70-210">**Właściwość containerName**</span><span class="sxs-lookup"><span data-stu-id="ede70-210">**containerName**</span></span>|<span data-ttu-id="ede70-211">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="ede70-211">Optional.</span></span> <span data-ttu-id="ede70-212">Nazwa kontenera obiektów blob na koncie magazynu Azure używanego do przechowywania zrzuty awaryjne.</span><span class="sxs-lookup"><span data-stu-id="ede70-212">The name of the blob container in your Azure Storage account to be used to store crash dumps.</span></span>|  
|<span data-ttu-id="ede70-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="ede70-213">**crashDumpType**</span></span>|<span data-ttu-id="ede70-214">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="ede70-214">Optional.</span></span>  <span data-ttu-id="ede70-215">Konfiguruje diagnostyki Azure do zbieranie zrzutów mini lub pełnej awarii.</span><span class="sxs-lookup"><span data-stu-id="ede70-215">Configures Azure Diagnostics to collect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="ede70-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="ede70-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="ede70-217">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="ede70-217">Optional.</span></span>  <span data-ttu-id="ede70-218">Określa procent **overallQuotaInMB** mają zostać zarezerwowane dla zrzuty awaryjne na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ede70-218">Configures the percentage of **overallQuotaInMB** to be reserved for crash dumps on the VM.</span></span>|  

|<span data-ttu-id="ede70-219">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="ede70-219">Child Elements</span></span>|<span data-ttu-id="ede70-220">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ede70-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ede70-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="ede70-222">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="ede70-222">Required.</span></span> <span data-ttu-id="ede70-223">Definiuje wartości konfiguracji dla każdego procesu.</span><span class="sxs-lookup"><span data-stu-id="ede70-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="ede70-224">Następujący atrybut jest również wymagany:</span><span class="sxs-lookup"><span data-stu-id="ede70-224">The following attribute is also required:</span></span><br /><br /> <span data-ttu-id="ede70-225">**Parametr** — nazwa procesu ma diagnostyki Azure, aby zbierać zrzutu awaryjnego dla.</span><span class="sxs-lookup"><span data-stu-id="ede70-225">**processName** - The name of the process you want Azure Diagnostics to collect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="ede70-226">Element katalogów</span><span class="sxs-lookup"><span data-stu-id="ede70-226">Directories Element</span></span> 
 <span data-ttu-id="ede70-227">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - katalogów katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="ede70-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="ede70-228">Umożliwia zbieranie zawartości katalogu, dzienniki żądań dostępu do usług IIS nie powiodło się i/lub dzienniki programu IIS.</span><span class="sxs-lookup"><span data-stu-id="ede70-228">Enables the collection of the contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="ede70-229">Opcjonalne **scheduledTransferPeriod** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="ede70-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="ede70-230">Zawiera wyjaśnienie wcześniej.</span><span class="sxs-lookup"><span data-stu-id="ede70-230">See explanation earlier.</span></span>  

|<span data-ttu-id="ede70-231">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="ede70-231">Child Elements</span></span>|<span data-ttu-id="ede70-232">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ede70-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="ede70-233">**IISLogs**</span></span>|<span data-ttu-id="ede70-234">W tym ten element w konfiguracji umożliwia zbieranie dzienników usług IIS:</span><span class="sxs-lookup"><span data-stu-id="ede70-234">Including this element in the configuration enables the collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="ede70-235">**Właściwość containerName** — nazwa kontenera obiektów blob na koncie magazynu Azure używanego do przechowywania dzienników usług IIS.</span><span class="sxs-lookup"><span data-stu-id="ede70-235">**containerName** - The name of the blob container in your Azure Storage account to be used to store the IIS logs.</span></span>|   
|<span data-ttu-id="ede70-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="ede70-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="ede70-237">W tym ten element w konfiguracji umożliwia zbieranie dzienników dotyczące żądań zakończonych niepowodzeniem do witryny usług IIS lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ede70-237">Including this element in the configuration enables collection of logs about failed requests to an IIS site or application.</span></span> <span data-ttu-id="ede70-238">Należy też włączyć śledzenie opcje w obszarze **systemu. Serwer sieci Web** w **Web.config**.</span><span class="sxs-lookup"><span data-stu-id="ede70-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="ede70-239">**Źródła danych**</span><span class="sxs-lookup"><span data-stu-id="ede70-239">**DataSources**</span></span>|<span data-ttu-id="ede70-240">Lista katalogi do monitorowania.</span><span class="sxs-lookup"><span data-stu-id="ede70-240">A list of directories to monitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="ede70-241">Element źródeł danych</span><span class="sxs-lookup"><span data-stu-id="ede70-241">DataSources Element</span></span>  
 <span data-ttu-id="ede70-242">*Drzewa: Źródła danych PublicConfig - WadCFG - DiagnosticMonitorConfiguration - katalogów - głównego - DiagnosticsConfiguration-*</span><span class="sxs-lookup"><span data-stu-id="ede70-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="ede70-243">Lista katalogi do monitorowania.</span><span class="sxs-lookup"><span data-stu-id="ede70-243">A list of directories to monitor.</span></span>  

|<span data-ttu-id="ede70-244">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="ede70-244">Child Elements</span></span>|<span data-ttu-id="ede70-245">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ede70-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ede70-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="ede70-247">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="ede70-247">Required.</span></span> <span data-ttu-id="ede70-248">Wymagany atrybut:</span><span class="sxs-lookup"><span data-stu-id="ede70-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="ede70-249">**Właściwość containerName** — nazwa kontenera obiektów blob w magazynie Azure konta, które ma być używany do przechowywania plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="ede70-249">**containerName** - The name of the blob container in your Azure Storage account that to be used to store the log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="ede70-250">DirectoryConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="ede70-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="ede70-251">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - katalogów - DataSources — DirectoryConfiguration katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="ede70-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="ede70-252">Może zawierać **bezwzględną** lub **LocalResource** elementu, ale nie oba.</span><span class="sxs-lookup"><span data-stu-id="ede70-252">May include either the **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="ede70-253">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="ede70-253">Child Elements</span></span>|<span data-ttu-id="ede70-254">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ede70-255">**Bezwzględne**</span><span class="sxs-lookup"><span data-stu-id="ede70-255">**Absolute**</span></span>|<span data-ttu-id="ede70-256">Ścieżka bezwzględna do katalogu, do monitorowania.</span><span class="sxs-lookup"><span data-stu-id="ede70-256">The absolute path to the directory to monitor.</span></span> <span data-ttu-id="ede70-257">Wymagane są następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="ede70-257">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="ede70-258">- **Ścieżka** -ścieżka bezwzględna do katalogu, do monitorowania.</span><span class="sxs-lookup"><span data-stu-id="ede70-258">- **Path** - The absolute path to the directory to monitor.</span></span><br /><br /> <span data-ttu-id="ede70-259">- **expandEnvironment** — Określa, czy są rozwinięte zmiennych środowiskowych w ścieżce.</span><span class="sxs-lookup"><span data-stu-id="ede70-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="ede70-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="ede70-260">**LocalResource**</span></span>|<span data-ttu-id="ede70-261">Ścieżka względna zasobu lokalnego do monitorowania.</span><span class="sxs-lookup"><span data-stu-id="ede70-261">The path relative to a local resource to monitor.</span></span> <span data-ttu-id="ede70-262">Atrybuty wymagane są:</span><span class="sxs-lookup"><span data-stu-id="ede70-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="ede70-263">- **Nazwa** -zasób lokalny, zawierająca katalogi do monitorowania</span><span class="sxs-lookup"><span data-stu-id="ede70-263">- **Name** - The local resource that contains the directory to monitor</span></span><br /><br /> <span data-ttu-id="ede70-264">- **relativePath** -ścieżka względna nazwa zawierająca katalogi do monitorowania</span><span class="sxs-lookup"><span data-stu-id="ede70-264">- **relativePath** - The path relative to Name that contains the directory to monitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="ede70-265">EtwProviders Element</span><span class="sxs-lookup"><span data-stu-id="ede70-265">EtwProviders Element</span></span>  
 <span data-ttu-id="ede70-266">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="ede70-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="ede70-267">Zbieranie zdarzeń ETW z EventSource konfiguruje i/lub ETW manifestu na podstawie dostawców.</span><span class="sxs-lookup"><span data-stu-id="ede70-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="ede70-268">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="ede70-268">Child Elements</span></span>|<span data-ttu-id="ede70-269">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ede70-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ede70-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="ede70-271">Konfiguruje zbierania zdarzeń generowanych przez [EventSource — klasa](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="ede70-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="ede70-272">Wymagany atrybut:</span><span class="sxs-lookup"><span data-stu-id="ede70-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="ede70-273">**Dostawca** — Nazwa klasy zdarzenia EventSource.</span><span class="sxs-lookup"><span data-stu-id="ede70-273">**provider** - The class name of the EventSource event.</span></span><br /><br /> <span data-ttu-id="ede70-274">Opcjonalne atrybuty:</span><span class="sxs-lookup"><span data-stu-id="ede70-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="ede70-275">- **scheduledTransferLogLevelFilter** -minimalny poziom ważności na transfer do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ede70-275">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="ede70-276">- **scheduledTransferPeriod** — interwał transferu zaplanowane do magazynu zaokrąglona w górę do najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="ede70-276">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="ede70-277">Wartość jest [XML "Typ danych Duration."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="ede70-277">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="ede70-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ede70-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="ede70-279">Wymagany atrybut:</span><span class="sxs-lookup"><span data-stu-id="ede70-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="ede70-280">**Dostawca** — identyfikator GUID dostawcy zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ede70-280">**provider** - The GUID of the event provider</span></span><br /><br /> <span data-ttu-id="ede70-281">Opcjonalne atrybuty:</span><span class="sxs-lookup"><span data-stu-id="ede70-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="ede70-282">- **scheduledTransferLogLevelFilter** -minimalny poziom ważności na transfer do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ede70-282">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="ede70-283">- **scheduledTransferPeriod** — interwał transferu zaplanowane do magazynu zaokrąglona w górę do najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="ede70-283">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="ede70-284">Wartość jest [XML "Typ danych Duration."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="ede70-284">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="ede70-285">EtwEventSourceProviderConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="ede70-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="ede70-286">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwEventSourceProviderConfiguration katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="ede70-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="ede70-287">Konfiguruje zbierania zdarzeń generowanych przez [EventSource — klasa](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="ede70-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="ede70-288">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="ede70-288">Child Elements</span></span>|<span data-ttu-id="ede70-289">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ede70-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="ede70-290">**DefaultEvents**</span></span>|<span data-ttu-id="ede70-291">Atrybut opcjonalny:</span><span class="sxs-lookup"><span data-stu-id="ede70-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="ede70-292">**eventDestination** — Nazwa tabeli do przechowywania zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ede70-292">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="ede70-293">**Zdarzenie**</span><span class="sxs-lookup"><span data-stu-id="ede70-293">**Event**</span></span>|<span data-ttu-id="ede70-294">Wymagany atrybut:</span><span class="sxs-lookup"><span data-stu-id="ede70-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="ede70-295">**Identyfikator** — identyfikator zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="ede70-295">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="ede70-296">Atrybut opcjonalny:</span><span class="sxs-lookup"><span data-stu-id="ede70-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="ede70-297">**eventDestination** — Nazwa tabeli do przechowywania zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ede70-297">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="ede70-298">EtwManifestProviderConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="ede70-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="ede70-299">*Drzewa: EtwManifestProviderConfiguration PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - głównego - DiagnosticsConfiguration-*</span><span class="sxs-lookup"><span data-stu-id="ede70-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="ede70-300">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="ede70-300">Child Elements</span></span>|<span data-ttu-id="ede70-301">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ede70-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="ede70-302">**DefaultEvents**</span></span>|<span data-ttu-id="ede70-303">Atrybut opcjonalny:</span><span class="sxs-lookup"><span data-stu-id="ede70-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="ede70-304">**eventDestination** — Nazwa tabeli do przechowywania zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ede70-304">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="ede70-305">**Zdarzenie**</span><span class="sxs-lookup"><span data-stu-id="ede70-305">**Event**</span></span>|<span data-ttu-id="ede70-306">Wymagany atrybut:</span><span class="sxs-lookup"><span data-stu-id="ede70-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="ede70-307">**Identyfikator** — identyfikator zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="ede70-307">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="ede70-308">Atrybut opcjonalny:</span><span class="sxs-lookup"><span data-stu-id="ede70-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="ede70-309">**eventDestination** — Nazwa tabeli do przechowywania zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ede70-309">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="ede70-310">Element metryk</span><span class="sxs-lookup"><span data-stu-id="ede70-310">Metrics Element</span></span>  
 <span data-ttu-id="ede70-311">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - metryki katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="ede70-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="ede70-312">Umożliwia generowanie tabeli licznika wydajności, która jest zoptymalizowana pod kątem szybkiego zapytania.</span><span class="sxs-lookup"><span data-stu-id="ede70-312">Enables you to generate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="ede70-313">Każdego licznika wydajności, który jest zdefiniowany w **liczniki wydajności** elementu są przechowywane w tabeli metryki oprócz tabeli licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="ede70-313">Each performance counter that is defined in the **PerformanceCounters** element is stored in the Metrics table in addition to the Performance Counter table.</span></span>  

 <span data-ttu-id="ede70-314">**ResourceId** atrybut jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="ede70-314">The **resourceId** attribute is required.</span></span>  <span data-ttu-id="ede70-315">Identyfikator zasobu wdrażasz diagnostyki Azure do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ede70-315">The resource ID of the Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="ede70-316">Pobierz **resourceID** z [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ede70-316">Get the **resourceID** from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ede70-317">Wybierz **Przeglądaj** -> **grup zasobów** -> **< nazwa\>**.</span><span class="sxs-lookup"><span data-stu-id="ede70-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="ede70-318">Kliknij przycisk **właściwości** Kafelek i skopiuj wartości z **identyfikator** pola.</span><span class="sxs-lookup"><span data-stu-id="ede70-318">Click the **Properties** tile and copy the value from the **ID** field.</span></span>  

|<span data-ttu-id="ede70-319">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="ede70-319">Child Elements</span></span>|<span data-ttu-id="ede70-320">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ede70-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="ede70-321">**MetricAggregation**</span></span>|<span data-ttu-id="ede70-322">Wymagany atrybut:</span><span class="sxs-lookup"><span data-stu-id="ede70-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="ede70-323">**scheduledTransferPeriod** — interwał transferu zaplanowane do magazynu zaokrąglona w górę do najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="ede70-323">**scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="ede70-324">Wartość jest [XML "Typ danych Duration."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="ede70-324">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="ede70-325">PerformanceCounters — Element</span><span class="sxs-lookup"><span data-stu-id="ede70-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="ede70-326">*Drzewa: DiagnosticMonitorConfiguration PublicConfig - WadCFG - głównego - DiagnosticsConfiguration - - liczniki wydajności*</span><span class="sxs-lookup"><span data-stu-id="ede70-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="ede70-327">Umożliwia zbieranie liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="ede70-327">Enables the collection of performance counters.</span></span>  

 <span data-ttu-id="ede70-328">Atrybut opcjonalny:</span><span class="sxs-lookup"><span data-stu-id="ede70-328">Optional attribute:</span></span>  

 <span data-ttu-id="ede70-329">Opcjonalne **scheduledTransferPeriod** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="ede70-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="ede70-330">Zawiera wyjaśnienie wcześniej.</span><span class="sxs-lookup"><span data-stu-id="ede70-330">See explanation earlier.</span></span>

|<span data-ttu-id="ede70-331">Element podrzędny</span><span class="sxs-lookup"><span data-stu-id="ede70-331">Child Element</span></span>|<span data-ttu-id="ede70-332">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="ede70-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ede70-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="ede70-334">Wymagane są następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="ede70-334">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="ede70-335">- **counterSpecifier** — Nazwa licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="ede70-335">- **counterSpecifier** - The name of the performance counter.</span></span> <span data-ttu-id="ede70-336">Na przykład `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="ede70-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="ede70-337">Aby uzyskać listę liczników wydajności na hoście, uruchom polecenie `typeperf`.</span><span class="sxs-lookup"><span data-stu-id="ede70-337">To get a list of performance counters on your host, run the command `typeperf`.</span></span><br /><br /> <span data-ttu-id="ede70-338">- **sampleRate** -częstotliwość próbkowania licznika.</span><span class="sxs-lookup"><span data-stu-id="ede70-338">- **sampleRate** - How often the counter should be sampled.</span></span><br /><br /> <span data-ttu-id="ede70-339">Atrybut opcjonalny:</span><span class="sxs-lookup"><span data-stu-id="ede70-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="ede70-340">**Jednostka** — jednostka miary licznika.</span><span class="sxs-lookup"><span data-stu-id="ede70-340">**unit** - The unit of measure of the counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="ede70-341">WindowsEventLog Element</span><span class="sxs-lookup"><span data-stu-id="ede70-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="ede70-342">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="ede70-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="ede70-343">Umożliwia zbieranie dzienników zdarzeń systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="ede70-343">Enables the collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="ede70-344">Opcjonalne **scheduledTransferPeriod** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="ede70-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="ede70-345">Zawiera wyjaśnienie wcześniej.</span><span class="sxs-lookup"><span data-stu-id="ede70-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="ede70-346">Element podrzędny</span><span class="sxs-lookup"><span data-stu-id="ede70-346">Child Element</span></span>|<span data-ttu-id="ede70-347">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="ede70-348">**Źródło danych**</span><span class="sxs-lookup"><span data-stu-id="ede70-348">**DataSource**</span></span>|<span data-ttu-id="ede70-349">Dzienniki zdarzeń systemu Windows do zbierania.</span><span class="sxs-lookup"><span data-stu-id="ede70-349">The Windows Event logs to collect.</span></span> <span data-ttu-id="ede70-350">Wymagany atrybut:</span><span class="sxs-lookup"><span data-stu-id="ede70-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="ede70-351">**Nazwa** — Kwerenda XPath opisujące zdarzeń systemu windows, które mają być zbierane.</span><span class="sxs-lookup"><span data-stu-id="ede70-351">**name** - The XPath query describing the windows events to be collected.</span></span> <span data-ttu-id="ede70-352">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ede70-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="ede70-353">W celu gromadzenia wszystkich zdarzeń, określ "*"</span><span class="sxs-lookup"><span data-stu-id="ede70-353">To collect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="ede70-354">Element dzienników</span><span class="sxs-lookup"><span data-stu-id="ede70-354">Logs Element</span></span>  
 <span data-ttu-id="ede70-355">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - dzienniki katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="ede70-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="ede70-356">Przedstawia w wersji 1.0, 1.1.</span><span class="sxs-lookup"><span data-stu-id="ede70-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="ede70-357">Brak w 1.2.</span><span class="sxs-lookup"><span data-stu-id="ede70-357">Missing in 1.2.</span></span> <span data-ttu-id="ede70-358">Dodane ponownie w 1.3.</span><span class="sxs-lookup"><span data-stu-id="ede70-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="ede70-359">Definiuje konfigurację buforu podstawowe dzienników Azure.</span><span class="sxs-lookup"><span data-stu-id="ede70-359">Defines the buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="ede70-360">Atrybut</span><span class="sxs-lookup"><span data-stu-id="ede70-360">Attribute</span></span>|<span data-ttu-id="ede70-361">Typ</span><span class="sxs-lookup"><span data-stu-id="ede70-361">Type</span></span>|<span data-ttu-id="ede70-362">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="ede70-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="ede70-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="ede70-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="ede70-364">**unsignedInt**</span></span>|<span data-ttu-id="ede70-365">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="ede70-365">Optional.</span></span> <span data-ttu-id="ede70-366">Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla określonych danych.</span><span class="sxs-lookup"><span data-stu-id="ede70-366">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="ede70-367">Wartość domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="ede70-367">The default is 0.</span></span>|  
|<span data-ttu-id="ede70-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="ede70-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="ede70-369">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="ede70-369">**string**</span></span>|<span data-ttu-id="ede70-370">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="ede70-370">Optional.</span></span> <span data-ttu-id="ede70-371">Określa minimalny poziom ważności wpisy dziennika, które są przenoszone.</span><span class="sxs-lookup"><span data-stu-id="ede70-371">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="ede70-372">Wartość domyślna to **niezdefiniowane**, który przesyła wszystkie dzienniki.</span><span class="sxs-lookup"><span data-stu-id="ede70-372">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="ede70-373">Inne możliwe wartości (w kolejności od najbardziej do najmniej informacji) to **pełne**, **informacji**, **ostrzeżenie**, **błąd**i **Krytyczne**.</span><span class="sxs-lookup"><span data-stu-id="ede70-373">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="ede70-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="ede70-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="ede70-375">**czas trwania**</span><span class="sxs-lookup"><span data-stu-id="ede70-375">**duration**</span></span>|<span data-ttu-id="ede70-376">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="ede70-376">Optional.</span></span> <span data-ttu-id="ede70-377">Określa interwał między zaplanowane transferów danych, zaokrąglona w górę do najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="ede70-377">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="ede70-378">Wartość domyślna to PT0S.</span><span class="sxs-lookup"><span data-stu-id="ede70-378">The default is PT0S.</span></span>|  
|<span data-ttu-id="ede70-379">**wychwytywanie** dodane w wersji 1.5</span><span class="sxs-lookup"><span data-stu-id="ede70-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="ede70-380">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="ede70-380">**string**</span></span>|<span data-ttu-id="ede70-381">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="ede70-381">Optional.</span></span> <span data-ttu-id="ede70-382">Wskazuje lokalizację odbioru można również wysyłać dane diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="ede70-382">Points to a sink location to also send diagnostic data.</span></span> <span data-ttu-id="ede70-383">Na przykład usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ede70-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="ede70-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="ede70-384">DockerSources</span></span>
 <span data-ttu-id="ede70-385">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="ede70-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="ede70-386">Dodane w 1.9.</span><span class="sxs-lookup"><span data-stu-id="ede70-386">Added in 1.9.</span></span>

|<span data-ttu-id="ede70-387">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="ede70-387">Element Name</span></span>|<span data-ttu-id="ede70-388">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="ede70-389">**Statystyka**</span><span class="sxs-lookup"><span data-stu-id="ede70-389">**Stats**</span></span>|<span data-ttu-id="ede70-390">Informuje system, aby zebrać statystykę dla kontenerów Docker</span><span class="sxs-lookup"><span data-stu-id="ede70-390">Tells the system to collect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="ede70-391">SinksConfig Element</span><span class="sxs-lookup"><span data-stu-id="ede70-391">SinksConfig Element</span></span>  
 <span data-ttu-id="ede70-392">*Drzewa: SinksConfig PublicConfig - WadCFG - głównego - DiagnosticsConfiguration-*</span><span class="sxs-lookup"><span data-stu-id="ede70-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="ede70-393">Lista lokalizacji wysyłanie danych diagnostycznych i konfiguracji skojarzone z tych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="ede70-393">A list of locations to send diagnostics data to and the configuration associated with those locations.</span></span>  

|<span data-ttu-id="ede70-394">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="ede70-394">Element Name</span></span>|<span data-ttu-id="ede70-395">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="ede70-396">**Obiekt sink**</span><span class="sxs-lookup"><span data-stu-id="ede70-396">**Sink**</span></span>|<span data-ttu-id="ede70-397">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="ede70-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="ede70-398">Sink — Element</span><span class="sxs-lookup"><span data-stu-id="ede70-398">Sink Element</span></span>
 <span data-ttu-id="ede70-399">*Drzewa: - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - zbiornika katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="ede70-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="ede70-400">Dodane w wersji 1.5.</span><span class="sxs-lookup"><span data-stu-id="ede70-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="ede70-401">Określa lokalizacje do wysyłania danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="ede70-401">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="ede70-402">Na przykład usługa Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ede70-402">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="ede70-403">Atrybut</span><span class="sxs-lookup"><span data-stu-id="ede70-403">Attribute</span></span>|<span data-ttu-id="ede70-404">Typ</span><span class="sxs-lookup"><span data-stu-id="ede70-404">Type</span></span>|<span data-ttu-id="ede70-405">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="ede70-406">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="ede70-406">**name**</span></span>|<span data-ttu-id="ede70-407">Ciąg</span><span class="sxs-lookup"><span data-stu-id="ede70-407">string</span></span>|<span data-ttu-id="ede70-408">Ciąg identyfikujący sinkname.</span><span class="sxs-lookup"><span data-stu-id="ede70-408">A string identifying the sinkname.</span></span>|  

|<span data-ttu-id="ede70-409">Element</span><span class="sxs-lookup"><span data-stu-id="ede70-409">Element</span></span>|<span data-ttu-id="ede70-410">Typ</span><span class="sxs-lookup"><span data-stu-id="ede70-410">Type</span></span>|<span data-ttu-id="ede70-411">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="ede70-412">**Usługa Application Insights**</span><span class="sxs-lookup"><span data-stu-id="ede70-412">**Application Insights**</span></span>|<span data-ttu-id="ede70-413">Ciąg</span><span class="sxs-lookup"><span data-stu-id="ede70-413">string</span></span>|<span data-ttu-id="ede70-414">Używana tylko wtedy, gdy wysyłanie danych do usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ede70-414">Used only when sending data to Application Insights.</span></span> <span data-ttu-id="ede70-415">Zawiera klucz instrumentacji dla aktywnego konta usługi Application Insights, czy masz dostęp do.</span><span class="sxs-lookup"><span data-stu-id="ede70-415">Contain the Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="ede70-416">**Kanały**</span><span class="sxs-lookup"><span data-stu-id="ede70-416">**Channels**</span></span>|<span data-ttu-id="ede70-417">Ciąg</span><span class="sxs-lookup"><span data-stu-id="ede70-417">string</span></span>|<span data-ttu-id="ede70-418">Po jednej dla każdego dodatkowego filtrowania strumienia, który</span><span class="sxs-lookup"><span data-stu-id="ede70-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="ede70-419">Element kanałów</span><span class="sxs-lookup"><span data-stu-id="ede70-419">Channels Element</span></span>  
 <span data-ttu-id="ede70-420">*Drzewa: Kanały SinksConfig - zbiornika - głównego - DiagnosticsConfiguration - PublicConfig - WadCFG-*</span><span class="sxs-lookup"><span data-stu-id="ede70-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="ede70-421">Dodane w wersji 1.5.</span><span class="sxs-lookup"><span data-stu-id="ede70-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="ede70-422">Definiuje filtry dla strumieni danych dziennika przechodzącej przez zbiorniku.</span><span class="sxs-lookup"><span data-stu-id="ede70-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="ede70-423">Element</span><span class="sxs-lookup"><span data-stu-id="ede70-423">Element</span></span>|<span data-ttu-id="ede70-424">Typ</span><span class="sxs-lookup"><span data-stu-id="ede70-424">Type</span></span>|<span data-ttu-id="ede70-425">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="ede70-426">**Kanał**</span><span class="sxs-lookup"><span data-stu-id="ede70-426">**Channel**</span></span>|<span data-ttu-id="ede70-427">Ciąg</span><span class="sxs-lookup"><span data-stu-id="ede70-427">string</span></span>|<span data-ttu-id="ede70-428">Zobacz opis w innym miejscu na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="ede70-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="ede70-429">Element kanału</span><span class="sxs-lookup"><span data-stu-id="ede70-429">Channel Element</span></span>
 <span data-ttu-id="ede70-430">*Drzewa: Kanały SinksConfig - zbiornika - głównego - DiagnosticsConfiguration - PublicConfig - WadCFG - — kanału*</span><span class="sxs-lookup"><span data-stu-id="ede70-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="ede70-431">Dodane w wersji 1.5.</span><span class="sxs-lookup"><span data-stu-id="ede70-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="ede70-432">Określa lokalizacje do wysyłania danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="ede70-432">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="ede70-433">Na przykład usługa Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ede70-433">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="ede70-434">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="ede70-434">Attributes</span></span>|<span data-ttu-id="ede70-435">Typ</span><span class="sxs-lookup"><span data-stu-id="ede70-435">Type</span></span>|<span data-ttu-id="ede70-436">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="ede70-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="ede70-437">**logLevel**</span></span>|<span data-ttu-id="ede70-438">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="ede70-438">**string**</span></span>|<span data-ttu-id="ede70-439">Określa minimalny poziom ważności wpisy dziennika, które są przenoszone.</span><span class="sxs-lookup"><span data-stu-id="ede70-439">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="ede70-440">Wartość domyślna to **niezdefiniowane**, który przesyła wszystkie dzienniki.</span><span class="sxs-lookup"><span data-stu-id="ede70-440">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="ede70-441">Inne możliwe wartości (w kolejności od najbardziej do najmniej informacji) to **pełne**, **informacji**, **ostrzeżenie**, **błąd**i **Krytyczne**.</span><span class="sxs-lookup"><span data-stu-id="ede70-441">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="ede70-442">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="ede70-442">**name**</span></span>|<span data-ttu-id="ede70-443">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="ede70-443">**string**</span></span>|<span data-ttu-id="ede70-444">Unikatowa nazwa kanału do odwoływania się do</span><span class="sxs-lookup"><span data-stu-id="ede70-444">A unique name of the channel to refer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="ede70-445">PrivateConfig Element</span><span class="sxs-lookup"><span data-stu-id="ede70-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="ede70-446">*Drzewa: PrivateConfig - DiagnosticsConfiguration - katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="ede70-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="ede70-447">Dodany w wersji 1.3.</span><span class="sxs-lookup"><span data-stu-id="ede70-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="ede70-448">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="ede70-448">Optional</span></span>  

 <span data-ttu-id="ede70-449">Przechowuje prywatne informacje szczegółowe konta magazynu (nazwa, klucz i końcowy).</span><span class="sxs-lookup"><span data-stu-id="ede70-449">Stores the private details of the storage account (name, key, and endpoint).</span></span> <span data-ttu-id="ede70-450">Te informacje są wysyłane do maszyny wirtualnej, ale nie można pobrać z niego.</span><span class="sxs-lookup"><span data-stu-id="ede70-450">This information is sent to the virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="ede70-451">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="ede70-451">Child Elements</span></span>|<span data-ttu-id="ede70-452">Opis</span><span class="sxs-lookup"><span data-stu-id="ede70-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ede70-453">**Konto magazynu**</span><span class="sxs-lookup"><span data-stu-id="ede70-453">**StorageAccount**</span></span>|<span data-ttu-id="ede70-454">Konta magazynu do użycia.</span><span class="sxs-lookup"><span data-stu-id="ede70-454">The storage account to use.</span></span> <span data-ttu-id="ede70-455">Następujące atrybuty są wymagane</span><span class="sxs-lookup"><span data-stu-id="ede70-455">The following attributes are required</span></span><br /><br /> <span data-ttu-id="ede70-456">- **Nazwa** — nazwa konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ede70-456">- **name** - The name of the storage account.</span></span><br /><br /> <span data-ttu-id="ede70-457">- **klucz** — klucz do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ede70-457">- **key** - The key to the storage account.</span></span><br /><br /> <span data-ttu-id="ede70-458">- **punkt końcowy** — punkt końcowy do uzyskania dostępu do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ede70-458">- **endpoint** - The endpoint to access the storage account.</span></span> <br /><br /> <span data-ttu-id="ede70-459">-**sasToken** (dodany 1.8.1)-tokenu sygnatury dostępu Współdzielonego, zamiast klucz konta magazynu można określić w prywatnej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ede70-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in the private config.</span></span> <span data-ttu-id="ede70-460">Podany klucz konta magazynu jest ignorowana.</span><span class="sxs-lookup"><span data-stu-id="ede70-460">If provided, the storage account key is ignored.</span></span> <br /><span data-ttu-id="ede70-461">Wymagania dotyczące tokenu sygnatury dostępu Współdzielonego:</span><span class="sxs-lookup"><span data-stu-id="ede70-461">Requirements for the SAS Token:</span></span> <br /><span data-ttu-id="ede70-462">— Obsługuje tylko tokenu sygnatury dostępu Współdzielonego konta</span><span class="sxs-lookup"><span data-stu-id="ede70-462">- Supports account SAS token only</span></span> <br /><span data-ttu-id="ede70-463">- *b*, *t* typów usług są wymagane.</span><span class="sxs-lookup"><span data-stu-id="ede70-463">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="ede70-464">- **, *c*, *u*, *w* uprawnienia są wymagane.</span><span class="sxs-lookup"><span data-stu-id="ede70-464">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="ede70-465">- *c*, *o* typów zasobów są wymagane.</span><span class="sxs-lookup"><span data-stu-id="ede70-465">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="ede70-466">— Obsługuje tylko protokół HTTPS</span><span class="sxs-lookup"><span data-stu-id="ede70-466">- Supports the HTTPS protocol only</span></span> <br /> <span data-ttu-id="ede70-467">-Start i czas wygaśnięcia musi być prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="ede70-467">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="ede70-468">IsEnabled Element</span><span class="sxs-lookup"><span data-stu-id="ede70-468">IsEnabled Element</span></span>  
 <span data-ttu-id="ede70-469">*Drzewa: IsEnabled - DiagnosticsConfiguration - katalogu głównego*</span><span class="sxs-lookup"><span data-stu-id="ede70-469">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="ede70-470">Wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="ede70-470">Boolean.</span></span> <span data-ttu-id="ede70-471">Użyj `true` umożliwiające diagnostyki lub `false` wyłączyć diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="ede70-471">Use `true` to enable the diagnostics or `false` to disable the diagnostics.</span></span>
