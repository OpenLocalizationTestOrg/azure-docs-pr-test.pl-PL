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
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a>Włączanie diagnostyki w maszynach wirtualnych platformy Azure
Zobacz [Omówienie diagnostyki Azure](../monitoring-and-diagnostics/azure-diagnostics.md) w tle na diagnostyki Azure.

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a>Jak tooEnable diagnostyki na maszynie wirtualnej
Ta krokach związanych z opisano, jak zainstalować tooremotely tooan diagnostyki maszyny wirtualnej platformy Azure z komputera. Możesz też dowiedzieć się, jak tooimplement działającą na tej maszynie wirtualnej Azure i emituje telemetrii danych przy użyciu aplikacji hello .NET [EventSource — klasa][EventSource Class]. Diagnostyka Azure hello toocollect używane w danych telemetrycznych i zapisz go w koncie magazynu platformy Azure.

### <a name="pre-requisites"></a>Wymagania wstępne
To krokach związanych z zakłada posiadania subskrypcji platformy Azure i za pomocą programu Visual Studio 2017 hello Azure SDK. Jeśli nie masz subskrypcji platformy Azure, można utworzysz hello [bezpłatnej wersji próbnej][Free Trial]. Upewnij się, że zbyt[Instalowanie i konfigurowanie programu Azure PowerShell w wersji 0.8.7 lub nowszym][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-virtual-machine"></a>Krok 1: Tworzenie maszyny wirtualnej
1. Na komputerze deweloperskim Uruchom program Visual Studio 2017 r.
2. W Visual Studio hello **Eksploratora serwera** rozwiń **Azure**, kliknij prawym przyciskiem myszy **maszyn wirtualnych** następnie wybierz **Utwórz maszynę wirtualną**.
3. Wybierz subskrypcję platformy Azure w hello **Wybierz subskrypcję** okno dialogowe i kliknij przycisk **dalej**.
4. Wybierz **systemu Windows Server 2012 R2 Datacenter, 2017 czerwca** w hello **Wybieranie obrazu maszyny wirtualnej** okno dialogowe i kliknij przycisk **dalej**.
5. W hello **ustawienia podstawowej maszyny wirtualnej**, ustaw nazwę maszyny wirtualnej hello zbyt "wadexample". Ustaw swoją nazwę użytkownika administratora i hasło, a następnie kliknij przycisk **dalej**.
6. W hello **ustawienia usługi w chmurze** okna dialogowego Utwórz nową usługę w chmurze o nazwie "wadexampleVM". Utwórz nowe konto magazynu o nazwie "wadexample", a następnie kliknij przycisk **dalej**.
7. Kliknij przycisk **Utwórz**.

### <a name="step-2-create-your-application"></a>Krok 2: Tworzenie aplikacji
1. Na komputerze deweloperskim Uruchom program Visual Studio 2017 r.
2. Utwórz nową Visual C# aplikację konsoli przeznaczonego dla programu .NET Framework 4.5. Nazwa projektu hello "WadExampleVM".

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. Zastąp zawartość pliku Program.cs hello hello następującego kodu. Witaj klasy **SampleEventSourceWriter** implementuje cztery metody rejestrowania: **SendEnums**, **MessageMethod**, **SetOther** i  **HighFreq**. Hello pierwszy parametr toohello metody metody WriteEvent definiuje hello identyfikator hello odpowiednie zdarzenie. Hello metoda Run implementuje nieskończoną pętlę, która wywołuje każdą z hello metod rejestrowania w hello **SampleEventSourceWriter** klasy co 10 sekund.

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
4. Zapisz plik hello i wybierz **Kompiluj rozwiązanie** z hello **kompilacji** menu toobuild kodu.

### <a name="step-3-deploy-your-application"></a>Krok 3: Wdrażanie aplikacji
1. Kliknij prawym przyciskiem myszy na powitania **WadExampleVM** projektu w **Eksploratora rozwiązań** i wybierz polecenie **Otwórz Folder w Eksploratorze plików**.
2. Przejdź toohello *bin\Debug* folder i wszystkie hello kopiowania plików (WadExampleVM.*)
3. W **Eksploratora serwera** kliknij prawym przyciskiem myszy na maszynie wirtualnej hello i wybierz polecenie **łączyć się przy użyciu pulpitu zdalnego**.
4. Po nawiązaniu połączenia toohello maszyny Wirtualnej Utwórz folder o nazwie WadExampleVM i wklejać pliki aplikacji hello folderu.
5. Uruchamianie aplikacji hello WadExampleVM.exe. Powinny zostać wyświetlone okno konsoli puste.

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a>Krok 4: Tworzenie konfiguracji diagnostyki i instalacja hello rozszerzenia
1. Pobierz komputerze dewelopera tooyour definicji schematu hello publicznej konfiguracji pliku, wykonując następujące polecenia programu PowerShell hello:

     (Get-AzureServiceAvailableExtension - ExtensionName "PaaSDiagnostics" - ProviderNamespace "Microsoft.Azure.Diagnostics"). PublicConfigurationSchema | Wyjściowego pliku — kodowanie utf8 - FilePath "WadConfig.xsd"
2. Otwórz nowy plik XML w Visual Studio, albo w projekcie już otwarte lub w programie Visual Studio wystąpienia z Brak otwartych projektów. W programie Visual Studio, wybierz **Dodaj** -> **nowy element...** -> **Visual C# elementów** -> **danych** -> **pliku XML**. Nazwa pliku hello "WadExample.xml"
3. Skojarz hello WadConfig.xsd z hello pliku konfiguracji. Upewnij się, że okno edytora WadExample.xml hello hello okno jest aktywne. Naciśnij klawisz **F4** tooopen hello **właściwości** okna. Polecenie hello **schematy** właściwości w hello **właściwości** okna. Kliknij przycisk hello **...** w hello **schematy** właściwości. Kliknij przycisk hello **Dodaj...** przycisk i przejdź toohello lokalizacji pliku XSD hello i wybierz hello pliku WadConfig.xsd. Kliknij przycisk **OK**.
4. Zastąp zawartość pliku konfiguracji WadExample.xml hello hello z powitania po XML, a następnie zapisz plik hello. Ten plik konfiguracyjny definiuje kilka toocollect liczników wydajności: jeden dla jednego wykorzystania pamięci i czasu procesora. Następnie konfiguracji hello definiuje zdarzenia cztery hello odpowiadającego toohello metod w hello SampleEventSourceWriter klasy.

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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a>Krok 5: Zdalnie zainstalować diagnostyki maszyny wirtualnej na platformie Azure
Witaj poleceń cmdlet programu PowerShell do zarządzania diagnostyki na maszynie Wirtualnej są: Set-AzureVMDiagnosticsExtension, Get AzureVMDiagnosticsExtension i Usuń AzureVMDiagnosticsExtension.

1. Na komputerze dewelopera Otwórz program Azure PowerShell.
2. Wykonanie instalacji tooremotely skryptu hello diagnostyki na maszynie Wirtualnej (Zastąp `<user>` nazwą katalogu użytkownika. Zastąp `<StorageAccountKey>` kluczem konta magazynu hello konta magazynu wadexamplevm):
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
### <a name="step-6-look-at-your-telemetry-data"></a>Krok 6: Sprawdź dane telemetryczne
W Visual Studio hello **Eksploratora serwera** Przejdź konta magazynu wadexample toohello. Po hello wirtualna została uruchomiona około 5 minut powinna zostać wyświetlona tabel hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** i **WADSetOtherTable**. Kliknij dwukrotnie jeden hello tabel tooview hello telemetrii, które zostały zebrane.

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a>Schemat pliku konfiguracji
plik konfiguracji diagnostyki Hello definiuje wartości, które są tooinitialize używanych ustawień diagnostycznych konfiguracji podczas uruchamiania agenta diagnostyki hello. Zobacz hello [najnowsze odwołanie do schematu](https://msdn.microsoft.com/library/azure/mt634524.aspx) poprawne wartości i przykłady.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Zobacz [Rozwiązywanie problemów z diagnostyki Azure](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) Aby uzyskać więcej informacji.

## <a name="next-steps"></a>Następne kroki
[Zobacz listę maszyn wirtualnych innych pokrewnych artykułach diagnostyki Azure](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toochange hello dane są zbierane, rozwiązywanie problemów lub Dowiedz się więcej o diagnostyce ogólnie.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
