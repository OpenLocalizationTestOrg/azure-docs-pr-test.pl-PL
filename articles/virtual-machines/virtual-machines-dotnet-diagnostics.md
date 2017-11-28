---
title: toouse aaaHow diagnostycznych platformy Azure na maszynach wirtualnych | Dokumentacja firmy Microsoft
description: "Przy użyciu diagnostyki Azure toogather danych z maszyn wirtualnych Azure debugowanie, pomiaru wydajności, monitorowania, analizy ruchu sieciowego i inne."
services: virtual-machines
documentationcenter: .net
author: davidmu1
manager: 
editor: 
ms.assetid: dfaabc7a-23e7-4af0-8369-f504d2915b3d
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/16/2016
ms.author: davidmu
ms.openlocfilehash: 54cdfd30d7bbbb71af449826e90234faf5ecdf44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a><span data-ttu-id="f9f17-103">Włączanie diagnostyki w maszynach wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f9f17-103">Enabling Diagnostics in Azure Virtual Machines</span></span>
<span data-ttu-id="f9f17-104">Zobacz [Omówienie diagnostyki Azure](../monitoring-and-diagnostics/azure-diagnostics.md) w tle na diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="f9f17-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a><span data-ttu-id="f9f17-105">Jak tooEnable diagnostyki na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f9f17-105">How tooEnable Diagnostics in a Virtual Machine</span></span>
<span data-ttu-id="f9f17-106">Ta krokach związanych z opisano, jak zainstalować tooremotely tooan diagnostyki maszyny wirtualnej platformy Azure z komputera.</span><span class="sxs-lookup"><span data-stu-id="f9f17-106">This walk through describes how tooremotely install Diagnostics tooan Azure virtual machine from a development computer.</span></span> <span data-ttu-id="f9f17-107">Możesz też dowiedzieć się, jak tooimplement działającą na tej maszynie wirtualnej Azure i emituje telemetrii danych przy użyciu aplikacji hello .NET [EventSource — klasa][EventSource Class].</span><span class="sxs-lookup"><span data-stu-id="f9f17-107">You also learn how tooimplement an application that runs on that Azure virtual machine and emits telemetry data using hello .NET [EventSource Class][EventSource Class].</span></span> <span data-ttu-id="f9f17-108">Diagnostyka Azure hello toocollect używane w danych telemetrycznych i zapisz go w koncie magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f9f17-108">Azure Diagnostics is used toocollect hello telemetry and store it in an Azure storage account.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="f9f17-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f9f17-109">Pre-requisites</span></span>
<span data-ttu-id="f9f17-110">To krokach związanych z zakłada posiadania subskrypcji platformy Azure i za pomocą programu Visual Studio 2017 hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="f9f17-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2017 with hello Azure SDK.</span></span> <span data-ttu-id="f9f17-111">Jeśli nie masz subskrypcji platformy Azure, można utworzysz hello [bezpłatnej wersji próbnej][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="f9f17-111">If you do not have an Azure subscription, you can sign up for hello [Free Trial][Free Trial].</span></span> <span data-ttu-id="f9f17-112">Upewnij się, że zbyt[Instalowanie i konfigurowanie programu Azure PowerShell w wersji 0.8.7 lub nowszym][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="f9f17-112">Make sure too[Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-virtual-machine"></a><span data-ttu-id="f9f17-113">Krok 1: Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f9f17-113">Step 1: Create a Virtual Machine</span></span>
1. <span data-ttu-id="f9f17-114">Na komputerze deweloperskim Uruchom program Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="f9f17-114">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="f9f17-115">W Visual Studio hello **Eksploratora serwera** rozwiń **Azure**, kliknij prawym przyciskiem myszy **maszyn wirtualnych** następnie wybierz **Utwórz maszynę wirtualną**.</span><span class="sxs-lookup"><span data-stu-id="f9f17-115">In hello Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span></span>
3. <span data-ttu-id="f9f17-116">Wybierz subskrypcję platformy Azure w hello **Wybierz subskrypcję** okno dialogowe i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="f9f17-116">Select your Azure subscription in hello **Choose a Subscription** dialog and click **Next**.</span></span>
4. <span data-ttu-id="f9f17-117">Wybierz **systemu Windows Server 2012 R2 Datacenter, 2017 czerwca** w hello **Wybieranie obrazu maszyny wirtualnej** okno dialogowe i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="f9f17-117">Select **Windows Server 2012 R2 Datacenter, June 2017** in hello **Select a Virtual Machine Image** dialog and click **Next**.</span></span>
5. <span data-ttu-id="f9f17-118">W hello **ustawienia podstawowej maszyny wirtualnej**, ustaw nazwę maszyny wirtualnej hello zbyt "wadexample".</span><span class="sxs-lookup"><span data-stu-id="f9f17-118">In hello **Virtual Machine Basic Settings**, set hello virtual machine name too"wadexample".</span></span> <span data-ttu-id="f9f17-119">Ustaw swoją nazwę użytkownika administratora i hasło, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="f9f17-119">Set your Administrator user name and password and click **Next**.</span></span>
6. <span data-ttu-id="f9f17-120">W hello **ustawienia usługi w chmurze** okna dialogowego Utwórz nową usługę w chmurze o nazwie "wadexampleVM".</span><span class="sxs-lookup"><span data-stu-id="f9f17-120">In hello **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span></span> <span data-ttu-id="f9f17-121">Utwórz nowe konto magazynu o nazwie "wadexample", a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="f9f17-121">Create a new Storage account named "wadexample" and click **Next**.</span></span>
7. <span data-ttu-id="f9f17-122">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f9f17-122">Click **Create**.</span></span>

### <a name="step-2-create-your-application"></a><span data-ttu-id="f9f17-123">Krok 2: Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f9f17-123">Step 2: Create your Application</span></span>
1. <span data-ttu-id="f9f17-124">Na komputerze deweloperskim Uruchom program Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="f9f17-124">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="f9f17-125">Utwórz nową Visual C# aplikację konsoli przeznaczonego dla programu .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="f9f17-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span></span> <span data-ttu-id="f9f17-126">Nazwa projektu hello "WadExampleVM".</span><span class="sxs-lookup"><span data-stu-id="f9f17-126">Name hello project "WadExampleVM".</span></span>

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. <span data-ttu-id="f9f17-128">Zastąp zawartość pliku Program.cs hello hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="f9f17-128">Replace hello contents of Program.cs with hello following code.</span></span> <span data-ttu-id="f9f17-129">Witaj klasy **SampleEventSourceWriter** implementuje cztery metody rejestrowania: **SendEnums**, **MessageMethod**, **SetOther** i  **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="f9f17-129">hello class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="f9f17-130">Hello pierwszy parametr toohello metody metody WriteEvent definiuje hello identyfikator hello odpowiednie zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="f9f17-130">hello first parameter toohello WriteEvent method defines hello ID for hello respective event.</span></span> <span data-ttu-id="f9f17-131">Hello metoda Run implementuje nieskończoną pętlę, która wywołuje każdą z hello metod rejestrowania w hello **SampleEventSourceWriter** klasy co 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="f9f17-131">hello Run method implements an infinite loop that calls each of hello logging methods implemented in hello **SampleEventSourceWriter** class every 10 seconds.</span></span>

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums tooint for efficient logging.
         public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
         public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
         public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }
       }

       enum MyColor {
         Red,
         Blue,
         Green
       }

       [Flags]
       enum MyFlags {
         Flag1 = 1,
         Flag2 = 2,
         Flag3 = 4
       }

       class Program
       {
         static void Main(string[] args) {
         Trace.TraceInformation("My application entry point called");

         int value = 0;

         while (true) {
             Thread.Sleep(10000);
             Trace.TraceInformation("Working");

             // Emit several events every time we go through hello loop
             for (int i = 0; i < 6; i++) {
                 SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
             }

             for (int i = 0; i < 3; i++) {
                 SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                 SampleEventSourceWriter.Log.SetOther(true, 123456789);
             }

             if (value == int.MaxValue) value = 0;
             SampleEventSourceWriter.Log.HighFreq(value++);
         }

        }
      }
     }
     ```
4. <span data-ttu-id="f9f17-132">Zapisz plik hello i wybierz **Kompiluj rozwiązanie** z hello **kompilacji** menu toobuild kodu.</span><span class="sxs-lookup"><span data-stu-id="f9f17-132">Save hello file and select **Build Solution** from hello **Build** menu toobuild your code.</span></span>

### <a name="step-3-deploy-your-application"></a><span data-ttu-id="f9f17-133">Krok 3: Wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f9f17-133">Step 3: Deploy your Application</span></span>
1. <span data-ttu-id="f9f17-134">Kliknij prawym przyciskiem myszy na powitania **WadExampleVM** projektu w **Eksploratora rozwiązań** i wybierz polecenie **Otwórz Folder w Eksploratorze plików**.</span><span class="sxs-lookup"><span data-stu-id="f9f17-134">Right-click on hello **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span></span>
2. <span data-ttu-id="f9f17-135">Przejdź toohello *bin\Debug* folder i wszystkie hello kopiowania plików (WadExampleVM.*)</span><span class="sxs-lookup"><span data-stu-id="f9f17-135">Navigate toohello *bin\Debug* folder and copy all hello files (WadExampleVM.*)</span></span>
3. <span data-ttu-id="f9f17-136">W **Eksploratora serwera** kliknij prawym przyciskiem myszy na maszynie wirtualnej hello i wybierz polecenie **łączyć się przy użyciu pulpitu zdalnego**.</span><span class="sxs-lookup"><span data-stu-id="f9f17-136">In **Server Explorer** right-click on hello virtual machine and choose **Connect using Remote Desktop**.</span></span>
4. <span data-ttu-id="f9f17-137">Po nawiązaniu połączenia toohello maszyny Wirtualnej Utwórz folder o nazwie WadExampleVM i wklejać pliki aplikacji hello folderu.</span><span class="sxs-lookup"><span data-stu-id="f9f17-137">Once connected toohello VM create a folder named WadExampleVM and paste your application files into hello folder.</span></span>
5. <span data-ttu-id="f9f17-138">Uruchamianie aplikacji hello WadExampleVM.exe.</span><span class="sxs-lookup"><span data-stu-id="f9f17-138">Launch hello application WadExampleVM.exe.</span></span> <span data-ttu-id="f9f17-139">Powinny zostać wyświetlone okno konsoli puste.</span><span class="sxs-lookup"><span data-stu-id="f9f17-139">You should see a blank console window.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a><span data-ttu-id="f9f17-140">Krok 4: Tworzenie konfiguracji diagnostyki i instalacja hello rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="f9f17-140">Step 4: Create your Diagnostics configuration and install hello Extension</span></span>
1. <span data-ttu-id="f9f17-141">Pobierz komputerze dewelopera tooyour definicji schematu hello publicznej konfiguracji pliku, wykonując następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="f9f17-141">Download hello public configuration file schema definition tooyour development computer by executing hello following PowerShell command:</span></span>

     <span data-ttu-id="f9f17-142">(Get-AzureServiceAvailableExtension - ExtensionName "PaaSDiagnostics" - ProviderNamespace "Microsoft.Azure.Diagnostics"). PublicConfigurationSchema | Wyjściowego pliku — kodowanie utf8 - FilePath "WadConfig.xsd"</span><span class="sxs-lookup"><span data-stu-id="f9f17-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span></span>
2. <span data-ttu-id="f9f17-143">Otwórz nowy plik XML w Visual Studio, albo w projekcie już otwarte lub w programie Visual Studio wystąpienia z Brak otwartych projektów.</span><span class="sxs-lookup"><span data-stu-id="f9f17-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span></span> <span data-ttu-id="f9f17-144">W programie Visual Studio, wybierz **Dodaj** -> **nowy element...**</span><span class="sxs-lookup"><span data-stu-id="f9f17-144">In Visual Studio, select **Add** -> **New Item…**</span></span><span data-ttu-id="f9f17-145"> -> **Visual C# elementów** -> **danych** -> **pliku XML**.</span><span class="sxs-lookup"><span data-stu-id="f9f17-145"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="f9f17-146">Nazwa pliku hello "WadExample.xml"</span><span class="sxs-lookup"><span data-stu-id="f9f17-146">Name hello file "WadExample.xml"</span></span>
3. <span data-ttu-id="f9f17-147">Skojarz hello WadConfig.xsd z hello pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f9f17-147">Associate hello WadConfig.xsd with hello configuration file.</span></span> <span data-ttu-id="f9f17-148">Upewnij się, że okno edytora WadExample.xml hello hello okno jest aktywne.</span><span class="sxs-lookup"><span data-stu-id="f9f17-148">Make sure hello WadExample.xml editor window is hello active window.</span></span> <span data-ttu-id="f9f17-149">Naciśnij klawisz **F4** tooopen hello **właściwości** okna.</span><span class="sxs-lookup"><span data-stu-id="f9f17-149">Press **F4** tooopen hello **Properties** window.</span></span> <span data-ttu-id="f9f17-150">Polecenie hello **schematy** właściwości w hello **właściwości** okna.</span><span class="sxs-lookup"><span data-stu-id="f9f17-150">Click on hello **Schemas** property in hello **Properties** window.</span></span> <span data-ttu-id="f9f17-151">Kliknij przycisk hello **...**</span><span class="sxs-lookup"><span data-stu-id="f9f17-151">Click hello **…**</span></span> <span data-ttu-id="f9f17-152">w hello **schematy** właściwości.</span><span class="sxs-lookup"><span data-stu-id="f9f17-152">in hello **Schemas** property.</span></span> <span data-ttu-id="f9f17-153">Kliknij przycisk hello **Dodaj...**</span><span class="sxs-lookup"><span data-stu-id="f9f17-153">Click hello **Add…**</span></span> <span data-ttu-id="f9f17-154">przycisk i przejdź toohello lokalizacji pliku XSD hello i wybierz hello pliku WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="f9f17-154">button and navigate toohello location where you saved hello XSD file and select hello file WadConfig.xsd.</span></span> <span data-ttu-id="f9f17-155">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9f17-155">Click **OK**.</span></span>
4. <span data-ttu-id="f9f17-156">Zastąp zawartość pliku konfiguracji WadExample.xml hello hello z powitania po XML, a następnie zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="f9f17-156">Replace hello contents of hello WadExample.xml configuration file with hello following XML and save hello file.</span></span> <span data-ttu-id="f9f17-157">Ten plik konfiguracyjny definiuje kilka toocollect liczników wydajności: jeden dla jednego wykorzystania pamięci i czasu procesora.</span><span class="sxs-lookup"><span data-stu-id="f9f17-157">This configuration file defines a couple performance counters toocollect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="f9f17-158">Następnie konfiguracji hello definiuje zdarzenia cztery hello odpowiadającego toohello metod w hello SampleEventSourceWriter klasy.</span><span class="sxs-lookup"><span data-stu-id="f9f17-158">Then hello configuration defines hello four events corresponding toohello methods in hello SampleEventSourceWriter class.</span></span>

```
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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a><span data-ttu-id="f9f17-159">Krok 5: Zdalnie zainstalować diagnostyki maszyny wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f9f17-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span></span>
<span data-ttu-id="f9f17-160">Witaj poleceń cmdlet programu PowerShell do zarządzania diagnostyki na maszynie Wirtualnej są: Set-AzureVMDiagnosticsExtension, Get AzureVMDiagnosticsExtension i Usuń AzureVMDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="f9f17-160">hello PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span></span>

1. <span data-ttu-id="f9f17-161">Na komputerze dewelopera Otwórz program Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f9f17-161">On your developer computer, open Azure PowerShell.</span></span>
2. <span data-ttu-id="f9f17-162">Wykonanie instalacji tooremotely skryptu hello diagnostyki na maszynie Wirtualnej (Zastąp `<user>` nazwą katalogu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f9f17-162">Execute hello script tooremotely install Diagnostics on your VM (Replace `<user>` with your user directory name.</span></span> <span data-ttu-id="f9f17-163">Zastąp `<StorageAccountKey>` kluczem konta magazynu hello konta magazynu wadexamplevm):</span><span class="sxs-lookup"><span data-stu-id="f9f17-163">Replace `<StorageAccountKey>` with hello storage account key for your wadexamplevm storage account):</span></span>
```
     $storage_name = "wadexamplevm"
     $key = "<StorageAccountKey>"
     $config_path="c:\users\<user>\documents\visual studio 2017\Projects\WadExampleVM\WadExampleVM\WadExample.xml"
     $service_name="wadexamplevm"
     $vm_name="WadExample"
     $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
     $VM1 = Get-AzureVM -ServiceName $service_name -Name $vm_name
     $VM2 = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $config_path -Version "1.*" -VM $VM1 -StorageContext $storageContext
     $VM3 = Update-AzureVM -ServiceName $service_name -Name $vm_name -VM $VM2.VM
```
### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="f9f17-164">Krok 6: Sprawdź dane telemetryczne</span><span class="sxs-lookup"><span data-stu-id="f9f17-164">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="f9f17-165">W Visual Studio hello **Eksploratora serwera** Przejdź konta magazynu wadexample toohello.</span><span class="sxs-lookup"><span data-stu-id="f9f17-165">In hello Visual Studio **Server Explorer** navigate toohello wadexample storage account.</span></span> <span data-ttu-id="f9f17-166">Po hello wirtualna została uruchomiona około 5 minut powinna zostać wyświetlona tabel hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** i **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="f9f17-166">After hello VM has been running about 5 minutes you should see hello tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="f9f17-167">Kliknij dwukrotnie jeden hello tabel tooview hello telemetrii, które zostały zebrane.</span><span class="sxs-lookup"><span data-stu-id="f9f17-167">Double-click on one of hello tables tooview hello telemetry that has been collected.</span></span>

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="f9f17-169">Schemat pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="f9f17-169">Configuration file schema</span></span>
<span data-ttu-id="f9f17-170">plik konfiguracji diagnostyki Hello definiuje wartości, które są tooinitialize używanych ustawień diagnostycznych konfiguracji podczas uruchamiania agenta diagnostyki hello.</span><span class="sxs-lookup"><span data-stu-id="f9f17-170">hello Diagnostics configuration file defines values that are used tooinitialize diagnostic configuration settings when hello diagnostics agent starts.</span></span> <span data-ttu-id="f9f17-171">Zobacz hello [najnowsze odwołanie do schematu](https://msdn.microsoft.com/library/azure/mt634524.aspx) poprawne wartości i przykłady.</span><span class="sxs-lookup"><span data-stu-id="f9f17-171">See hello [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f9f17-172">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="f9f17-172">Troubleshooting</span></span>
<span data-ttu-id="f9f17-173">Zobacz [Rozwiązywanie problemów z diagnostyki Azure](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="f9f17-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9f17-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f9f17-174">Next steps</span></span>
<span data-ttu-id="f9f17-175">[Zobacz listę maszyn wirtualnych innych pokrewnych artykułach diagnostyki Azure](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toochange hello dane są zbierane, rozwiązywanie problemów lub Dowiedz się więcej o diagnostyce ogólnie.</span><span class="sxs-lookup"><span data-stu-id="f9f17-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toochange hello data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
