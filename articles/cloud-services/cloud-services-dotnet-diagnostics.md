---
title: "toouse aaaHow diagnostycznych platformy Azure (.NET) z usługami w chmurze | Dokumentacja firmy Microsoft"
description: "Za pomocą diagnostyki Azure toogather dane platformy Azure z usługami w chmurze do debugowania, pomiaru wydajności, monitorowania, analizy ruchu sieciowego i inne."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 89623a0e-4e78-4b67-a446-7d19a35a44be
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/22/2017
ms.author: robb
ms.openlocfilehash: 1525eac1e85955d8f05aa21a9805e0a80d0e4bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a><span data-ttu-id="bb166-103">Włączanie diagnostyki Azure usług w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="bb166-103">Enabling Azure Diagnostics in Azure Cloud Services</span></span>
<span data-ttu-id="bb166-104">Zobacz [Omówienie diagnostyki Azure](../azure-diagnostics.md) w tle na diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="bb166-104">See [Azure Diagnostics Overview](../azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-tooenable-diagnostics-in-a-worker-role"></a><span data-ttu-id="bb166-105">Jak tooEnable diagnostyki w roli procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="bb166-105">How tooEnable Diagnostics in a Worker Role</span></span>
<span data-ttu-id="bb166-106">W tym przewodniku opisano, jak tooimplement roli procesu roboczego platformy Azure, który emituje telemetrii danych przy użyciu hello .NET EventSource — klasa.</span><span class="sxs-lookup"><span data-stu-id="bb166-106">This walkthrough describes how tooimplement an Azure worker role that emits telemetry data using hello .NET EventSource class.</span></span> <span data-ttu-id="bb166-107">Diagnostyka Azure jest dane telemetryczne hello toocollect używane i zapisz go w konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bb166-107">Azure Diagnostics is used toocollect hello telemetry data and store it in an Azure storage account.</span></span> <span data-ttu-id="bb166-108">Podczas tworzenia roli procesu roboczego, Visual Studio automatycznie włącza 1.0 diagnostyki jako część rozwiązania hello Azure SDK dla platformy .NET 2.4 i starszych wersji.</span><span class="sxs-lookup"><span data-stu-id="bb166-108">When creating a worker role, Visual Studio automatically enables Diagnostics 1.0 as part of hello solution in Azure SDKs for .NET 2.4 and earlier.</span></span> <span data-ttu-id="bb166-109">Witaj poniższe instrukcje przedstawiają hello proces tworzenia roli procesu roboczego hello, wyłączenie diagnostyki 1.0 z rozwiązania hello i wdrażanie 1.2 diagnostyki lub roli proces roboczy tooyour 1.3.</span><span class="sxs-lookup"><span data-stu-id="bb166-109">hello following instructions describe hello process for creating hello worker role, disabling Diagnostics 1.0 from hello solution, and deploying Diagnostics 1.2 or 1.3 tooyour worker role.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="bb166-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bb166-110">Prerequisites</span></span>
<span data-ttu-id="bb166-111">W tym artykule przyjęto założenie, posiadania subskrypcji platformy Azure i przy użyciu programu Visual Studio z hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="bb166-111">This article assumes you have an Azure subscription and are using Visual Studio with hello Azure SDK.</span></span> <span data-ttu-id="bb166-112">Jeśli nie masz subskrypcji platformy Azure, można utworzysz hello [bezpłatnej wersji próbnej][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="bb166-112">If you do not have an Azure subscription, you can sign up for hello [Free Trial][Free Trial].</span></span> <span data-ttu-id="bb166-113">Upewnij się, że zbyt[Instalowanie i konfigurowanie programu Azure PowerShell w wersji 0.8.7 lub nowszym][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="bb166-113">Make sure too[Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-worker-role"></a><span data-ttu-id="bb166-114">Krok 1: Tworzenie roli procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="bb166-114">Step 1: Create a Worker Role</span></span>
1. <span data-ttu-id="bb166-115">Uruchom program **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="bb166-115">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="bb166-116">Utwórz **usługi w chmurze Azure** projektu z hello **chmury** szablonu, którego celem jest środowisko .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="bb166-116">Create an **Azure Cloud Service** project from hello **Cloud** template that targets .NET Framework 4.5.</span></span>  <span data-ttu-id="bb166-117">Nazwa projektu hello "WadExample", a następnie kliknij przycisk Ok.</span><span class="sxs-lookup"><span data-stu-id="bb166-117">Name hello project "WadExample" and click Ok.</span></span>
3. <span data-ttu-id="bb166-118">Wybierz **roli procesu roboczego** i kliknij przycisk Ok.</span><span class="sxs-lookup"><span data-stu-id="bb166-118">Select **Worker Role** and click Ok.</span></span> <span data-ttu-id="bb166-119">Witaj, projekt zostanie utworzony.</span><span class="sxs-lookup"><span data-stu-id="bb166-119">hello project will be created.</span></span>
4. <span data-ttu-id="bb166-120">W **Eksploratora rozwiązań**, kliknij dwukrotnie hello **WorkerRole1** właściwości pliku.</span><span class="sxs-lookup"><span data-stu-id="bb166-120">In **Solution Explorer**, double-click hello **WorkerRole1** properties file.</span></span>
5. <span data-ttu-id="bb166-121">W hello **konfiguracji** karcie, usuń zaznaczenie **włączyć diagnostyki** toodisable 1.0 diagnostyki Azure SDK (2.4 lub starszej).</span><span class="sxs-lookup"><span data-stu-id="bb166-121">In hello **Configuration** tab, un-check **Enable Diagnostics** toodisable Diagnostics 1.0 (Azure SDK 2.4 and earlier).</span></span>
6. <span data-ttu-id="bb166-122">Tworzenie tooverify Twojego rozwiązania, które użytkownik nie ma błędów.</span><span class="sxs-lookup"><span data-stu-id="bb166-122">Build your solution tooverify that you have no errors.</span></span>

### <a name="step-2-instrument-your-code"></a><span data-ttu-id="bb166-123">Krok 2: Instrumentacja kodu</span><span class="sxs-lookup"><span data-stu-id="bb166-123">Step 2: Instrument your code</span></span>
<span data-ttu-id="bb166-124">Zamień zawartość hello WorkerRole.cs hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="bb166-124">Replace hello contents of WorkerRole.cs with hello following code.</span></span> <span data-ttu-id="bb166-125">Witaj klasy SampleEventSourceWriter, odziedziczone hello [EventSource — klasa][EventSource Class], implementuje cztery metody rejestrowania: **SendEnums**, **MessageMethod** , **SetOther** i **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="bb166-125">hello class SampleEventSourceWriter, inherited from hello [EventSource Class][EventSource Class], implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="bb166-126">Witaj pierwszy parametr toohello **metody WriteEvent** Metoda określa identyfikator hello hello odpowiednie zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="bb166-126">hello first parameter toohello **WriteEvent** method defines hello ID for hello respective event.</span></span> <span data-ttu-id="bb166-127">Hello metoda Run implementuje nieskończoną pętlę, która wywołuje każdą z hello metod rejestrowania w hello **SampleEventSourceWriter** klasy co 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="bb166-127">hello Run method implements an infinite loop that calls each of hello logging methods implemented in hello **SampleEventSourceWriter** class every 10 seconds.</span></span>

```csharp
using Microsoft.WindowsAzure.ServiceRuntime;
using System;
using System.Diagnostics;
using System.Diagnostics.Tracing;
using System.Net;
using System.Threading;

namespace WorkerRole1
{
    sealed class SampleEventSourceWriter : EventSource
    {
        public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums tooint for efficient logging.
        public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
        public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
        public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }

    }

    enum MyColor
    {
        Red,
        Blue,
        Green
    }

    [Flags]
    enum MyFlags
    {
        Flag1 = 1,
        Flag2 = 2,
        Flag3 = 4
    }

    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
            // This is a sample worker implementation. Replace with your logic.
            Trace.TraceInformation("WorkerRole1 entry point called");

            int value = 0;

            while (true)
            {
                Thread.Sleep(10000);
                Trace.TraceInformation("Working");

                // Emit several events every time we go through hello loop
                for (int i = 0; i < 6; i++)
                {
                    SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
                }

                for (int i = 0; i < 3; i++)
                {
                    SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                    SampleEventSourceWriter.Log.SetOther(true, 123456789);
                }

                if (value == int.MaxValue) value = 0;
                SampleEventSourceWriter.Log.HighFreq(value++);
            }
        }

        public override bool OnStart()
        {
            // Set hello maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a><span data-ttu-id="bb166-128">Krok 3: Wdrażanie swojej roli procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="bb166-128">Step 3: Deploy your Worker Role</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. <span data-ttu-id="bb166-129">Wdrażanie procesu roboczego tooAzure roli z poziomu programu Visual Studio, wybierając hello **WadExample** projektu w hello Eksploratora rozwiązań następnie **publikowania** z hello **kompilacji** menu.</span><span class="sxs-lookup"><span data-stu-id="bb166-129">Deploy your worker role tooAzure from within Visual Studio by selecting hello **WadExample** project in hello Solution Explorer then **Publish** from hello **Build** menu.</span></span>
2. <span data-ttu-id="bb166-130">Wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="bb166-130">Choose your subscription.</span></span>
3. <span data-ttu-id="bb166-131">W hello **ustawień publikowania platformy Azure Microsoft** okno dialogowe, wybierz opcję **Utwórz nowy...** .</span><span class="sxs-lookup"><span data-stu-id="bb166-131">In hello **Microsoft Azure Publish Settings** dialog, select **Create New…**.</span></span>
4. <span data-ttu-id="bb166-132">W hello **Tworzenie usługi w chmurze i konto magazynu** okna dialogowego, wprowadź **nazwa** (na przykład "WadExample") i wybierz region lub grupę koligacji.</span><span class="sxs-lookup"><span data-stu-id="bb166-132">In hello **Create Cloud Service and Storage Account** dialog, enter a **Name** (for example, "WadExample") and select a region or affinity group.</span></span>
5. <span data-ttu-id="bb166-133">Zestaw hello **środowiska** za**przemieszczania**.</span><span class="sxs-lookup"><span data-stu-id="bb166-133">Set hello **Environment** too**Staging**.</span></span>
6. <span data-ttu-id="bb166-134">Zmodyfikuj inne **ustawienia** jako odpowiednie i kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="bb166-134">Modify any other **Settings** as appropriate and click **Publish**.</span></span>
7. <span data-ttu-id="bb166-135">Sprawdź, czy po zakończeniu wdrożenia w hello portalu Azure, która usługi w chmurze jest w **systemem** stanu.</span><span class="sxs-lookup"><span data-stu-id="bb166-135">After deployment has completed, verify in hello Azure portal that your cloud service is in a **Running** state.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-hello-extension"></a><span data-ttu-id="bb166-136">Krok 4: Tworzenie pliku konfiguracji diagnostyki i zainstaluj rozszerzenie hello</span><span class="sxs-lookup"><span data-stu-id="bb166-136">Step 4: Create your Diagnostics configuration file and install hello extension</span></span>
1. <span data-ttu-id="bb166-137">Pobierz definicję schematu pliku konfiguracji publicznego hello, wykonując następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="bb166-137">Download hello public configuration file schema definition by executing hello following PowerShell command:</span></span>

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. <span data-ttu-id="bb166-138">Dodaj tooyour pliku XML **WorkerRole1** projektu, klikając prawym przyciskiem myszy na powitania **WorkerRole1** projekt i wybierz **Dodaj** -> **nowy element...**</span><span class="sxs-lookup"><span data-stu-id="bb166-138">Add an XML file tooyour **WorkerRole1** project by right-clicking on hello **WorkerRole1** project and select **Add** -> **New Item…**</span></span><span data-ttu-id="bb166-139"> -> **Visual C# elementów** -> **danych** -> **pliku XML**.</span><span class="sxs-lookup"><span data-stu-id="bb166-139"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="bb166-140">Nadaj nazwę plikowi hello "WadExample.xml".</span><span class="sxs-lookup"><span data-stu-id="bb166-140">Name hello file "WadExample.xml".</span></span>

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. <span data-ttu-id="bb166-142">Skojarz hello WadConfig.xsd z hello pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bb166-142">Associate hello WadConfig.xsd with hello configuration file.</span></span> <span data-ttu-id="bb166-143">Upewnij się, że okno edytora WadExample.xml hello hello okno jest aktywne.</span><span class="sxs-lookup"><span data-stu-id="bb166-143">Make sure hello WadExample.xml editor window is hello active window.</span></span> <span data-ttu-id="bb166-144">Naciśnij klawisz **F4** tooopen hello **właściwości** okna.</span><span class="sxs-lookup"><span data-stu-id="bb166-144">Press **F4** tooopen hello **Properties** window.</span></span> <span data-ttu-id="bb166-145">Kliknij przycisk hello **schematy** właściwości w hello **właściwości** okna.</span><span class="sxs-lookup"><span data-stu-id="bb166-145">Click hello **Schemas** property in hello **Properties** window.</span></span> <span data-ttu-id="bb166-146">Kliknij przycisk hello **...**</span><span class="sxs-lookup"><span data-stu-id="bb166-146">Click hello **…**</span></span> <span data-ttu-id="bb166-147">w hello **schematy** właściwości.</span><span class="sxs-lookup"><span data-stu-id="bb166-147">in hello **Schemas** property.</span></span> <span data-ttu-id="bb166-148">Kliknij przycisk hello **Dodaj...**</span><span class="sxs-lookup"><span data-stu-id="bb166-148">Click hello **Add…**</span></span> <span data-ttu-id="bb166-149">przycisk i przejdź toohello lokalizacji pliku XSD hello i wybierz hello pliku WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="bb166-149">button and navigate toohello location where you saved hello XSD file and select hello file WadConfig.xsd.</span></span> <span data-ttu-id="bb166-150">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="bb166-150">Click **OK**.</span></span>

4. <span data-ttu-id="bb166-151">Zastąp zawartość pliku konfiguracji WadExample.xml hello hello z powitania po XML, a następnie zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="bb166-151">Replace hello contents of hello WadExample.xml configuration file with hello following XML and save hello file.</span></span> <span data-ttu-id="bb166-152">Ten plik konfiguracyjny definiuje kilka toocollect liczników wydajności: jeden dla jednego wykorzystania pamięci i czasu procesora.</span><span class="sxs-lookup"><span data-stu-id="bb166-152">This configuration file defines a couple performance counters toocollect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="bb166-153">Następnie konfiguracji hello definiuje zdarzenia cztery hello odpowiadającego toohello metod w hello SampleEventSourceWriter klasy.</span><span class="sxs-lookup"><span data-stu-id="bb166-153">Then hello configuration defines hello four events corresponding toohello methods in hello SampleEventSourceWriter class.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="25000">
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT1M" unit="bytes"/>
      </PerformanceCounters>
      <EtwProviders>
        <EtwEventSourceProviderConfiguration provider="SampleEventSourceWriter" scheduledTransferPeriod="PT5M">
          <Event id="1" eventDestination="EnumsTable"/>
          <Event id="2" eventDestination="MessageTable"/>
          <Event id="3" eventDestination="SetOtherTable"/>
          <Event id="4" eventDestination="HighFreqTable"/>
          <DefaultEvents eventDestination="DefaultTable" />
        </EtwEventSourceProviderConfiguration>
      </EtwProviders>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```

### <a name="step-5-install-diagnostics-on-your-worker-role"></a><span data-ttu-id="bb166-154">Krok 5: Instalowanie diagnostyki w swojej roli procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="bb166-154">Step 5: Install Diagnostics on your Worker Role</span></span>
<span data-ttu-id="bb166-155">Witaj poleceń cmdlet programu PowerShell do zarządzania diagnostyki dla roli sieci web lub procesu roboczego są: Set-AzureServiceDiagnosticsExtension, Get AzureServiceDiagnosticsExtension i Usuń AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="bb166-155">hello PowerShell cmdlets for managing Diagnostics on a web or worker role are: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension, and Remove-AzureServiceDiagnosticsExtension.</span></span>

1. <span data-ttu-id="bb166-156">Otwórz program Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb166-156">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="bb166-157">Wykonaj hello skryptu tooinstall diagnostyki w swojej roli procesu roboczego (Zastąp *StorageAccountKey* kluczem konta magazynu hello konta magazynu wadexample i *config_path* ze ścieżką hello toohello *WadExample.xml* pliku):</span><span class="sxs-lookup"><span data-stu-id="bb166-157">Execute hello script tooinstall Diagnostics on your worker role (replace *StorageAccountKey* with hello storage account key for your wadexample storage account and *config_path* with hello path toohello *WadExample.xml* file):</span></span>

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="bb166-158">Krok 6: Sprawdź dane telemetryczne</span><span class="sxs-lookup"><span data-stu-id="bb166-158">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="bb166-159">W Visual Studio hello **Eksploratora serwera**, przejdź do konta magazynu wadexample toohello.</span><span class="sxs-lookup"><span data-stu-id="bb166-159">In hello Visual Studio **Server Explorer**, navigate toohello wadexample storage account.</span></span> <span data-ttu-id="bb166-160">Po około pięciu (5) minut była uruchomiona usługa w chmurze hello, powinny pojawić się tabele hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** i **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="bb166-160">After hello cloud service has been running about five (5) minutes, you should see hello tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="bb166-161">Kliknij dwukrotnie jeden z hello tabel tooview hello telemetrii, które zostały zebrane.</span><span class="sxs-lookup"><span data-stu-id="bb166-161">Double-click one of hello tables tooview hello telemetry that has been collected.</span></span>

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="bb166-163">Schemat pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="bb166-163">Configuration File Schema</span></span>
<span data-ttu-id="bb166-164">plik konfiguracji diagnostyki Hello definiuje wartości, które są tooinitialize używanych ustawień diagnostycznych konfiguracji podczas uruchamiania agenta diagnostyki hello.</span><span class="sxs-lookup"><span data-stu-id="bb166-164">hello Diagnostics configuration file defines values that are used tooinitialize diagnostic configuration settings when hello diagnostics agent starts.</span></span> <span data-ttu-id="bb166-165">Zobacz hello [najnowsze odwołanie do schematu](https://msdn.microsoft.com/library/azure/mt634524.aspx) poprawne wartości i przykłady.</span><span class="sxs-lookup"><span data-stu-id="bb166-165">See hello [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="bb166-166">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="bb166-166">Troubleshooting</span></span>
<span data-ttu-id="bb166-167">Jeśli masz problemy, zobacz [Rozwiązywanie problemów z diagnostyki Azure](../azure-diagnostics-troubleshooting.md) Aby uzyskać pomoc dotyczącą typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="bb166-167">If you have trouble, see [Troubleshooting Azure Diagnostics](../azure-diagnostics-troubleshooting.md) for help with common problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb166-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bb166-168">Next Steps</span></span>
<span data-ttu-id="bb166-169">[Zobacz listę pokrewne artykuły diagnostycznych maszyn wirtualnych Azure](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) toochange hello dane są zbierane, rozwiązywanie problemów lub Dowiedz się więcej o diagnostyce ogólnie.</span><span class="sxs-lookup"><span data-stu-id="bb166-169">[See a list of related Azure virtual-machine diagnostic articles](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) toochange hello data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
