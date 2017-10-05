---
title: Schemat konfiguracji diagnostyki Azure 1.0 | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: a8fdfb52d5091d3fc9779657737c7430fcfada51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="be21f-103">Schemat konfiguracji diagnostyki Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="be21f-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="be21f-104">Diagnostyka Azure jest używane do zbierania liczników wydajności i innych danych statystycznych z maszyn wirtualnych platformy Azure, zestawy skalowania maszyn wirtualnych, sieci szkieletowej usług i usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="be21f-104">Azure Diagnostics is the component used to collect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="be21f-105">Ta strona jest tylko istotne, jeśli używasz tych usług.</span><span class="sxs-lookup"><span data-stu-id="be21f-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="be21f-106">Diagnostyka Azure jest używana z innymi produktami firmy Microsoft diagnostyki, takich jak Azure monitora, usługi Application Insights i analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="be21f-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="be21f-107">Plik konfiguracji diagnostyki Azure definiuje wartości, które są używane do zainicjowania monitora diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="be21f-107">The Azure Diagnostics configuration file defines values that are used to initialize the Diagnostics Monitor.</span></span> <span data-ttu-id="be21f-108">Ten plik służy do inicjowania ustawień diagnostycznych konfiguracji podczas uruchamiania Monitora diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="be21f-108">This file is used to initialize diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

 <span data-ttu-id="be21f-109">Domyślnie plik schematu konfiguracji diagnostyki Azure jest instalowany na `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` katalogu.</span><span class="sxs-lookup"><span data-stu-id="be21f-109">By default, the Azure Diagnostics configuration schema file is installed to the `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="be21f-110">Zastąp `<version>` z zainstalowaną wersją [zestawu Azure SDK](http://www.windowsazure.com/develop/downloads/).</span><span class="sxs-lookup"><span data-stu-id="be21f-110">Replace `<version>` with the installed version of the [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="be21f-111">Plik konfiguracji diagnostyki zazwyczaj jest używany z uruchomienia zadania, które wymagają danych diagnostycznych, które mają być zbierane wcześniej w procesie uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="be21f-111">The diagnostics configuration file is typically used with startup tasks that require diagnostic data to be collected earlier in the startup process.</span></span> <span data-ttu-id="be21f-112">Aby uzyskać więcej informacji o korzystaniu z diagnostyki Azure, zobacz [zbierania danych rejestrowania za pomocą diagnostyki Azure](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span><span class="sxs-lookup"><span data-stu-id="be21f-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="be21f-113">Przykładowy plik konfiguracji diagnostyki</span><span class="sxs-lookup"><span data-stu-id="be21f-113">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="be21f-114">W poniższym przykładzie przedstawiono plik konfiguracji typowych diagnostyki:</span><span class="sxs-lookup"><span data-stu-id="be21f-114">The following example shows a typical diagnostics configuration file:</span></span>  

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

      <!-- These three elements specify the special directories   
           that are set up for the log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories the DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative to a local   
                 resource defined in the service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- The counter specifier is in the same format as the imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- The event log name is in the same format as the imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="be21f-115">Namespace DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="be21f-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="be21f-116">Przestrzeń nazw XML dla pliku konfiguracji diagnostyki jest:</span><span class="sxs-lookup"><span data-stu-id="be21f-116">The XML namespace for the diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="be21f-117">Elementy schematu</span><span class="sxs-lookup"><span data-stu-id="be21f-117">Schema Elements</span></span>  
 <span data-ttu-id="be21f-118">Plik konfiguracji diagnostyki obejmuje następujące elementy.</span><span class="sxs-lookup"><span data-stu-id="be21f-118">The diagnostics configuration file includes the following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="be21f-119">DiagnosticMonitorConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="be21f-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="be21f-120">Element najwyższego poziomu w pliku konfiguracji diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="be21f-120">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="be21f-121">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="be21f-121">Attributes:</span></span>

|<span data-ttu-id="be21f-122">Atrybut</span><span class="sxs-lookup"><span data-stu-id="be21f-122">Attribute</span></span>  |<span data-ttu-id="be21f-123">Typ</span><span class="sxs-lookup"><span data-stu-id="be21f-123">Type</span></span>   |<span data-ttu-id="be21f-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="be21f-124">Required</span></span>| <span data-ttu-id="be21f-125">Domyślne</span><span class="sxs-lookup"><span data-stu-id="be21f-125">Default</span></span> | <span data-ttu-id="be21f-126">Opis</span><span class="sxs-lookup"><span data-stu-id="be21f-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="be21f-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="be21f-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="be21f-128">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="be21f-128">duration</span></span>|<span data-ttu-id="be21f-129">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="be21f-129">Optional</span></span> | <span data-ttu-id="be21f-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="be21f-130">PT1M</span></span>| <span data-ttu-id="be21f-131">Określa interwał, jaką monitor diagnostyczny sonduje zmiany konfiguracji diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="be21f-131">Specifies the interval at which the diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="be21f-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="be21f-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="be21f-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="be21f-133">unsignedInt</span></span>|<span data-ttu-id="be21f-134">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="be21f-134">Optional</span></span>| <span data-ttu-id="be21f-135">4000 MB.</span><span class="sxs-lookup"><span data-stu-id="be21f-135">4000 MB.</span></span> <span data-ttu-id="be21f-136">Jeżeli określona wartość nie może przekraczać tę wartość</span><span class="sxs-lookup"><span data-stu-id="be21f-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="be21f-137">Łączną ilość przydzielonego na wszystkie bufory rejestrowania magazyn systemu plików.</span><span class="sxs-lookup"><span data-stu-id="be21f-137">The total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="be21f-138">DiagnosticInfrastructureLogs Element</span><span class="sxs-lookup"><span data-stu-id="be21f-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="be21f-139">Definiuje konfigurację buforu dzienników, które są generowane przez podstawowej infrastruktury diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="be21f-139">Defines the buffer configuration for the logs that are generated by the underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="be21f-140">Element nadrzędny: [DiagnosticMonitorConfiguration elementu](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="be21f-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="be21f-141">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="be21f-141">Attributes:</span></span>

|<span data-ttu-id="be21f-142">Atrybut</span><span class="sxs-lookup"><span data-stu-id="be21f-142">Attribute</span></span>|<span data-ttu-id="be21f-143">Typ</span><span class="sxs-lookup"><span data-stu-id="be21f-143">Type</span></span>|<span data-ttu-id="be21f-144">Opis</span><span class="sxs-lookup"><span data-stu-id="be21f-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="be21f-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="be21f-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="be21f-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="be21f-146">unsignedInt</span></span>|<span data-ttu-id="be21f-147">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="be21f-147">Optional.</span></span> <span data-ttu-id="be21f-148">Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla określonych danych.</span><span class="sxs-lookup"><span data-stu-id="be21f-148">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="be21f-149">Wartość domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="be21f-149">The default is 0.</span></span>|  
|<span data-ttu-id="be21f-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="be21f-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="be21f-151">Ciąg</span><span class="sxs-lookup"><span data-stu-id="be21f-151">string</span></span>|<span data-ttu-id="be21f-152">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="be21f-152">Optional.</span></span> <span data-ttu-id="be21f-153">Określa minimalny poziom ważności wpisy dziennika, które są przenoszone.</span><span class="sxs-lookup"><span data-stu-id="be21f-153">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="be21f-154">Wartość domyślna to **niezdefiniowane**.</span><span class="sxs-lookup"><span data-stu-id="be21f-154">The default value is **Undefined**.</span></span> <span data-ttu-id="be21f-155">Inne możliwe wartości to **pełne**, **informacji**, **ostrzeżenie**, **błąd**, i **krytyczny**.</span><span class="sxs-lookup"><span data-stu-id="be21f-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="be21f-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="be21f-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="be21f-157">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="be21f-157">duration</span></span>|<span data-ttu-id="be21f-158">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="be21f-158">Optional.</span></span> <span data-ttu-id="be21f-159">Określa interwał między zaplanowane transferów danych, zaokrąglona w górę do najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="be21f-159">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="be21f-160">Wartość domyślna to PT0S.</span><span class="sxs-lookup"><span data-stu-id="be21f-160">The default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="be21f-161">Element dzienników</span><span class="sxs-lookup"><span data-stu-id="be21f-161">Logs Element</span></span>  
 <span data-ttu-id="be21f-162">Definiuje konfigurację buforu podstawowe dzienników Azure.</span><span class="sxs-lookup"><span data-stu-id="be21f-162">Defines the buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="be21f-163">Element nadrzędny: [DiagnosticMonitorConfiguration elementu](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="be21f-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="be21f-164">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="be21f-164">Attributes:</span></span>  

|<span data-ttu-id="be21f-165">Atrybut</span><span class="sxs-lookup"><span data-stu-id="be21f-165">Attribute</span></span>|<span data-ttu-id="be21f-166">Typ</span><span class="sxs-lookup"><span data-stu-id="be21f-166">Type</span></span>|<span data-ttu-id="be21f-167">Opis</span><span class="sxs-lookup"><span data-stu-id="be21f-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="be21f-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="be21f-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="be21f-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="be21f-169">unsignedInt</span></span>|<span data-ttu-id="be21f-170">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="be21f-170">Optional.</span></span> <span data-ttu-id="be21f-171">Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla określonych danych.</span><span class="sxs-lookup"><span data-stu-id="be21f-171">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="be21f-172">Wartość domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="be21f-172">The default is 0.</span></span>|  
|<span data-ttu-id="be21f-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="be21f-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="be21f-174">Ciąg</span><span class="sxs-lookup"><span data-stu-id="be21f-174">string</span></span>|<span data-ttu-id="be21f-175">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="be21f-175">Optional.</span></span> <span data-ttu-id="be21f-176">Określa minimalny poziom ważności wpisy dziennika, które są przenoszone.</span><span class="sxs-lookup"><span data-stu-id="be21f-176">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="be21f-177">Wartość domyślna to **niezdefiniowane**.</span><span class="sxs-lookup"><span data-stu-id="be21f-177">The default value is **Undefined**.</span></span> <span data-ttu-id="be21f-178">Inne możliwe wartości to **pełne**, **informacji**, **ostrzeżenie**, **błąd**, i **krytyczny**.</span><span class="sxs-lookup"><span data-stu-id="be21f-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="be21f-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="be21f-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="be21f-180">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="be21f-180">duration</span></span>|<span data-ttu-id="be21f-181">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="be21f-181">Optional.</span></span> <span data-ttu-id="be21f-182">Określa interwał między zaplanowane transferów danych, zaokrąglona w górę do najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="be21f-182">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="be21f-183">Wartość domyślna to PT0S.</span><span class="sxs-lookup"><span data-stu-id="be21f-183">The default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="be21f-184">Element katalogów</span><span class="sxs-lookup"><span data-stu-id="be21f-184">Directories Element</span></span>  
<span data-ttu-id="be21f-185">Definiuje konfigurację buforu dla opartych na plikach dzienników zdefiniowanych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="be21f-185">Defines the buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="be21f-186">Element nadrzędny: [DiagnosticMonitorConfiguration elementu](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="be21f-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="be21f-187">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="be21f-187">Attributes:</span></span>  

|<span data-ttu-id="be21f-188">Atrybut</span><span class="sxs-lookup"><span data-stu-id="be21f-188">Attribute</span></span>|<span data-ttu-id="be21f-189">Typ</span><span class="sxs-lookup"><span data-stu-id="be21f-189">Type</span></span>|<span data-ttu-id="be21f-190">Opis</span><span class="sxs-lookup"><span data-stu-id="be21f-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="be21f-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="be21f-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="be21f-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="be21f-192">unsignedInt</span></span>|<span data-ttu-id="be21f-193">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="be21f-193">Optional.</span></span> <span data-ttu-id="be21f-194">Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla określonych danych.</span><span class="sxs-lookup"><span data-stu-id="be21f-194">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="be21f-195">Wartość domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="be21f-195">The default is 0.</span></span>|  
|<span data-ttu-id="be21f-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="be21f-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="be21f-197">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="be21f-197">duration</span></span>|<span data-ttu-id="be21f-198">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="be21f-198">Optional.</span></span> <span data-ttu-id="be21f-199">Określa interwał między zaplanowane transferów danych, zaokrąglona w górę do najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="be21f-199">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="be21f-200">Wartość domyślna to PT0S.</span><span class="sxs-lookup"><span data-stu-id="be21f-200">The default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="be21f-201">Element zrzutów awaryjnych</span><span class="sxs-lookup"><span data-stu-id="be21f-201">CrashDumps Element</span></span>  
 <span data-ttu-id="be21f-202">Określa katalog zrzuty awaryjne.</span><span class="sxs-lookup"><span data-stu-id="be21f-202">Defines the crash dumps directory.</span></span>

 <span data-ttu-id="be21f-203">Element nadrzędny: [Element katalogów](#Directories).</span><span class="sxs-lookup"><span data-stu-id="be21f-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="be21f-204">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="be21f-204">Attributes:</span></span>  

|<span data-ttu-id="be21f-205">Atrybut</span><span class="sxs-lookup"><span data-stu-id="be21f-205">Attribute</span></span>|<span data-ttu-id="be21f-206">Typ</span><span class="sxs-lookup"><span data-stu-id="be21f-206">Type</span></span>|<span data-ttu-id="be21f-207">Opis</span><span class="sxs-lookup"><span data-stu-id="be21f-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="be21f-208">**kontener**</span><span class="sxs-lookup"><span data-stu-id="be21f-208">**container**</span></span>|<span data-ttu-id="be21f-209">Ciąg</span><span class="sxs-lookup"><span data-stu-id="be21f-209">string</span></span>|<span data-ttu-id="be21f-210">Nazwa kontenera, w którym ma zostać przeniesiony zawartość katalogu.</span><span class="sxs-lookup"><span data-stu-id="be21f-210">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="be21f-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="be21f-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="be21f-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="be21f-212">unsignedInt</span></span>|<span data-ttu-id="be21f-213">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="be21f-213">Optional.</span></span> <span data-ttu-id="be21f-214">Określa maksymalny rozmiar katalogu w megabajtach.</span><span class="sxs-lookup"><span data-stu-id="be21f-214">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="be21f-215">Wartość domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="be21f-215">The default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="be21f-216">FailedRequestLogs Element</span><span class="sxs-lookup"><span data-stu-id="be21f-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="be21f-217">Określa katalog dziennika nie powiodło się żądanie.</span><span class="sxs-lookup"><span data-stu-id="be21f-217">Defines the failed request log directory.</span></span>

 <span data-ttu-id="be21f-218">Element nadrzędny elementu [Element katalogów](#Directories).</span><span class="sxs-lookup"><span data-stu-id="be21f-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="be21f-219">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="be21f-219">Attributes:</span></span>  

|<span data-ttu-id="be21f-220">Atrybut</span><span class="sxs-lookup"><span data-stu-id="be21f-220">Attribute</span></span>|<span data-ttu-id="be21f-221">Typ</span><span class="sxs-lookup"><span data-stu-id="be21f-221">Type</span></span>|<span data-ttu-id="be21f-222">Opis</span><span class="sxs-lookup"><span data-stu-id="be21f-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="be21f-223">**kontener**</span><span class="sxs-lookup"><span data-stu-id="be21f-223">**container**</span></span>|<span data-ttu-id="be21f-224">Ciąg</span><span class="sxs-lookup"><span data-stu-id="be21f-224">string</span></span>|<span data-ttu-id="be21f-225">Nazwa kontenera, w którym ma zostać przeniesiony zawartość katalogu.</span><span class="sxs-lookup"><span data-stu-id="be21f-225">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="be21f-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="be21f-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="be21f-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="be21f-227">unsignedInt</span></span>|<span data-ttu-id="be21f-228">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="be21f-228">Optional.</span></span> <span data-ttu-id="be21f-229">Określa maksymalny rozmiar katalogu w megabajtach.</span><span class="sxs-lookup"><span data-stu-id="be21f-229">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="be21f-230">Wartość domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="be21f-230">The default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="be21f-231">IISLogs Element</span><span class="sxs-lookup"><span data-stu-id="be21f-231">IISLogs Element</span></span>  
 <span data-ttu-id="be21f-232">Określa katalog dziennika usług IIS.</span><span class="sxs-lookup"><span data-stu-id="be21f-232">Defines the IIS log directory.</span></span>

 <span data-ttu-id="be21f-233">Element nadrzędny elementu [Element katalogów](#Directories).</span><span class="sxs-lookup"><span data-stu-id="be21f-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="be21f-234">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="be21f-234">Attributes:</span></span>  

|<span data-ttu-id="be21f-235">Atrybut</span><span class="sxs-lookup"><span data-stu-id="be21f-235">Attribute</span></span>|<span data-ttu-id="be21f-236">Typ</span><span class="sxs-lookup"><span data-stu-id="be21f-236">Type</span></span>|<span data-ttu-id="be21f-237">Opis</span><span class="sxs-lookup"><span data-stu-id="be21f-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="be21f-238">**kontener**</span><span class="sxs-lookup"><span data-stu-id="be21f-238">**container**</span></span>|<span data-ttu-id="be21f-239">Ciąg</span><span class="sxs-lookup"><span data-stu-id="be21f-239">string</span></span>|<span data-ttu-id="be21f-240">Nazwa kontenera, w którym ma zostać przeniesiony zawartość katalogu.</span><span class="sxs-lookup"><span data-stu-id="be21f-240">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="be21f-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="be21f-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="be21f-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="be21f-242">unsignedInt</span></span>|<span data-ttu-id="be21f-243">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="be21f-243">Optional.</span></span> <span data-ttu-id="be21f-244">Określa maksymalny rozmiar katalogu w megabajtach.</span><span class="sxs-lookup"><span data-stu-id="be21f-244">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="be21f-245">Wartość domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="be21f-245">The default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="be21f-246">Element źródeł danych</span><span class="sxs-lookup"><span data-stu-id="be21f-246">DataSources Element</span></span>  
 <span data-ttu-id="be21f-247">Definiuje zero lub więcej katalogów dodatkowe dziennika.</span><span class="sxs-lookup"><span data-stu-id="be21f-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="be21f-248">Element nadrzędny: [Element katalogów](#Directories).</span><span class="sxs-lookup"><span data-stu-id="be21f-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="be21f-249">DirectoryConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="be21f-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="be21f-250">Określa katalog plików dziennika do monitorowania.</span><span class="sxs-lookup"><span data-stu-id="be21f-250">Defines the directory of log files to monitor.</span></span>

 <span data-ttu-id="be21f-251">Element nadrzędny: [źródeł danych elementu](#DataSources).</span><span class="sxs-lookup"><span data-stu-id="be21f-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="be21f-252">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="be21f-252">Attributes:</span></span>

|<span data-ttu-id="be21f-253">Atrybut</span><span class="sxs-lookup"><span data-stu-id="be21f-253">Attribute</span></span>|<span data-ttu-id="be21f-254">Typ</span><span class="sxs-lookup"><span data-stu-id="be21f-254">Type</span></span>|<span data-ttu-id="be21f-255">Opis</span><span class="sxs-lookup"><span data-stu-id="be21f-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="be21f-256">**kontener**</span><span class="sxs-lookup"><span data-stu-id="be21f-256">**container**</span></span>|<span data-ttu-id="be21f-257">Ciąg</span><span class="sxs-lookup"><span data-stu-id="be21f-257">string</span></span>|<span data-ttu-id="be21f-258">Nazwa kontenera, w którym ma zostać przeniesiony zawartość katalogu.</span><span class="sxs-lookup"><span data-stu-id="be21f-258">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="be21f-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="be21f-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="be21f-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="be21f-260">unsignedInt</span></span>|<span data-ttu-id="be21f-261">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="be21f-261">Optional.</span></span> <span data-ttu-id="be21f-262">Określa maksymalny rozmiar katalogu w megabajtach.</span><span class="sxs-lookup"><span data-stu-id="be21f-262">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="be21f-263">Wartość domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="be21f-263">The default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="be21f-264">Element bezwzględne</span><span class="sxs-lookup"><span data-stu-id="be21f-264">Absolute Element</span></span>  
 <span data-ttu-id="be21f-265">Określa ścieżkę bezwzględną katalogu można monitorować za pomocą środowiska opcjonalne rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="be21f-265">Defines an absolute path of the directory to monitor with optional environment expansion.</span></span>

 <span data-ttu-id="be21f-266">Element nadrzędny: [DirectoryConfiguration elementu](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="be21f-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="be21f-267">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="be21f-267">Attributes:</span></span>  

|<span data-ttu-id="be21f-268">Atrybut</span><span class="sxs-lookup"><span data-stu-id="be21f-268">Attribute</span></span>|<span data-ttu-id="be21f-269">Typ</span><span class="sxs-lookup"><span data-stu-id="be21f-269">Type</span></span>|<span data-ttu-id="be21f-270">Opis</span><span class="sxs-lookup"><span data-stu-id="be21f-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="be21f-271">**Ścieżka**</span><span class="sxs-lookup"><span data-stu-id="be21f-271">**path**</span></span>|<span data-ttu-id="be21f-272">Ciąg</span><span class="sxs-lookup"><span data-stu-id="be21f-272">string</span></span>|<span data-ttu-id="be21f-273">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="be21f-273">Required.</span></span> <span data-ttu-id="be21f-274">Ścieżka bezwzględna do katalogu, do monitorowania.</span><span class="sxs-lookup"><span data-stu-id="be21f-274">The absolute path to the directory to monitor.</span></span>|  
|<span data-ttu-id="be21f-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="be21f-275">**expandEnvironment**</span></span>|<span data-ttu-id="be21f-276">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="be21f-276">boolean</span></span>|<span data-ttu-id="be21f-277">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="be21f-277">Required.</span></span> <span data-ttu-id="be21f-278">Jeśli ustawiono **true**, zostaną rozwinięte zmiennych środowiskowych w ścieżce.</span><span class="sxs-lookup"><span data-stu-id="be21f-278">If set to **true**, environment variables in the path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="be21f-279">LocalResource Element</span><span class="sxs-lookup"><span data-stu-id="be21f-279">LocalResource Element</span></span>  
 <span data-ttu-id="be21f-280">Określa ścieżkę względną wobec zasobu lokalnego określona w definicji usługi.</span><span class="sxs-lookup"><span data-stu-id="be21f-280">Defines a path relative to a local resource defined in the service definition.</span></span>

 <span data-ttu-id="be21f-281">Element nadrzędny: [DirectoryConfiguration elementu](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="be21f-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="be21f-282">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="be21f-282">Attributes:</span></span>  

|<span data-ttu-id="be21f-283">Atrybut</span><span class="sxs-lookup"><span data-stu-id="be21f-283">Attribute</span></span>|<span data-ttu-id="be21f-284">Typ</span><span class="sxs-lookup"><span data-stu-id="be21f-284">Type</span></span>|<span data-ttu-id="be21f-285">Opis</span><span class="sxs-lookup"><span data-stu-id="be21f-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="be21f-286">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="be21f-286">**name**</span></span>|<span data-ttu-id="be21f-287">Ciąg</span><span class="sxs-lookup"><span data-stu-id="be21f-287">string</span></span>|<span data-ttu-id="be21f-288">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="be21f-288">Required.</span></span> <span data-ttu-id="be21f-289">Nazwa zasobu lokalnego zawierająca katalogi do monitorowania.</span><span class="sxs-lookup"><span data-stu-id="be21f-289">The name of the local resource that contains the directory to monitor.</span></span>|  
|<span data-ttu-id="be21f-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="be21f-290">**relativePath**</span></span>|<span data-ttu-id="be21f-291">Ciąg</span><span class="sxs-lookup"><span data-stu-id="be21f-291">string</span></span>|<span data-ttu-id="be21f-292">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="be21f-292">Required.</span></span> <span data-ttu-id="be21f-293">Ścieżka względna zasobu lokalnego do monitorowania.</span><span class="sxs-lookup"><span data-stu-id="be21f-293">The path relative to the local resource to monitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="be21f-294">PerformanceCounters — Element</span><span class="sxs-lookup"><span data-stu-id="be21f-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="be21f-295">Określa ścieżkę do wartości licznika wydajności do zbierania.</span><span class="sxs-lookup"><span data-stu-id="be21f-295">Defines the path to the performance counter to collect.</span></span>

 <span data-ttu-id="be21f-296">Element nadrzędny: [DiagnosticMonitorConfiguration elementu](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="be21f-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="be21f-297">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="be21f-297">Attributes:</span></span>  

|<span data-ttu-id="be21f-298">Atrybut</span><span class="sxs-lookup"><span data-stu-id="be21f-298">Attribute</span></span>|<span data-ttu-id="be21f-299">Typ</span><span class="sxs-lookup"><span data-stu-id="be21f-299">Type</span></span>|<span data-ttu-id="be21f-300">Opis</span><span class="sxs-lookup"><span data-stu-id="be21f-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="be21f-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="be21f-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="be21f-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="be21f-302">unsignedInt</span></span>|<span data-ttu-id="be21f-303">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="be21f-303">Optional.</span></span> <span data-ttu-id="be21f-304">Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla określonych danych.</span><span class="sxs-lookup"><span data-stu-id="be21f-304">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="be21f-305">Wartość domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="be21f-305">The default is 0.</span></span>|  
|<span data-ttu-id="be21f-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="be21f-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="be21f-307">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="be21f-307">duration</span></span>|<span data-ttu-id="be21f-308">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="be21f-308">Optional.</span></span> <span data-ttu-id="be21f-309">Określa interwał między zaplanowane transferów danych, zaokrąglona w górę do najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="be21f-309">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="be21f-310">Wartość domyślna to PT0S.</span><span class="sxs-lookup"><span data-stu-id="be21f-310">The default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="be21f-311">PerformanceCounterConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="be21f-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="be21f-312">Określa licznik wydajności do zbierania.</span><span class="sxs-lookup"><span data-stu-id="be21f-312">Defines the performance counter to collect.</span></span>

 <span data-ttu-id="be21f-313">Element nadrzędny: [PerformanceCounters — Element](#PerformanceCounters).</span><span class="sxs-lookup"><span data-stu-id="be21f-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="be21f-314">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="be21f-314">Attributes:</span></span>  

|<span data-ttu-id="be21f-315">Atrybut</span><span class="sxs-lookup"><span data-stu-id="be21f-315">Attribute</span></span>|<span data-ttu-id="be21f-316">Typ</span><span class="sxs-lookup"><span data-stu-id="be21f-316">Type</span></span>|<span data-ttu-id="be21f-317">Opis</span><span class="sxs-lookup"><span data-stu-id="be21f-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="be21f-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="be21f-318">**counterSpecifier**</span></span>|<span data-ttu-id="be21f-319">Ciąg</span><span class="sxs-lookup"><span data-stu-id="be21f-319">string</span></span>|<span data-ttu-id="be21f-320">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="be21f-320">Required.</span></span> <span data-ttu-id="be21f-321">Ścieżka do liczników wydajności do zbierania.</span><span class="sxs-lookup"><span data-stu-id="be21f-321">The path to the performance counter to collect.</span></span>|  
|<span data-ttu-id="be21f-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="be21f-322">**sampleRate**</span></span>|<span data-ttu-id="be21f-323">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="be21f-323">duration</span></span>|<span data-ttu-id="be21f-324">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="be21f-324">Required.</span></span> <span data-ttu-id="be21f-325">Częstotliwość licznika wydajności powinny być zbierane.</span><span class="sxs-lookup"><span data-stu-id="be21f-325">The rate at which the performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="be21f-326">WindowsEventLog Element</span><span class="sxs-lookup"><span data-stu-id="be21f-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="be21f-327">Definiuje dzienniki zdarzeń, aby monitorować.</span><span class="sxs-lookup"><span data-stu-id="be21f-327">Defines the event logs to monitor.</span></span>

 <span data-ttu-id="be21f-328">Element nadrzędny: [DiagnosticMonitorConfiguration elementu](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="be21f-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="be21f-329">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="be21f-329">Attributes:</span></span>

|<span data-ttu-id="be21f-330">Atrybut</span><span class="sxs-lookup"><span data-stu-id="be21f-330">Attribute</span></span>|<span data-ttu-id="be21f-331">Typ</span><span class="sxs-lookup"><span data-stu-id="be21f-331">Type</span></span>|<span data-ttu-id="be21f-332">Opis</span><span class="sxs-lookup"><span data-stu-id="be21f-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="be21f-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="be21f-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="be21f-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="be21f-334">unsignedInt</span></span>|<span data-ttu-id="be21f-335">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="be21f-335">Optional.</span></span> <span data-ttu-id="be21f-336">Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla określonych danych.</span><span class="sxs-lookup"><span data-stu-id="be21f-336">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="be21f-337">Wartość domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="be21f-337">The default is 0.</span></span>|  
|<span data-ttu-id="be21f-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="be21f-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="be21f-339">Ciąg</span><span class="sxs-lookup"><span data-stu-id="be21f-339">string</span></span>|<span data-ttu-id="be21f-340">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="be21f-340">Optional.</span></span> <span data-ttu-id="be21f-341">Określa minimalny poziom ważności wpisy dziennika, które są przenoszone.</span><span class="sxs-lookup"><span data-stu-id="be21f-341">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="be21f-342">Wartość domyślna to **niezdefiniowane**.</span><span class="sxs-lookup"><span data-stu-id="be21f-342">The default value is **Undefined**.</span></span> <span data-ttu-id="be21f-343">Inne możliwe wartości to **pełne**, **informacji**, **ostrzeżenie**, **błąd**, i **krytyczny**.</span><span class="sxs-lookup"><span data-stu-id="be21f-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="be21f-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="be21f-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="be21f-345">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="be21f-345">duration</span></span>|<span data-ttu-id="be21f-346">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="be21f-346">Optional.</span></span> <span data-ttu-id="be21f-347">Określa interwał między zaplanowane transferów danych, zaokrąglona w górę do najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="be21f-347">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="be21f-348">Wartość domyślna to PT0S.</span><span class="sxs-lookup"><span data-stu-id="be21f-348">The default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="be21f-349">DataSource Element</span><span class="sxs-lookup"><span data-stu-id="be21f-349">DataSource Element</span></span>  
 <span data-ttu-id="be21f-350">Definiuje dziennik zdarzeń w celu monitorowania.</span><span class="sxs-lookup"><span data-stu-id="be21f-350">Defines the event log to monitor.</span></span>

 <span data-ttu-id="be21f-351">Element nadrzędny: [WindowsEventLog elementu](#windowsEventLog).</span><span class="sxs-lookup"><span data-stu-id="be21f-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="be21f-352">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="be21f-352">Attributes:</span></span>

|<span data-ttu-id="be21f-353">Atrybut</span><span class="sxs-lookup"><span data-stu-id="be21f-353">Attribute</span></span>|<span data-ttu-id="be21f-354">Typ</span><span class="sxs-lookup"><span data-stu-id="be21f-354">Type</span></span>|<span data-ttu-id="be21f-355">Opis</span><span class="sxs-lookup"><span data-stu-id="be21f-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="be21f-356">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="be21f-356">**name**</span></span>|<span data-ttu-id="be21f-357">Ciąg</span><span class="sxs-lookup"><span data-stu-id="be21f-357">string</span></span>|<span data-ttu-id="be21f-358">Wymagane.</span><span class="sxs-lookup"><span data-stu-id="be21f-358">Required.</span></span> <span data-ttu-id="be21f-359">Wyrażenie XPath, określając dziennika do zbierania.</span><span class="sxs-lookup"><span data-stu-id="be21f-359">An XPath expression specifying the log to collect.</span></span>|  
