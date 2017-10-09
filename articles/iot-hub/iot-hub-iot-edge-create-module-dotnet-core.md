---
title: "aaaCreate moduł Azure IoT krawędzi w języku C# | Dokumentacja firmy Microsoft"
description: "W tym samouczku ilustrację, jak toowrite cz danych konwertera modułu przy użyciu hello najnowszych pakietów NuGet krawędzi IoT Azure, programu Visual Studio Code i C#."
services: iot-hub
author: jeffreyCline
manager: timlt
keywords: "Azure iot, samouczek, modułu, nuget, vscode, csharp, krawędzi"
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: jcline
ms.openlocfilehash: b104609c05d1613e21acc7d7bed547f311179151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a>Utwórz moduł Azure IoT krawędzi z C & #x23;

W tym samouczku ilustrację jak toocreate a modułu dla `Azure IoT Edge` przy użyciu `Visual Studio Code` i `C#`.

W tym samouczku przeprowadzenie możemy konfiguracji środowiska i w jaki sposób toowrite [cz](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) danych konwertera modułu przy użyciu najnowszych hello `Azure IoT Edge NuGet` pakietów. 

>[!NOTE]
Ten samouczek używa hello `.NET Core SDK`, który obsługuje zgodności między platformami. Witaj następujące samouczek jest przeznaczony przy użyciu hello `Windows 10` systemu operacyjnego. Niektóre polecenia hello w tym samouczku mogą być różne w zależności od Twojego `development environment`. 

## <a name="prerequisites"></a>Wymagania wstępne

W tej sekcji możemy konfiguracji środowiska pod kątem `Azure IoT Edge` programowanie modułu. Ma to zastosowanie tooboth **64-bitowym systemie Windows** i **64-bitowego systemu Linux (8 Ubuntu/Debian)** systemów operacyjnych.

wymagane jest Hello następującego oprogramowania:

- [Klient Git](https://git-scm.com/downloads)
- [Zestaw SDK dla platformy .NET Core](https://www.microsoft.com/net/core#windowscmd)
- [Visual Studio Code](https://code.visualstudio.com/)

Nie trzeba tooclone hello repozytorium dla tego przykładu, jednak wszystkie hello przykładowy kod przedstawiony omówione w tym samouczku znajduje się w hello następujące repozytorium:

- `git clone https://github.com/Azure-Samples/iot-edge-samples.git`.
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a>Wprowadzenie

1. Zainstaluj `.NET Core SDK`.
2. Zainstaluj `Visual Studio Code` i hello `C# extension` z hello Visual Studio Marketplace kodu.

Wyświetlić [krótki samouczek wideo](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) dotyczące sposobu uruchamiania przy użyciu tooget `Visual Studio Code` i hello `.NET Core SDK`.

## <a name="creating-hello-azure-iot-edge-converter-module"></a>Tworzenie hello Azure IoT krawędzi konwertera modułu

1. Zainicjuj nowy `.NET Core` klasy projektu biblioteki C#:
    - Otwórz okno wiersza polecenia (`Windows + R` -> `cmd` -> `enter`).
    - Przejdź do folderu toohello, gdzie ma toocreate hello `C#` projektu.
    - Typ **dotnet nowej biblioteki klas -o IoTEdgeConverterModule -f netstandard1.3**. 
    - To polecenie tworzy pustą klasę o nazwie `Class1.cs` w katalogu projektów.
2. Przejdź do folderu toohello gdzie właśnie utworzyliśmy projektu biblioteki klas hello wpisując **cd IoTEdgeConverterModule**.
3. Witaj Otwórz projekt w `Visual Studio Code` , wpisując **kodu.**.
4. Po otwarciu projektu hello w `Visual Studio Code`, kliknij na powitania **IoTEdgeConverterModule.csproj** tooopen hello pliku, jak pokazano w powitania po obrazu:

    ![Okno edycji w usłudze Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. Wstaw hello `XML` pokazano hello następującego fragmentu kodu między hello zamknięcia obiektu blob `PropertyGroup` tagu i hello zamknięcia `Project` tagów; wiersz sześć w hello poprzedzających obrazu i Zapisz plik hello naciskając `Ctrl`  +  `S`.

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. Po zapisaniu hello `.csproj` pliku `Visual Studio Code` powinien monit o `unresolved dependencies` okna dialogowego w powitania po obrazu: 

    ![Okno dialogowe programu Visual Studio Code przywracania zależności](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    ) kliknij `Restore` toorestore odwołania do wszystkich hello w projektach hello `.csproj` pliku w tym hello `PackageReferences` dodaliśmy. 

    (b) `Visual Studio Code` automatycznie tworzy hello `project.assets.json` pliku w projektach `obj` folderu. Ten plik zawiera informacje o projektu zależności toomake kolejnych operacji przywracania szybciej.
 
    >[!NOTE]
    `.NET Core Tools`znajdują się teraz na podstawie programu MSBuild. Co oznacza, że `.csproj` plik projektu jest tworzony zamiast `project.json`.

    - Jeśli `Visual Studio Code` Monituj użytkownika o jest prawidłowy, możemy go ręcznie. Otwórz hello `Visual Studio Code` zintegrowane okno terminalu przez naciśnięcie przycisku hello `Ctrl`  +  `backtick` kluczy lub za pomocą menu hello `View`  ->  `Integrated Terminal`.
    - W hello `Integrated Terminal` typ okna **przywracania dotnet**.
    
7. Zmień nazwę hello `Class1.cs` pliku zbyt`BleConverterModule.cs`. 

    ) plik hello toorename najpierw kliknij plik hello a następnie naciśnij klawisz hello `F2` klucza.
    
    (b) wpisz nazwę nowego hello **BleConverterModule**, jak pokazano w powitania po obrazu:

    ![Visual Studio Code zmiana nazwy klasy](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. Zastąp istniejący kod hello w hello `BleConverterModule.cs` pliku przez kopiowanie i wklejanie hello następującego fragmentu kodu w Twojej `BleConverterModule.cs` pliku.

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Globalization;
   using System.Linq;
   using System.Text;
   using System.Threading;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace IoTEdgeConverterModule
   {
       public class BleConverterModule : IGatewayModule, IGatewayModuleStart
       {
           private Broker broker;
           private string configuration;
           private int messageCount;

           public void Create(Broker broker, byte[] configuration)
           {
               this.broker = broker;
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Start()
           {
           }

           public void Destroy()
           {
           }

           public void Receive(Message received_message)
           {
               string recMsg = Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               BleData receivedData = JsonConvert.DeserializeObject<BleData>(recMsg);

               float temperature = float.Parse(receivedData.Temperature, CultureInfo.InvariantCulture.NumberFormat); 
               Dictionary<string, string> receivedProperties = received_message.Properties;
            
               Dictionary<string, string> properties = new Dictionary<string, string>();
               properties.Add("source", receivedProperties["source"]);
               properties.Add("macAddress", receivedProperties["macAddress"]);
               properties.Add("temperatureAlert", temperature > 30 ? "true" : "false");
   
               String content = String.Format("{0} \"deviceId\": \"Intel NUC Gateway\", \"messageId\": {1}, \"temperature\": {2} {3}", "{", ++this.messageCount, temperature, "}");
               Message messageToPublish = new Message(content, properties);
   
               this.broker.Publish(messageToPublish);
           }
       }
   }
   ```

9. Zapisz plik hello naciskając `Ctrl`  +  `S`.

10. Utwórz nowy plik o nazwie `Untitled-1` przez naciśnięcie przycisku hello `Ctrl`  +  `N` kluczy w powitania po obrazu:

    ![Visual Studio Code nowy plik.](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. Witaj toodeserialize `JSON` obiektu otrzymane od hello symulowane `BLE` urządzenia, po kodu na powitania hello kopiowania `Untitled-1` okna edytora kodu w pliku. 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace IoTEdgeConverterModule
   {
       public class BleData
       {
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

12. Zapisz plik hello jako `BleData.cs` naciskając `Ctrl`  +  `Shift`  +  `S` kluczy.
    - Na powitania Zapisz jako okno dialogowe, w hello `Save as Type` menu rozwijanego wybierz `C# (*.cs;*.csx)` w powitania po obrazu:

    ![Visual Studio Code Zapisz jako okna dialogowego](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. Utwórz nowy plik o nazwie `Untitled-1` przez naciśnięcie przycisku hello `Ctrl`  +  `N` kluczy.

14. Skopiuj i Wklej hello następującego fragmentu kodu na powitania `Untitled-1` pliku. Ta klasa jest `Azure IoT Edge` moduł, który używamy toooutput hello danych otrzymywanych z naszych `BleConverterModule`.

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace PrinterModule
   {
       public class DotNetPrinterModule : IGatewayModule
       {
           private string configuration;
           public void Create(Broker broker, byte[] configuration)
           {
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Destroy()
           {
           }
   
           public void Receive(Message received_message)
           {
               string recMsg = System.Text.Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               Dictionary<string, string> receivedProperties = received_message.Properties;
               
               BleConverterData receivedData = JsonConvert.DeserializeObject<BleConverterData>(recMsg);
   
               Console.WriteLine();
               Console.WriteLine("Module           : [DotNetPrinterModule]");
               Console.WriteLine("received_message : {0}", recMsg);
   
               if(received_message.Properties["source"] == "bleTelemetry")
               {
                   Console.WriteLine("Source           : {0}", receivedProperties["source"]);
                   Console.WriteLine("MAC address      : {0}", receivedProperties["macAddress"]);
                   Console.WriteLine("Temperature Alert: {0}", receivedProperties["temperatureAlert"]);
                   Console.WriteLine("Deserialized Obj : [BleConverterData]");
                   Console.WriteLine("  DeviceId       : {0}", receivedData.DeviceId);
                   Console.WriteLine("  MessageId      : {0}", receivedData.MessageId);
                   Console.WriteLine("  Temperature    : {0}", receivedData.Temperature);
               }
   
               Console.WriteLine();
           }
       }
   }
   ```

15. Zapisz plik hello jako `DotNetPrinterModule.cs` naciskając `Ctrl`  +  `Shift`  +  `S`.
    - Na powitania Zapisz jako okno dialogowe, w hello `Save as Type` menu rozwijanego wybierz `C# (*.cs;*.csx)`.

16. Utwórz nowy plik o nazwie `Untitled-1` przez naciśnięcie przycisku hello `Ctrl`  +  `N` kluczy.

17. Witaj toodeserialize `JSON` obiektu otrzymane od hello `BleConverterModule`, kopiowania i wklejania hello następujące fragment kodu do hello `Untitled-1` pliku. 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace PrinterModule
   {
       public class BleConverterData
       {
           [JsonProperty(PropertyName = "deviceId")]
           public string DeviceId { get; set; }
   
           [JsonProperty(PropertyName = "messageId")]
           public string MessageId { get; set; }
   
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

18. Zapisz plik hello jako `BleConverterData.cs` naciskając `Ctrl`  +  `Shift`  +  `S`.
    - Na powitania Zapisz jako okno dialogowe, w hello `Save as Type` menu rozwijanego wybierz `C# (*.cs;*.csx)`.

19. Utwórz nowy plik o nazwie `Untitled-1` przez naciśnięcie przycisku hello `Ctrl`  +  `N` kluczy.

20. Skopiuj i Wklej hello następującego fragmentu kodu na powitania `Untitled-1` pliku.

   ```json
   {
       "loaders": [
           {
               "type": "dotnetcore",
               "name": "dotnetcore",
               "configuration": {
                   "binding.path": "dotnetcore.dll",
                   "binding.coreclrpath": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\coreclr.dll",
                   "binding.trustedplatformassemblieslocation": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\"
               }
           }
       ],
          "modules": [
           {
               "name": "simulated_device",
               "loader": {
                   "name": "native",
                   "entrypoint": {
                       "module.path": "simulated_device.dll"
                   }
               },
               "args": {
                   "macAddress": "01:02:03:03:02:01",
                   "messagePeriod": 500
               }
           },
           {
               "name": "ble_converter_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "IoTEdgeConverterModule.BleConverterModule"
                   }
               },
               "args": ""
           },
           {
               "name": "printer_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "PrinterModule.DotNetPrinterModule"
                   }
               },
               "args": ""
           }
       ],
       "links": [
           {
               "source": "simulated_device", "sink": "ble_converter_module"
           },
           {
               "source": "ble_converter_module", "sink": "printer_module"
           }
   ]
   }
   ```

21. Zapisz plik hello jako `gw-config.json` naciskając `Ctrl`  +  `Shift`  +  `S`.
    - Na powitania Zapisz jako okno dialogowe, w hello `Save as Type` menu rozwijanego wybierz `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.

22. Kopiowanie tooenable toohello pliku konfiguracji hello output katalogu, hello aktualizacji `IoTEdgeConverterModule.csproj` z hello następującego obiektu blob XML:

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - Zaktualizowano Hello `IoTEdgeConverterModule.csproj` powinien wyglądać podobnie jak hello po obrazu:

    ![Visual Studio Code zaktualizować pliku .csproj](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. Utwórz nowy plik o nazwie `Untitled-1` przez naciśnięcie przycisku hello `Ctrl`  +  `N` kluczy.

24. Skopiuj i Wklej hello następującego fragmentu kodu na powitania `Untitled-1` pliku.

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. Zapisz plik hello jako `binplace.ps1` naciskając `Ctrl`  +  `Shift`  +  `S`.
    - Na powitania Zapisz jako okno dialogowe, w hello `Save as Type` menu rozwijanego wybierz `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.

26. Tworzenie hello projektu przez naciśnięcie przycisku hello `Ctrl`  +  `Shift`  +  `B` kluczy. Podczas kompilowania projektu hello na powitania po raz pierwszy, `Visual Studio Code` monit hello `No build task defined.` okna dialogowego w powitania po obrazu:

    ![Zadanie kompilacji programu Visual Studio Code okna dialogowego](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    ) kliknij hello `Configure Build Task` przycisku.

    (b) w hello `Select a Task Runner` menu rozwijanego okna dialogowego. Wybierz `.NET Core` w powitania po obrazu: 

    ![Visual Studio Code wybierz Okno zadań](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    hello c) kliknięcie przycisku `.NET Core` elementu tworzy hello `tasks.json` plików w sieci `.vscode` katalogu i otwiera plik w hello hello `code editor` okna. Nie jest toomodify nie konieczności ten plik, zamknij hello kartę.

27.  Otwórz hello `Visual Studio Code` zintegrowane okno terminalu przez naciśnięcie przycisku hello `Ctrl`  +  `backtick` kluczy lub za pomocą menu hello `View`  ->  `Integrated Terminal` i typ **.\binplace.ps1**do hello `PowerShell` wiersza polecenia. To polecenie powoduje skopiowanie wszystkich naszych zależności toohello katalogu wyjściowego.

28. Przejdź do katalogu wyjściowego projektów toohello w hello `Integrated Terminal` okna, wpisując **cd.\bin\Debug\netstandard1.3**.

29. Uruchom hello przykładowy projekt, wpisując **. \gw.exe gw — config.json** do hello `Integrated Terminal` okno. 
    - Jeśli zostały wykonane kroki hello ściśle w tym samouczku, użytkownik powinien teraz korzystać z hello `Azure IoT Edge BLE Data Converter Module` przykładowy projekt w powitania po obrazu:
    
        ![Przykład symulowane urządzenie działa w programie Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - Jeśli chcesz, aby aplikacja hello tooterminate, naciśnij klawisz hello `<Enter>` klucza.

>[!IMPORTANT]
Nie zaleca się toouse `Ctrl`  +  `C` tooterminate hello `IoT Edge` bramy aplikacji (czyli **gw.exe**). Ponieważ ta akcja może spowodować tooterminate procesu hello nieprawidłowo.

