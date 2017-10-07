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
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a>Włączanie diagnostyki Azure usług w chmurze Azure
Zobacz [Omówienie diagnostyki Azure](../azure-diagnostics.md) w tle na diagnostyki Azure.

## <a name="how-tooenable-diagnostics-in-a-worker-role"></a>Jak tooEnable diagnostyki w roli procesu roboczego
W tym przewodniku opisano, jak tooimplement roli procesu roboczego platformy Azure, który emituje telemetrii danych przy użyciu hello .NET EventSource — klasa. Diagnostyka Azure jest dane telemetryczne hello toocollect używane i zapisz go w konta magazynu platformy Azure. Podczas tworzenia roli procesu roboczego, Visual Studio automatycznie włącza 1.0 diagnostyki jako część rozwiązania hello Azure SDK dla platformy .NET 2.4 i starszych wersji. Witaj poniższe instrukcje przedstawiają hello proces tworzenia roli procesu roboczego hello, wyłączenie diagnostyki 1.0 z rozwiązania hello i wdrażanie 1.2 diagnostyki lub roli proces roboczy tooyour 1.3.

### <a name="prerequisites"></a>Wymagania wstępne
W tym artykule przyjęto założenie, posiadania subskrypcji platformy Azure i przy użyciu programu Visual Studio z hello Azure SDK. Jeśli nie masz subskrypcji platformy Azure, można utworzysz hello [bezpłatnej wersji próbnej][Free Trial]. Upewnij się, że zbyt[Instalowanie i konfigurowanie programu Azure PowerShell w wersji 0.8.7 lub nowszym][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-worker-role"></a>Krok 1: Tworzenie roli procesu roboczego
1. Uruchom program **Visual Studio**.
2. Utwórz **usługi w chmurze Azure** projektu z hello **chmury** szablonu, którego celem jest środowisko .NET Framework 4.5.  Nazwa projektu hello "WadExample", a następnie kliknij przycisk Ok.
3. Wybierz **roli procesu roboczego** i kliknij przycisk Ok. Witaj, projekt zostanie utworzony.
4. W **Eksploratora rozwiązań**, kliknij dwukrotnie hello **WorkerRole1** właściwości pliku.
5. W hello **konfiguracji** karcie, usuń zaznaczenie **włączyć diagnostyki** toodisable 1.0 diagnostyki Azure SDK (2.4 lub starszej).
6. Tworzenie tooverify Twojego rozwiązania, które użytkownik nie ma błędów.

### <a name="step-2-instrument-your-code"></a>Krok 2: Instrumentacja kodu
Zamień zawartość hello WorkerRole.cs hello następującego kodu. Witaj klasy SampleEventSourceWriter, odziedziczone hello [EventSource — klasa][EventSource Class], implementuje cztery metody rejestrowania: **SendEnums**, **MessageMethod** , **SetOther** i **HighFreq**. Witaj pierwszy parametr toohello **metody WriteEvent** Metoda określa identyfikator hello hello odpowiednie zdarzenie. Hello metoda Run implementuje nieskończoną pętlę, która wywołuje każdą z hello metod rejestrowania w hello **SampleEventSourceWriter** klasy co 10 sekund.

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


### <a name="step-3-deploy-your-worker-role"></a>Krok 3: Wdrażanie swojej roli procesu roboczego

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. Wdrażanie procesu roboczego tooAzure roli z poziomu programu Visual Studio, wybierając hello **WadExample** projektu w hello Eksploratora rozwiązań następnie **publikowania** z hello **kompilacji** menu.
2. Wybierz subskrypcję.
3. W hello **ustawień publikowania platformy Azure Microsoft** okno dialogowe, wybierz opcję **Utwórz nowy...** .
4. W hello **Tworzenie usługi w chmurze i konto magazynu** okna dialogowego, wprowadź **nazwa** (na przykład "WadExample") i wybierz region lub grupę koligacji.
5. Zestaw hello **środowiska** za**przemieszczania**.
6. Zmodyfikuj inne **ustawienia** jako odpowiednie i kliknij przycisk **publikowania**.
7. Sprawdź, czy po zakończeniu wdrożenia w hello portalu Azure, która usługi w chmurze jest w **systemem** stanu.

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-hello-extension"></a>Krok 4: Tworzenie pliku konfiguracji diagnostyki i zainstaluj rozszerzenie hello
1. Pobierz definicję schematu pliku konfiguracji publicznego hello, wykonując następujące polecenia programu PowerShell hello:

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. Dodaj tooyour pliku XML **WorkerRole1** projektu, klikając prawym przyciskiem myszy na powitania **WorkerRole1** projekt i wybierz **Dodaj** -> **nowy element...** -> **Visual C# elementów** -> **danych** -> **pliku XML**. Nadaj nazwę plikowi hello "WadExample.xml".

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. Skojarz hello WadConfig.xsd z hello pliku konfiguracji. Upewnij się, że okno edytora WadExample.xml hello hello okno jest aktywne. Naciśnij klawisz **F4** tooopen hello **właściwości** okna. Kliknij przycisk hello **schematy** właściwości w hello **właściwości** okna. Kliknij przycisk hello **...** w hello **schematy** właściwości. Kliknij przycisk hello **Dodaj...** przycisk i przejdź toohello lokalizacji pliku XSD hello i wybierz hello pliku WadConfig.xsd. Kliknij przycisk **OK**.

4. Zastąp zawartość pliku konfiguracji WadExample.xml hello hello z powitania po XML, a następnie zapisz plik hello. Ten plik konfiguracyjny definiuje kilka toocollect liczników wydajności: jeden dla jednego wykorzystania pamięci i czasu procesora. Następnie konfiguracji hello definiuje zdarzenia cztery hello odpowiadającego toohello metod w hello SampleEventSourceWriter klasy.

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

### <a name="step-5-install-diagnostics-on-your-worker-role"></a>Krok 5: Instalowanie diagnostyki w swojej roli procesu roboczego
Witaj poleceń cmdlet programu PowerShell do zarządzania diagnostyki dla roli sieci web lub procesu roboczego są: Set-AzureServiceDiagnosticsExtension, Get AzureServiceDiagnosticsExtension i Usuń AzureServiceDiagnosticsExtension.

1. Otwórz program Azure PowerShell.
2. Wykonaj hello skryptu tooinstall diagnostyki w swojej roli procesu roboczego (Zastąp *StorageAccountKey* kluczem konta magazynu hello konta magazynu wadexample i *config_path* ze ścieżką hello toohello *WadExample.xml* pliku):

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a>Krok 6: Sprawdź dane telemetryczne
W Visual Studio hello **Eksploratora serwera**, przejdź do konta magazynu wadexample toohello. Po około pięciu (5) minut była uruchomiona usługa w chmurze hello, powinny pojawić się tabele hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** i **WADSetOtherTable**. Kliknij dwukrotnie jeden z hello tabel tooview hello telemetrii, które zostały zebrane.

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a>Schemat pliku konfiguracji
plik konfiguracji diagnostyki Hello definiuje wartości, które są tooinitialize używanych ustawień diagnostycznych konfiguracji podczas uruchamiania agenta diagnostyki hello. Zobacz hello [najnowsze odwołanie do schematu](https://msdn.microsoft.com/library/azure/mt634524.aspx) poprawne wartości i przykłady.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli masz problemy, zobacz [Rozwiązywanie problemów z diagnostyki Azure](../azure-diagnostics-troubleshooting.md) Aby uzyskać pomoc dotyczącą typowych problemów.

## <a name="next-steps"></a>Następne kroki
[Zobacz listę pokrewne artykuły diagnostycznych maszyn wirtualnych Azure](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) toochange hello dane są zbierane, rozwiązywanie problemów lub Dowiedz się więcej o diagnostyce ogólnie.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
