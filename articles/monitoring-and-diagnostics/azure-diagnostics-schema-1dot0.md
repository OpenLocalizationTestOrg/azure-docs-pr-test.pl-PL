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
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="27989-103">Schemat konfiguracji diagnostyki Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="27989-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="27989-104">Diagnostyka Azure to liczniki wydajności toocollect używany składnik hello i innych danych statystycznych z maszyn wirtualnych platformy Azure, zestawy skalowania maszyn wirtualnych, sieci szkieletowej usług i usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="27989-104">Azure Diagnostics is hello component used toocollect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="27989-105">Ta strona jest tylko istotne, jeśli używasz tych usług.</span><span class="sxs-lookup"><span data-stu-id="27989-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="27989-106">Diagnostyka Azure jest używana z innymi produktami firmy Microsoft diagnostyki, takich jak Azure monitora, usługi Application Insights i analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="27989-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="27989-107">plik konfiguracji diagnostyki Azure Hello definiuje wartości, które są używane tooinitialize hello Monitor diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="27989-107">hello Azure Diagnostics configuration file defines values that are used tooinitialize hello Diagnostics Monitor.</span></span> <span data-ttu-id="27989-108">Ten plik jest tooinitialize używanych ustawień diagnostycznych konfiguracji diagnostyki hello monitorujący uruchamia.</span><span class="sxs-lookup"><span data-stu-id="27989-108">This file is used tooinitialize diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

 <span data-ttu-id="27989-109">Domyślnie plik schematu konfiguracji diagnostyki Azure hello jest zainstalowana toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` katalogu.</span><span class="sxs-lookup"><span data-stu-id="27989-109">By default, hello Azure Diagnostics configuration schema file is installed toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="27989-110">Zastąp `<version>` z hello zainstalowana wersja hello [zestawu Azure SDK](http://www.windowsazure.com/develop/downloads/).</span><span class="sxs-lookup"><span data-stu-id="27989-110">Replace `<version>` with hello installed version of hello [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="27989-111">plik konfiguracji diagnostyki Hello są zwykle stosowane z uruchomienia zadania, które wymagają toobe danych diagnostycznych zebranych wcześniej w procesie uruchamiania hello.</span><span class="sxs-lookup"><span data-stu-id="27989-111">hello diagnostics configuration file is typically used with startup tasks that require diagnostic data toobe collected earlier in hello startup process.</span></span> <span data-ttu-id="27989-112">Aby uzyskać więcej informacji o korzystaniu z diagnostyki Azure, zobacz [zbierania danych rejestrowania za pomocą diagnostyki Azure](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span><span class="sxs-lookup"><span data-stu-id="27989-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="27989-113">Przykładowy plik konfiguracji diagnostyki hello</span><span class="sxs-lookup"><span data-stu-id="27989-113">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="27989-114">Hello poniższy przykład przedstawia plik diagnostyki typowych konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="27989-114">hello following example shows a typical diagnostics configuration file:</span></span>  

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

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="27989-115">Namespace DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="27989-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="27989-116">przestrzeń nazw XML Hello pliku konfiguracji diagnostyki hello jest:</span><span class="sxs-lookup"><span data-stu-id="27989-116">hello XML namespace for hello diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="27989-117">Elementy schematu</span><span class="sxs-lookup"><span data-stu-id="27989-117">Schema Elements</span></span>  
 <span data-ttu-id="27989-118">plik konfiguracji diagnostyki Hello obejmuje hello następujące elementy.</span><span class="sxs-lookup"><span data-stu-id="27989-118">hello diagnostics configuration file includes hello following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="27989-119">DiagnosticMonitorConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="27989-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="27989-120">element najwyższego poziomu Hello pliku konfiguracyjnego hello diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="27989-120">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="27989-121">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="27989-121">Attributes:</span></span>

|<span data-ttu-id="27989-122">Atrybut</span><span class="sxs-lookup"><span data-stu-id="27989-122">Attribute</span></span>  |<span data-ttu-id="27989-123">Typ</span><span class="sxs-lookup"><span data-stu-id="27989-123">Type</span></span>   |<span data-ttu-id="27989-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="27989-124">Required</span></span>| <span data-ttu-id="27989-125">Domyślne</span><span class="sxs-lookup"><span data-stu-id="27989-125">Default</span></span> | <span data-ttu-id="27989-126">Opis</span><span class="sxs-lookup"><span data-stu-id="27989-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="27989-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="27989-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="27989-128">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="27989-128">duration</span></span>|<span data-ttu-id="27989-129">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="27989-129">Optional</span></span> | <span data-ttu-id="27989-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="27989-130">PT1M</span></span>| <span data-ttu-id="27989-131">Określa interwał hello, w których sond diagnostycznych monitor hello zmian konfiguracji diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="27989-131">Specifies hello interval at which hello diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="27989-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="27989-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="27989-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="27989-133">unsignedInt</span></span>|<span data-ttu-id="27989-134">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="27989-134">Optional</span></span>| <span data-ttu-id="27989-135">4000 MB.</span><span class="sxs-lookup"><span data-stu-id="27989-135">4000 MB.</span></span> <span data-ttu-id="27989-136">Jeżeli określona wartość nie może przekraczać tę wartość</span><span class="sxs-lookup"><span data-stu-id="27989-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="27989-137">Witaj łączną ilość przydzielonego na wszystkie bufory rejestrowania magazyn systemu plików.</span><span class="sxs-lookup"><span data-stu-id="27989-137">hello total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="27989-138">DiagnosticInfrastructureLogs Element</span><span class="sxs-lookup"><span data-stu-id="27989-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="27989-139">Definiuje konfigurację buforu hello hello dzienników, które są generowane przez hello podstawowej infrastruktury diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="27989-139">Defines hello buffer configuration for hello logs that are generated by hello underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="27989-140">Element nadrzędny: [DiagnosticMonitorConfiguration elementu](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="27989-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="27989-141">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="27989-141">Attributes:</span></span>

|<span data-ttu-id="27989-142">Atrybut</span><span class="sxs-lookup"><span data-stu-id="27989-142">Attribute</span></span>|<span data-ttu-id="27989-143">Typ</span><span class="sxs-lookup"><span data-stu-id="27989-143">Type</span></span>|<span data-ttu-id="27989-144">Opis</span><span class="sxs-lookup"><span data-stu-id="27989-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="27989-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="27989-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="27989-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="27989-146">unsignedInt</span></span>|<span data-ttu-id="27989-147">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="27989-147">Optional.</span></span> <span data-ttu-id="27989-148">Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla hello określony hello danych.</span><span class="sxs-lookup"><span data-stu-id="27989-148">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="27989-149">Witaj domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="27989-149">hello default is 0.</span></span>|  
|<span data-ttu-id="27989-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="27989-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="27989-151">Ciąg</span><span class="sxs-lookup"><span data-stu-id="27989-151">string</span></span>|<span data-ttu-id="27989-152">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="27989-152">Optional.</span></span> <span data-ttu-id="27989-153">Określa hello minimalny poziom ważności wpisy dziennika, które są przenoszone.</span><span class="sxs-lookup"><span data-stu-id="27989-153">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="27989-154">Witaj, wartość domyślna to **niezdefiniowane**.</span><span class="sxs-lookup"><span data-stu-id="27989-154">hello default value is **Undefined**.</span></span> <span data-ttu-id="27989-155">Inne możliwe wartości to **pełne**, **informacji**, **ostrzeżenie**, **błąd**, i **krytyczny**.</span><span class="sxs-lookup"><span data-stu-id="27989-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="27989-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="27989-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="27989-157">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="27989-157">duration</span></span>|<span data-ttu-id="27989-158">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="27989-158">Optional.</span></span> <span data-ttu-id="27989-159">Określa interwał hello między zaplanowane transferów danych, zaokrąglona w górę toohello najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="27989-159">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="27989-160">Domyślnie Hello jest PT0S.</span><span class="sxs-lookup"><span data-stu-id="27989-160">hello default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="27989-161">Element dzienników</span><span class="sxs-lookup"><span data-stu-id="27989-161">Logs Element</span></span>  
 <span data-ttu-id="27989-162">Definiuje konfigurację buforu hello podstawowe dzienników Azure.</span><span class="sxs-lookup"><span data-stu-id="27989-162">Defines hello buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="27989-163">Element nadrzędny: [DiagnosticMonitorConfiguration elementu](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="27989-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="27989-164">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="27989-164">Attributes:</span></span>  

|<span data-ttu-id="27989-165">Atrybut</span><span class="sxs-lookup"><span data-stu-id="27989-165">Attribute</span></span>|<span data-ttu-id="27989-166">Typ</span><span class="sxs-lookup"><span data-stu-id="27989-166">Type</span></span>|<span data-ttu-id="27989-167">Opis</span><span class="sxs-lookup"><span data-stu-id="27989-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="27989-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="27989-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="27989-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="27989-169">unsignedInt</span></span>|<span data-ttu-id="27989-170">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="27989-170">Optional.</span></span> <span data-ttu-id="27989-171">Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla hello określony hello danych.</span><span class="sxs-lookup"><span data-stu-id="27989-171">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="27989-172">Witaj domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="27989-172">hello default is 0.</span></span>|  
|<span data-ttu-id="27989-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="27989-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="27989-174">Ciąg</span><span class="sxs-lookup"><span data-stu-id="27989-174">string</span></span>|<span data-ttu-id="27989-175">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="27989-175">Optional.</span></span> <span data-ttu-id="27989-176">Określa hello minimalny poziom ważności wpisy dziennika, które są przenoszone.</span><span class="sxs-lookup"><span data-stu-id="27989-176">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="27989-177">Witaj, wartość domyślna to **niezdefiniowane**.</span><span class="sxs-lookup"><span data-stu-id="27989-177">hello default value is **Undefined**.</span></span> <span data-ttu-id="27989-178">Inne możliwe wartości to **pełne**, **informacji**, **ostrzeżenie**, **błąd**, i **krytyczny**.</span><span class="sxs-lookup"><span data-stu-id="27989-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="27989-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="27989-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="27989-180">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="27989-180">duration</span></span>|<span data-ttu-id="27989-181">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="27989-181">Optional.</span></span> <span data-ttu-id="27989-182">Określa interwał hello między zaplanowane transferów danych, zaokrąglona w górę toohello najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="27989-182">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="27989-183">Domyślnie Hello jest PT0S.</span><span class="sxs-lookup"><span data-stu-id="27989-183">hello default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="27989-184">Element katalogów</span><span class="sxs-lookup"><span data-stu-id="27989-184">Directories Element</span></span>  
<span data-ttu-id="27989-185">Definiuje konfigurację buforu hello opartych na plikach dzienników zdefiniowanych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="27989-185">Defines hello buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="27989-186">Element nadrzędny: [DiagnosticMonitorConfiguration elementu](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="27989-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="27989-187">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="27989-187">Attributes:</span></span>  

|<span data-ttu-id="27989-188">Atrybut</span><span class="sxs-lookup"><span data-stu-id="27989-188">Attribute</span></span>|<span data-ttu-id="27989-189">Typ</span><span class="sxs-lookup"><span data-stu-id="27989-189">Type</span></span>|<span data-ttu-id="27989-190">Opis</span><span class="sxs-lookup"><span data-stu-id="27989-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="27989-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="27989-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="27989-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="27989-192">unsignedInt</span></span>|<span data-ttu-id="27989-193">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="27989-193">Optional.</span></span> <span data-ttu-id="27989-194">Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla hello określony hello danych.</span><span class="sxs-lookup"><span data-stu-id="27989-194">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="27989-195">Witaj domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="27989-195">hello default is 0.</span></span>|  
|<span data-ttu-id="27989-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="27989-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="27989-197">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="27989-197">duration</span></span>|<span data-ttu-id="27989-198">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="27989-198">Optional.</span></span> <span data-ttu-id="27989-199">Określa interwał hello między zaplanowane transferów danych, zaokrąglona w górę toohello najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="27989-199">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="27989-200">Domyślnie Hello jest PT0S.</span><span class="sxs-lookup"><span data-stu-id="27989-200">hello default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="27989-201">Element zrzutów awaryjnych</span><span class="sxs-lookup"><span data-stu-id="27989-201">CrashDumps Element</span></span>  
 <span data-ttu-id="27989-202">Określa katalog zrzuty awaryjne hello.</span><span class="sxs-lookup"><span data-stu-id="27989-202">Defines hello crash dumps directory.</span></span>

 <span data-ttu-id="27989-203">Element nadrzędny: [Element katalogów](#Directories).</span><span class="sxs-lookup"><span data-stu-id="27989-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="27989-204">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="27989-204">Attributes:</span></span>  

|<span data-ttu-id="27989-205">Atrybut</span><span class="sxs-lookup"><span data-stu-id="27989-205">Attribute</span></span>|<span data-ttu-id="27989-206">Typ</span><span class="sxs-lookup"><span data-stu-id="27989-206">Type</span></span>|<span data-ttu-id="27989-207">Opis</span><span class="sxs-lookup"><span data-stu-id="27989-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="27989-208">**kontener**</span><span class="sxs-lookup"><span data-stu-id="27989-208">**container**</span></span>|<span data-ttu-id="27989-209">Ciąg</span><span class="sxs-lookup"><span data-stu-id="27989-209">string</span></span>|<span data-ttu-id="27989-210">Nazwa Hello kontenera hello gdzie hello zawartość katalogu hello jest toobe transferu.</span><span class="sxs-lookup"><span data-stu-id="27989-210">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="27989-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="27989-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="27989-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="27989-212">unsignedInt</span></span>|<span data-ttu-id="27989-213">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="27989-213">Optional.</span></span> <span data-ttu-id="27989-214">Określa maksymalny rozmiar katalogu hello hello w megabajtach.</span><span class="sxs-lookup"><span data-stu-id="27989-214">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="27989-215">Witaj domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="27989-215">hello default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="27989-216">FailedRequestLogs Element</span><span class="sxs-lookup"><span data-stu-id="27989-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="27989-217">Określa katalog dziennika nie powiodło się Żądanie hello.</span><span class="sxs-lookup"><span data-stu-id="27989-217">Defines hello failed request log directory.</span></span>

 <span data-ttu-id="27989-218">Element nadrzędny elementu [Element katalogów](#Directories).</span><span class="sxs-lookup"><span data-stu-id="27989-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="27989-219">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="27989-219">Attributes:</span></span>  

|<span data-ttu-id="27989-220">Atrybut</span><span class="sxs-lookup"><span data-stu-id="27989-220">Attribute</span></span>|<span data-ttu-id="27989-221">Typ</span><span class="sxs-lookup"><span data-stu-id="27989-221">Type</span></span>|<span data-ttu-id="27989-222">Opis</span><span class="sxs-lookup"><span data-stu-id="27989-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="27989-223">**kontener**</span><span class="sxs-lookup"><span data-stu-id="27989-223">**container**</span></span>|<span data-ttu-id="27989-224">Ciąg</span><span class="sxs-lookup"><span data-stu-id="27989-224">string</span></span>|<span data-ttu-id="27989-225">Nazwa Hello kontenera hello gdzie hello zawartość katalogu hello jest toobe transferu.</span><span class="sxs-lookup"><span data-stu-id="27989-225">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="27989-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="27989-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="27989-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="27989-227">unsignedInt</span></span>|<span data-ttu-id="27989-228">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="27989-228">Optional.</span></span> <span data-ttu-id="27989-229">Określa maksymalny rozmiar katalogu hello hello w megabajtach.</span><span class="sxs-lookup"><span data-stu-id="27989-229">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="27989-230">Witaj domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="27989-230">hello default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="27989-231">IISLogs Element</span><span class="sxs-lookup"><span data-stu-id="27989-231">IISLogs Element</span></span>  
 <span data-ttu-id="27989-232">Określa katalog dziennika usług IIS hello.</span><span class="sxs-lookup"><span data-stu-id="27989-232">Defines hello IIS log directory.</span></span>

 <span data-ttu-id="27989-233">Element nadrzędny elementu [Element katalogów](#Directories).</span><span class="sxs-lookup"><span data-stu-id="27989-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="27989-234">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="27989-234">Attributes:</span></span>  

|<span data-ttu-id="27989-235">Atrybut</span><span class="sxs-lookup"><span data-stu-id="27989-235">Attribute</span></span>|<span data-ttu-id="27989-236">Typ</span><span class="sxs-lookup"><span data-stu-id="27989-236">Type</span></span>|<span data-ttu-id="27989-237">Opis</span><span class="sxs-lookup"><span data-stu-id="27989-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="27989-238">**kontener**</span><span class="sxs-lookup"><span data-stu-id="27989-238">**container**</span></span>|<span data-ttu-id="27989-239">Ciąg</span><span class="sxs-lookup"><span data-stu-id="27989-239">string</span></span>|<span data-ttu-id="27989-240">Nazwa Hello kontenera hello gdzie hello zawartość katalogu hello jest toobe transferu.</span><span class="sxs-lookup"><span data-stu-id="27989-240">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="27989-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="27989-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="27989-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="27989-242">unsignedInt</span></span>|<span data-ttu-id="27989-243">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="27989-243">Optional.</span></span> <span data-ttu-id="27989-244">Określa maksymalny rozmiar katalogu hello hello w megabajtach.</span><span class="sxs-lookup"><span data-stu-id="27989-244">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="27989-245">Witaj domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="27989-245">hello default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="27989-246">Element źródeł danych</span><span class="sxs-lookup"><span data-stu-id="27989-246">DataSources Element</span></span>  
 <span data-ttu-id="27989-247">Definiuje zero lub więcej katalogów dodatkowe dziennika.</span><span class="sxs-lookup"><span data-stu-id="27989-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="27989-248">Element nadrzędny: [Element katalogów](#Directories).</span><span class="sxs-lookup"><span data-stu-id="27989-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="27989-249">DirectoryConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="27989-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="27989-250">Określa katalog hello toomonitor plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="27989-250">Defines hello directory of log files toomonitor.</span></span>

 <span data-ttu-id="27989-251">Element nadrzędny: [źródeł danych elementu](#DataSources).</span><span class="sxs-lookup"><span data-stu-id="27989-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="27989-252">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="27989-252">Attributes:</span></span>

|<span data-ttu-id="27989-253">Atrybut</span><span class="sxs-lookup"><span data-stu-id="27989-253">Attribute</span></span>|<span data-ttu-id="27989-254">Typ</span><span class="sxs-lookup"><span data-stu-id="27989-254">Type</span></span>|<span data-ttu-id="27989-255">Opis</span><span class="sxs-lookup"><span data-stu-id="27989-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="27989-256">**kontener**</span><span class="sxs-lookup"><span data-stu-id="27989-256">**container**</span></span>|<span data-ttu-id="27989-257">Ciąg</span><span class="sxs-lookup"><span data-stu-id="27989-257">string</span></span>|<span data-ttu-id="27989-258">Nazwa Hello kontenera hello gdzie hello zawartość katalogu hello jest toobe transferu.</span><span class="sxs-lookup"><span data-stu-id="27989-258">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="27989-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="27989-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="27989-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="27989-260">unsignedInt</span></span>|<span data-ttu-id="27989-261">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="27989-261">Optional.</span></span> <span data-ttu-id="27989-262">Określa maksymalny rozmiar katalogu hello hello w megabajtach.</span><span class="sxs-lookup"><span data-stu-id="27989-262">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="27989-263">Witaj domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="27989-263">hello default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="27989-264">Element bezwzględne</span><span class="sxs-lookup"><span data-stu-id="27989-264">Absolute Element</span></span>  
 <span data-ttu-id="27989-265">Określa ścieżkę bezwzględną hello toomonitor katalogu o rozszerzeniu środowiska opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="27989-265">Defines an absolute path of hello directory toomonitor with optional environment expansion.</span></span>

 <span data-ttu-id="27989-266">Element nadrzędny: [DirectoryConfiguration elementu](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="27989-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="27989-267">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="27989-267">Attributes:</span></span>  

|<span data-ttu-id="27989-268">Atrybut</span><span class="sxs-lookup"><span data-stu-id="27989-268">Attribute</span></span>|<span data-ttu-id="27989-269">Typ</span><span class="sxs-lookup"><span data-stu-id="27989-269">Type</span></span>|<span data-ttu-id="27989-270">Opis</span><span class="sxs-lookup"><span data-stu-id="27989-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="27989-271">**Ścieżka**</span><span class="sxs-lookup"><span data-stu-id="27989-271">**path**</span></span>|<span data-ttu-id="27989-272">Ciąg</span><span class="sxs-lookup"><span data-stu-id="27989-272">string</span></span>|<span data-ttu-id="27989-273">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="27989-273">Required.</span></span> <span data-ttu-id="27989-274">Witaj toomonitor katalogu toohello ścieżkę bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="27989-274">hello absolute path toohello directory toomonitor.</span></span>|  
|<span data-ttu-id="27989-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="27989-275">**expandEnvironment**</span></span>|<span data-ttu-id="27989-276">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="27989-276">boolean</span></span>|<span data-ttu-id="27989-277">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="27989-277">Required.</span></span> <span data-ttu-id="27989-278">Jeśli ustawiona zbyt**true**, zmiennych środowiskowych w ścieżce hello są rozwinięte.</span><span class="sxs-lookup"><span data-stu-id="27989-278">If set too**true**, environment variables in hello path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="27989-279">LocalResource Element</span><span class="sxs-lookup"><span data-stu-id="27989-279">LocalResource Element</span></span>  
 <span data-ttu-id="27989-280">Określa ścieżkę względną tooa zasób lokalny, określona w definicji usługi hello.</span><span class="sxs-lookup"><span data-stu-id="27989-280">Defines a path relative tooa local resource defined in hello service definition.</span></span>

 <span data-ttu-id="27989-281">Element nadrzędny: [DirectoryConfiguration elementu](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="27989-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="27989-282">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="27989-282">Attributes:</span></span>  

|<span data-ttu-id="27989-283">Atrybut</span><span class="sxs-lookup"><span data-stu-id="27989-283">Attribute</span></span>|<span data-ttu-id="27989-284">Typ</span><span class="sxs-lookup"><span data-stu-id="27989-284">Type</span></span>|<span data-ttu-id="27989-285">Opis</span><span class="sxs-lookup"><span data-stu-id="27989-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="27989-286">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="27989-286">**name**</span></span>|<span data-ttu-id="27989-287">Ciąg</span><span class="sxs-lookup"><span data-stu-id="27989-287">string</span></span>|<span data-ttu-id="27989-288">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="27989-288">Required.</span></span> <span data-ttu-id="27989-289">Nazwa Hello hello zasób lokalny, który zawiera toomonitor katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="27989-289">hello name of hello local resource that contains hello directory toomonitor.</span></span>|  
|<span data-ttu-id="27989-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="27989-290">**relativePath**</span></span>|<span data-ttu-id="27989-291">Ciąg</span><span class="sxs-lookup"><span data-stu-id="27989-291">string</span></span>|<span data-ttu-id="27989-292">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="27989-292">Required.</span></span> <span data-ttu-id="27989-293">Witaj toomonitor zasobu lokalnego toohello względną ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="27989-293">hello path relative toohello local resource toomonitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="27989-294">PerformanceCounters — Element</span><span class="sxs-lookup"><span data-stu-id="27989-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="27989-295">Definiuje hello ścieżki toohello wydajności licznika toocollect.</span><span class="sxs-lookup"><span data-stu-id="27989-295">Defines hello path toohello performance counter toocollect.</span></span>

 <span data-ttu-id="27989-296">Element nadrzędny: [DiagnosticMonitorConfiguration elementu](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="27989-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="27989-297">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="27989-297">Attributes:</span></span>  

|<span data-ttu-id="27989-298">Atrybut</span><span class="sxs-lookup"><span data-stu-id="27989-298">Attribute</span></span>|<span data-ttu-id="27989-299">Typ</span><span class="sxs-lookup"><span data-stu-id="27989-299">Type</span></span>|<span data-ttu-id="27989-300">Opis</span><span class="sxs-lookup"><span data-stu-id="27989-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="27989-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="27989-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="27989-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="27989-302">unsignedInt</span></span>|<span data-ttu-id="27989-303">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="27989-303">Optional.</span></span> <span data-ttu-id="27989-304">Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla hello określony hello danych.</span><span class="sxs-lookup"><span data-stu-id="27989-304">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="27989-305">Witaj domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="27989-305">hello default is 0.</span></span>|  
|<span data-ttu-id="27989-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="27989-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="27989-307">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="27989-307">duration</span></span>|<span data-ttu-id="27989-308">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="27989-308">Optional.</span></span> <span data-ttu-id="27989-309">Określa interwał hello między zaplanowane transferów danych, zaokrąglona w górę toohello najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="27989-309">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="27989-310">Domyślnie Hello jest PT0S.</span><span class="sxs-lookup"><span data-stu-id="27989-310">hello default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="27989-311">PerformanceCounterConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="27989-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="27989-312">Definiuje toocollect licznika wydajności hello.</span><span class="sxs-lookup"><span data-stu-id="27989-312">Defines hello performance counter toocollect.</span></span>

 <span data-ttu-id="27989-313">Element nadrzędny: [PerformanceCounters — Element](#PerformanceCounters).</span><span class="sxs-lookup"><span data-stu-id="27989-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="27989-314">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="27989-314">Attributes:</span></span>  

|<span data-ttu-id="27989-315">Atrybut</span><span class="sxs-lookup"><span data-stu-id="27989-315">Attribute</span></span>|<span data-ttu-id="27989-316">Typ</span><span class="sxs-lookup"><span data-stu-id="27989-316">Type</span></span>|<span data-ttu-id="27989-317">Opis</span><span class="sxs-lookup"><span data-stu-id="27989-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="27989-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="27989-318">**counterSpecifier**</span></span>|<span data-ttu-id="27989-319">Ciąg</span><span class="sxs-lookup"><span data-stu-id="27989-319">string</span></span>|<span data-ttu-id="27989-320">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="27989-320">Required.</span></span> <span data-ttu-id="27989-321">Witaj toocollect licznika wydajności toohello ścieżki.</span><span class="sxs-lookup"><span data-stu-id="27989-321">hello path toohello performance counter toocollect.</span></span>|  
|<span data-ttu-id="27989-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="27989-322">**sampleRate**</span></span>|<span data-ttu-id="27989-323">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="27989-323">duration</span></span>|<span data-ttu-id="27989-324">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="27989-324">Required.</span></span> <span data-ttu-id="27989-325">częstotliwość Hello, w których hello powinny być gromadzone dane licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="27989-325">hello rate at which hello performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="27989-326">WindowsEventLog Element</span><span class="sxs-lookup"><span data-stu-id="27989-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="27989-327">Definiuje hello toomonitor dzienniki zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="27989-327">Defines hello event logs toomonitor.</span></span>

 <span data-ttu-id="27989-328">Element nadrzędny: [DiagnosticMonitorConfiguration elementu](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="27989-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="27989-329">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="27989-329">Attributes:</span></span>

|<span data-ttu-id="27989-330">Atrybut</span><span class="sxs-lookup"><span data-stu-id="27989-330">Attribute</span></span>|<span data-ttu-id="27989-331">Typ</span><span class="sxs-lookup"><span data-stu-id="27989-331">Type</span></span>|<span data-ttu-id="27989-332">Opis</span><span class="sxs-lookup"><span data-stu-id="27989-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="27989-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="27989-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="27989-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="27989-334">unsignedInt</span></span>|<span data-ttu-id="27989-335">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="27989-335">Optional.</span></span> <span data-ttu-id="27989-336">Określa maksymalną ilość pamięci systemu plików, która jest dostępna dla hello określony hello danych.</span><span class="sxs-lookup"><span data-stu-id="27989-336">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="27989-337">Witaj domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="27989-337">hello default is 0.</span></span>|  
|<span data-ttu-id="27989-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="27989-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="27989-339">Ciąg</span><span class="sxs-lookup"><span data-stu-id="27989-339">string</span></span>|<span data-ttu-id="27989-340">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="27989-340">Optional.</span></span> <span data-ttu-id="27989-341">Określa hello minimalny poziom ważności wpisy dziennika, które są przenoszone.</span><span class="sxs-lookup"><span data-stu-id="27989-341">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="27989-342">Witaj, wartość domyślna to **niezdefiniowane**.</span><span class="sxs-lookup"><span data-stu-id="27989-342">hello default value is **Undefined**.</span></span> <span data-ttu-id="27989-343">Inne możliwe wartości to **pełne**, **informacji**, **ostrzeżenie**, **błąd**, i **krytyczny**.</span><span class="sxs-lookup"><span data-stu-id="27989-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="27989-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="27989-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="27989-345">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="27989-345">duration</span></span>|<span data-ttu-id="27989-346">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="27989-346">Optional.</span></span> <span data-ttu-id="27989-347">Określa interwał hello między zaplanowane transferów danych, zaokrąglona w górę toohello najbliższej minutę.</span><span class="sxs-lookup"><span data-stu-id="27989-347">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="27989-348">Domyślnie Hello jest PT0S.</span><span class="sxs-lookup"><span data-stu-id="27989-348">hello default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="27989-349">DataSource Element</span><span class="sxs-lookup"><span data-stu-id="27989-349">DataSource Element</span></span>  
 <span data-ttu-id="27989-350">Definiuje hello toomonitor dziennika zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="27989-350">Defines hello event log toomonitor.</span></span>

 <span data-ttu-id="27989-351">Element nadrzędny: [WindowsEventLog elementu](#windowsEventLog).</span><span class="sxs-lookup"><span data-stu-id="27989-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="27989-352">Atrybuty:</span><span class="sxs-lookup"><span data-stu-id="27989-352">Attributes:</span></span>

|<span data-ttu-id="27989-353">Atrybut</span><span class="sxs-lookup"><span data-stu-id="27989-353">Attribute</span></span>|<span data-ttu-id="27989-354">Typ</span><span class="sxs-lookup"><span data-stu-id="27989-354">Type</span></span>|<span data-ttu-id="27989-355">Opis</span><span class="sxs-lookup"><span data-stu-id="27989-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="27989-356">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="27989-356">**name**</span></span>|<span data-ttu-id="27989-357">Ciąg</span><span class="sxs-lookup"><span data-stu-id="27989-357">string</span></span>|<span data-ttu-id="27989-358">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="27989-358">Required.</span></span> <span data-ttu-id="27989-359">Wyrażenie XPath, określając hello toocollect dziennika.</span><span class="sxs-lookup"><span data-stu-id="27989-359">An XPath expression specifying hello log toocollect.</span></span>|  
