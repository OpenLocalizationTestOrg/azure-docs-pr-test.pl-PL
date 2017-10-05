---
title: "Jak używać z usługami w chmurze Azure diagnostics (.NET) | Dokumentacja firmy Microsoft"
description: "Za pomocą diagnostyki Azure zbieranie danych z usług w chmurze Azure dla debugowania, pomiaru wydajności, monitorowania, analizy ruchu sieciowego i inne."
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
ms.openlocfilehash: 333d2f26ce043a167fb84858c8327cb39e868ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a><span data-ttu-id="f378e-103">Włączanie diagnostyki Azure usług w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="f378e-103">Enabling Azure Diagnostics in Azure Cloud Services</span></span>
<span data-ttu-id="f378e-104">Zobacz [Omówienie diagnostyki Azure](../azure-diagnostics.md) w tle na diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="f378e-104">See [Azure Diagnostics Overview](../azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-to-enable-diagnostics-in-a-worker-role"></a><span data-ttu-id="f378e-105">Jak włączyć diagnostyki w roli procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="f378e-105">How to Enable Diagnostics in a Worker Role</span></span>
<span data-ttu-id="f378e-106">W tym przewodniku opisano Implementowanie roli procesu roboczego platformy Azure, który emituje dane telemetryczne za pomocą klasy .NET EventSource.</span><span class="sxs-lookup"><span data-stu-id="f378e-106">This walkthrough describes how to implement an Azure worker role that emits telemetry data using the .NET EventSource class.</span></span> <span data-ttu-id="f378e-107">Diagnostyka Azure służy do zbierania danych telemetrycznych i zapisz go w koncie magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f378e-107">Azure Diagnostics is used to collect the telemetry data and store it in an Azure storage account.</span></span> <span data-ttu-id="f378e-108">Podczas tworzenia roli procesu roboczego, Visual Studio automatycznie włącza 1.0 diagnostyki w ramach rozwiązania w zestawy Azure SDK dla platformy .NET 2.4 i starszych wersji.</span><span class="sxs-lookup"><span data-stu-id="f378e-108">When creating a worker role, Visual Studio automatically enables Diagnostics 1.0 as part of the solution in Azure SDKs for .NET 2.4 and earlier.</span></span> <span data-ttu-id="f378e-109">Poniższe instrukcje opisują proces tworzenia roli procesu roboczego, wyłączenie diagnostyki 1.0 z rozwiązania oraz wdrażanie diagnostyki 1.2 lub 1.3 do swojej roli procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="f378e-109">The following instructions describe the process for creating the worker role, disabling Diagnostics 1.0 from the solution, and deploying Diagnostics 1.2 or 1.3 to your worker role.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f378e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f378e-110">Prerequisites</span></span>
<span data-ttu-id="f378e-111">W tym artykule przyjęto założenie, posiadania subskrypcji platformy Azure i przy użyciu programu Visual Studio z zestawem Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="f378e-111">This article assumes you have an Azure subscription and are using Visual Studio with the Azure SDK.</span></span> <span data-ttu-id="f378e-112">Jeśli nie masz subskrypcji platformy Azure, możesz zarejestrować się w celu [bezpłatnej wersji próbnej][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="f378e-112">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span></span> <span data-ttu-id="f378e-113">Upewnij się, że [Instalowanie i konfigurowanie programu Azure PowerShell w wersji 0.8.7 lub nowszym][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="f378e-113">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-worker-role"></a><span data-ttu-id="f378e-114">Krok 1: Tworzenie roli procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="f378e-114">Step 1: Create a Worker Role</span></span>
1. <span data-ttu-id="f378e-115">Uruchom **programu Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="f378e-115">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="f378e-116">Utwórz **usługi w chmurze Azure** projekt z **chmury** szablonu, którego celem jest środowisko .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="f378e-116">Create an **Azure Cloud Service** project from the **Cloud** template that targets .NET Framework 4.5.</span></span>  <span data-ttu-id="f378e-117">Nazwa projektu "WadExample", a następnie kliknij przycisk Ok.</span><span class="sxs-lookup"><span data-stu-id="f378e-117">Name the project "WadExample" and click Ok.</span></span>
3. <span data-ttu-id="f378e-118">Wybierz **roli procesu roboczego** i kliknij przycisk Ok.</span><span class="sxs-lookup"><span data-stu-id="f378e-118">Select **Worker Role** and click Ok.</span></span> <span data-ttu-id="f378e-119">Projekt zostanie utworzony.</span><span class="sxs-lookup"><span data-stu-id="f378e-119">The project will be created.</span></span>
4. <span data-ttu-id="f378e-120">W **Eksploratora rozwiązań**, kliknij dwukrotnie **WorkerRole1** właściwości pliku.</span><span class="sxs-lookup"><span data-stu-id="f378e-120">In **Solution Explorer**, double-click the **WorkerRole1** properties file.</span></span>
5. <span data-ttu-id="f378e-121">W **konfiguracji** karcie, usuń zaznaczenie **włączyć diagnostyki** wyłączenie 1.0 diagnostyki Azure SDK (2.4 lub starszej).</span><span class="sxs-lookup"><span data-stu-id="f378e-121">In the **Configuration** tab, un-check **Enable Diagnostics** to disable Diagnostics 1.0 (Azure SDK 2.4 and earlier).</span></span>
6. <span data-ttu-id="f378e-122">Skompiluj rozwiązanie, aby zweryfikować, że użytkownik nie ma błędów.</span><span class="sxs-lookup"><span data-stu-id="f378e-122">Build your solution to verify that you have no errors.</span></span>

### <a name="step-2-instrument-your-code"></a><span data-ttu-id="f378e-123">Krok 2: Instrumentacja kodu</span><span class="sxs-lookup"><span data-stu-id="f378e-123">Step 2: Instrument your code</span></span>
<span data-ttu-id="f378e-124">Zastąp zawartość WorkerRole.cs z następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="f378e-124">Replace the contents of WorkerRole.cs with the following code.</span></span> <span data-ttu-id="f378e-125">Odziedziczone po klasie SampleEventSourceWriter, [EventSource — klasa][EventSource Class], implementuje cztery metody rejestrowania: **SendEnums**, **MessageMethod** , **SetOther** i **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="f378e-125">The class SampleEventSourceWriter, inherited from the [EventSource Class][EventSource Class], implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="f378e-126">Pierwszy parametr **metody WriteEvent** Metoda określa identyfikator dla odpowiednich zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="f378e-126">The first parameter to the **WriteEvent** method defines the ID for the respective event.</span></span> <span data-ttu-id="f378e-127">Metoda Run implementuje nieskończoną pętlę, która wywołuje każdą z metod rejestrowania w **SampleEventSourceWriter** klasy co 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="f378e-127">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span></span>

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
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums to int for efficient logging.
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

                // Emit several events every time we go through the loop
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
            // Set the maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a><span data-ttu-id="f378e-128">Krok 3: Wdrażanie swojej roli procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="f378e-128">Step 3: Deploy your Worker Role</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. <span data-ttu-id="f378e-129">Wdrażanie swojej roli procesu roboczego na platformie Azure z poziomu programu Visual Studio, wybierając **WadExample** projekt w Eksploratorze rozwiązań następnie **publikowania** z **kompilacji** menu.</span><span class="sxs-lookup"><span data-stu-id="f378e-129">Deploy your worker role to Azure from within Visual Studio by selecting the **WadExample** project in the Solution Explorer then **Publish** from the **Build** menu.</span></span>
2. <span data-ttu-id="f378e-130">Wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="f378e-130">Choose your subscription.</span></span>
3. <span data-ttu-id="f378e-131">W **ustawień publikowania platformy Azure Microsoft** okno dialogowe, wybierz opcję **Utwórz nowy...** .</span><span class="sxs-lookup"><span data-stu-id="f378e-131">In the **Microsoft Azure Publish Settings** dialog, select **Create New…**.</span></span>
4. <span data-ttu-id="f378e-132">W **Tworzenie usługi w chmurze i konto magazynu** okna dialogowego, wprowadź **nazwa** (na przykład "WadExample") i wybierz region lub grupę koligacji.</span><span class="sxs-lookup"><span data-stu-id="f378e-132">In the **Create Cloud Service and Storage Account** dialog, enter a **Name** (for example, "WadExample") and select a region or affinity group.</span></span>
5. <span data-ttu-id="f378e-133">Ustaw **środowiska** do **przemieszczania**.</span><span class="sxs-lookup"><span data-stu-id="f378e-133">Set the **Environment** to **Staging**.</span></span>
6. <span data-ttu-id="f378e-134">Zmodyfikuj inne **ustawienia** jako odpowiednie i kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="f378e-134">Modify any other **Settings** as appropriate and click **Publish**.</span></span>
7. <span data-ttu-id="f378e-135">Sprawdź, czy po zakończeniu wdrożenia w portalu Azure, która usługi w chmurze jest w **systemem** stanu.</span><span class="sxs-lookup"><span data-stu-id="f378e-135">After deployment has completed, verify in the Azure portal that your cloud service is in a **Running** state.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-the-extension"></a><span data-ttu-id="f378e-136">Krok 4: Tworzenie pliku konfiguracji diagnostyki i zainstaluj rozszerzenie</span><span class="sxs-lookup"><span data-stu-id="f378e-136">Step 4: Create your Diagnostics configuration file and install the extension</span></span>
1. <span data-ttu-id="f378e-137">Pobierz definicję schematu pliku konfiguracji publicznego, wykonując następujące polecenie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f378e-137">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. <span data-ttu-id="f378e-138">Dodawanie pliku XML do Twojej **WorkerRole1** projektu, klikając prawym przyciskiem myszy **WorkerRole1** projekt i wybierz **Dodaj** -> **nowy element...**</span><span class="sxs-lookup"><span data-stu-id="f378e-138">Add an XML file to your **WorkerRole1** project by right-clicking on the **WorkerRole1** project and select **Add** -> **New Item…**</span></span><span data-ttu-id="f378e-139"> -> **Visual C# elementów** -> **danych** -> **pliku XML**.</span><span class="sxs-lookup"><span data-stu-id="f378e-139"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="f378e-140">Nadaj nazwę plikowi "WadExample.xml".</span><span class="sxs-lookup"><span data-stu-id="f378e-140">Name the file "WadExample.xml".</span></span>

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. <span data-ttu-id="f378e-142">Skojarz WadConfig.xsd z pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f378e-142">Associate the WadConfig.xsd with the configuration file.</span></span> <span data-ttu-id="f378e-143">Upewnij się, że okno edytora WadExample.xml jest aktywnym oknem.</span><span class="sxs-lookup"><span data-stu-id="f378e-143">Make sure the WadExample.xml editor window is the active window.</span></span> <span data-ttu-id="f378e-144">Naciśnij klawisz **F4** otworzyć **właściwości** okna.</span><span class="sxs-lookup"><span data-stu-id="f378e-144">Press **F4** to open the **Properties** window.</span></span> <span data-ttu-id="f378e-145">Kliknij przycisk **schematy** właściwości w **właściwości** okna.</span><span class="sxs-lookup"><span data-stu-id="f378e-145">Click the **Schemas** property in the **Properties** window.</span></span> <span data-ttu-id="f378e-146">Kliknij przycisk **...**</span><span class="sxs-lookup"><span data-stu-id="f378e-146">Click the **…**</span></span> <span data-ttu-id="f378e-147">w **schematy** właściwości.</span><span class="sxs-lookup"><span data-stu-id="f378e-147">in the **Schemas** property.</span></span> <span data-ttu-id="f378e-148">Kliknij przycisk **Dodaj...**</span><span class="sxs-lookup"><span data-stu-id="f378e-148">Click the **Add…**</span></span> <span data-ttu-id="f378e-149">przycisk i przejdź do lokalizacji, w której zapisano plik XSD, a następnie wybierz plik WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="f378e-149">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span></span> <span data-ttu-id="f378e-150">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f378e-150">Click **OK**.</span></span>

4. <span data-ttu-id="f378e-151">Zastąp zawartość pliku konfiguracji WadExample.xml następujące XML i Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="f378e-151">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span></span> <span data-ttu-id="f378e-152">Ten plik konfiguracyjny definiuje kilka liczniki wydajności do: jeden dla jednego wykorzystania pamięci i czasu procesora.</span><span class="sxs-lookup"><span data-stu-id="f378e-152">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="f378e-153">Konfiguracja definiuje zdarzenia cztery odpowiadających metod w klasie SampleEventSourceWriter.</span><span class="sxs-lookup"><span data-stu-id="f378e-153">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span></span>

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

### <a name="step-5-install-diagnostics-on-your-worker-role"></a><span data-ttu-id="f378e-154">Krok 5: Instalowanie diagnostyki w swojej roli procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="f378e-154">Step 5: Install Diagnostics on your Worker Role</span></span>
<span data-ttu-id="f378e-155">Polecenia cmdlet programu PowerShell do zarządzania diagnostyki dla roli sieci web lub procesu roboczego są: Set-AzureServiceDiagnosticsExtension, Get AzureServiceDiagnosticsExtension i Usuń AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="f378e-155">The PowerShell cmdlets for managing Diagnostics on a web or worker role are: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension, and Remove-AzureServiceDiagnosticsExtension.</span></span>

1. <span data-ttu-id="f378e-156">Otwórz program Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f378e-156">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="f378e-157">Uruchom skrypt do zainstalowania diagnostyki na swojej roli procesu roboczego (Zastąp *StorageAccountKey* kluczem konta magazynu dla konta magazynu wadexample i *config_path* ze ścieżką do  *WadExample.xml* pliku):</span><span class="sxs-lookup"><span data-stu-id="f378e-157">Execute the script to install Diagnostics on your worker role (replace *StorageAccountKey* with the storage account key for your wadexample storage account and *config_path* with the path to the *WadExample.xml* file):</span></span>

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="f378e-158">Krok 6: Sprawdź dane telemetryczne</span><span class="sxs-lookup"><span data-stu-id="f378e-158">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="f378e-159">W programie Visual Studio **Eksploratora serwera**, przejdź do konta magazynu wadexample.</span><span class="sxs-lookup"><span data-stu-id="f378e-159">In the Visual Studio **Server Explorer**, navigate to the wadexample storage account.</span></span> <span data-ttu-id="f378e-160">Po około pięciu (5) minut działaniu usługi w chmurze, należy wyświetlić tabele **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** i **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="f378e-160">After the cloud service has been running about five (5) minutes, you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="f378e-161">Dwukrotnie kliknij jedną z tabel, aby wyświetlić dane telemetryczne, które zostały zebrane.</span><span class="sxs-lookup"><span data-stu-id="f378e-161">Double-click one of the tables to view the telemetry that has been collected.</span></span>

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="f378e-163">Schemat pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="f378e-163">Configuration File Schema</span></span>
<span data-ttu-id="f378e-164">Plik konfiguracji diagnostyki definiuje wartości, które są używane do inicjowania ustawień diagnostycznych konfiguracji podczas uruchamiania agenta diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="f378e-164">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span></span> <span data-ttu-id="f378e-165">Zobacz [najnowsze odwołanie do schematu](https://msdn.microsoft.com/library/azure/mt634524.aspx) poprawne wartości i przykłady.</span><span class="sxs-lookup"><span data-stu-id="f378e-165">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f378e-166">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="f378e-166">Troubleshooting</span></span>
<span data-ttu-id="f378e-167">Jeśli masz problemy, zobacz [Rozwiązywanie problemów z diagnostyki Azure](../azure-diagnostics-troubleshooting.md) Aby uzyskać pomoc dotyczącą typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="f378e-167">If you have trouble, see [Troubleshooting Azure Diagnostics](../azure-diagnostics-troubleshooting.md) for help with common problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f378e-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f378e-168">Next Steps</span></span>
<span data-ttu-id="f378e-169">[Zobacz listę pokrewne artykuły diagnostycznych maszyn wirtualnych Azure](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) Aby zmienić dane są zbierane, rozwiązywanie problemów, lub Dowiedz się więcej o diagnostyce ogólnie.</span><span class="sxs-lookup"><span data-stu-id="f378e-169">[See a list of related Azure virtual-machine diagnostic articles](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
