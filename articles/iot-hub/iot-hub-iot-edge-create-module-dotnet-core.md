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
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="aa821-104">Utwórz moduł Azure IoT krawędzi z C & #x23;</span><span class="sxs-lookup"><span data-stu-id="aa821-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="aa821-105">W tym samouczku ilustrację jak toocreate a modułu dla `Azure IoT Edge` przy użyciu `Visual Studio Code` i `C#`.</span><span class="sxs-lookup"><span data-stu-id="aa821-105">This tutorial showcases how toocreate a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="aa821-106">W tym samouczku przeprowadzenie możemy konfiguracji środowiska i w jaki sposób toowrite [cz](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) danych konwertera modułu przy użyciu najnowszych hello `Azure IoT Edge NuGet` pakietów.</span><span class="sxs-lookup"><span data-stu-id="aa821-106">In this tutorial, we walk through environment set-up and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="aa821-107">Ten samouczek używa hello `.NET Core SDK`, który obsługuje zgodności między platformami.</span><span class="sxs-lookup"><span data-stu-id="aa821-107">This tutorial is using hello `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="aa821-108">Witaj następujące samouczek jest przeznaczony przy użyciu hello `Windows 10` systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="aa821-108">hello following tutorial is written using hello `Windows 10` operating system.</span></span> <span data-ttu-id="aa821-109">Niektóre polecenia hello w tym samouczku mogą być różne w zależności od Twojego `development environment`.</span><span class="sxs-lookup"><span data-stu-id="aa821-109">Some of hello commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="aa821-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="aa821-110">Prerequisites</span></span>

<span data-ttu-id="aa821-111">W tej sekcji możemy konfiguracji środowiska pod kątem `Azure IoT Edge` programowanie modułu.</span><span class="sxs-lookup"><span data-stu-id="aa821-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="aa821-112">Ma to zastosowanie tooboth **64-bitowym systemie Windows** i **64-bitowego systemu Linux (8 Ubuntu/Debian)** systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="aa821-112">It applies tooboth **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="aa821-113">wymagane jest Hello następującego oprogramowania:</span><span class="sxs-lookup"><span data-stu-id="aa821-113">hello following software is required:</span></span>

- [<span data-ttu-id="aa821-114">Klient Git</span><span class="sxs-lookup"><span data-stu-id="aa821-114">Git Client</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="aa821-115">Zestaw SDK dla platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="aa821-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="aa821-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="aa821-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="aa821-117">Nie trzeba tooclone hello repozytorium dla tego przykładu, jednak wszystkie hello przykładowy kod przedstawiony omówione w tym samouczku znajduje się w hello następujące repozytorium:</span><span class="sxs-lookup"><span data-stu-id="aa821-117">You do not need tooclone hello repo for this sample, however all of hello sample code discussed in this tutorial is located in hello following repository:</span></span>

- <span data-ttu-id="aa821-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="aa821-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="aa821-119">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="aa821-119">Getting started</span></span>

1. <span data-ttu-id="aa821-120">Zainstaluj `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="aa821-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="aa821-121">Zainstaluj `Visual Studio Code` i hello `C# extension` z hello Visual Studio Marketplace kodu.</span><span class="sxs-lookup"><span data-stu-id="aa821-121">Install `Visual Studio Code` and hello `C# extension` from hello Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="aa821-122">Wyświetlić [krótki samouczek wideo](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) dotyczące sposobu uruchamiania przy użyciu tooget `Visual Studio Code` i hello `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="aa821-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how tooget started using `Visual Studio Code` and hello `.NET Core SDK`.</span></span>

## <a name="creating-hello-azure-iot-edge-converter-module"></a><span data-ttu-id="aa821-123">Tworzenie hello Azure IoT krawędzi konwertera modułu</span><span class="sxs-lookup"><span data-stu-id="aa821-123">Creating hello Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="aa821-124">Zainicjuj nowy `.NET Core` klasy projektu biblioteki C#:</span><span class="sxs-lookup"><span data-stu-id="aa821-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="aa821-125">Otwórz okno wiersza polecenia (`Windows + R` -> `cmd` -> `enter`).</span><span class="sxs-lookup"><span data-stu-id="aa821-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="aa821-126">Przejdź do folderu toohello, gdzie ma toocreate hello `C#` projektu.</span><span class="sxs-lookup"><span data-stu-id="aa821-126">Navigate toohello folder where you'd like toocreate hello `C#` project.</span></span>
    - <span data-ttu-id="aa821-127">Typ **dotnet nowej biblioteki klas -o IoTEdgeConverterModule -f netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="aa821-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="aa821-128">To polecenie tworzy pustą klasę o nazwie `Class1.cs` w katalogu projektów.</span><span class="sxs-lookup"><span data-stu-id="aa821-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="aa821-129">Przejdź do folderu toohello gdzie właśnie utworzyliśmy projektu biblioteki klas hello wpisując **cd IoTEdgeConverterModule**.</span><span class="sxs-lookup"><span data-stu-id="aa821-129">Navigate toohello folder where we just created hello class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="aa821-130">Witaj Otwórz projekt w `Visual Studio Code` , wpisując **kodu.**.</span><span class="sxs-lookup"><span data-stu-id="aa821-130">Open hello project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="aa821-131">Po otwarciu projektu hello w `Visual Studio Code`, kliknij na powitania **IoTEdgeConverterModule.csproj** tooopen hello pliku, jak pokazano w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="aa821-131">Once hello project is opened in `Visual Studio Code`, click on hello **IoTEdgeConverterModule.csproj** tooopen hello file as shown in hello following image:</span></span>

    ![Okno edycji w usłudze Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="aa821-133">Wstaw hello `XML` pokazano hello następującego fragmentu kodu między hello zamknięcia obiektu blob `PropertyGroup` tagu i hello zamknięcia `Project` tagów; wiersz sześć w hello poprzedzających obrazu i Zapisz plik hello naciskając `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="aa821-133">Insert hello `XML` blob shown in hello following code snippet between hello closing `PropertyGroup` tag and hello closing `Project` tag; line six in hello preceding image and save hello file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="aa821-134">Po zapisaniu hello `.csproj` pliku `Visual Studio Code` powinien monit o `unresolved dependencies` okna dialogowego w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="aa821-134">Once you save hello `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in hello following image:</span></span> 

    ![Okno dialogowe programu Visual Studio Code przywracania zależności](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="aa821-136">) kliknij `Restore` toorestore odwołania do wszystkich hello w projektach hello `.csproj` pliku w tym hello `PackageReferences` dodaliśmy.</span><span class="sxs-lookup"><span data-stu-id="aa821-136">a) Click `Restore` toorestore all of hello references in hello projects `.csproj` file including hello `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="aa821-137">(b) `Visual Studio Code` automatycznie tworzy hello `project.assets.json` pliku w projektach `obj` folderu.</span><span class="sxs-lookup"><span data-stu-id="aa821-137">b) `Visual Studio Code` automatically creates hello `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="aa821-138">Ten plik zawiera informacje o projektu zależności toomake kolejnych operacji przywracania szybciej.</span><span class="sxs-lookup"><span data-stu-id="aa821-138">This file contains information about your project's dependencies toomake subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="aa821-139">`.NET Core Tools`znajdują się teraz na podstawie programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="aa821-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="aa821-140">Co oznacza, że `.csproj` plik projektu jest tworzony zamiast `project.json`.</span><span class="sxs-lookup"><span data-stu-id="aa821-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="aa821-141">Jeśli `Visual Studio Code` Monituj użytkownika o jest prawidłowy, możemy go ręcznie.</span><span class="sxs-lookup"><span data-stu-id="aa821-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="aa821-142">Otwórz hello `Visual Studio Code` zintegrowane okno terminalu przez naciśnięcie przycisku hello `Ctrl`  +  `backtick` kluczy lub za pomocą menu hello `View`  ->  `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="aa821-142">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="aa821-143">W hello `Integrated Terminal` typ okna **przywracania dotnet**.</span><span class="sxs-lookup"><span data-stu-id="aa821-143">In hello `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="aa821-144">Zmień nazwę hello `Class1.cs` pliku zbyt`BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="aa821-144">Rename hello `Class1.cs` file too`BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="aa821-145">) plik hello toorename najpierw kliknij plik hello a następnie naciśnij klawisz hello `F2` klucza.</span><span class="sxs-lookup"><span data-stu-id="aa821-145">a) toorename hello file first click on hello file then press hello `F2` key.</span></span>
    
    <span data-ttu-id="aa821-146">(b) wpisz nazwę nowego hello **BleConverterModule**, jak pokazano w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="aa821-146">b) Type in hello new name **BleConverterModule**, as seen in hello following image:</span></span>

    ![Visual Studio Code zmiana nazwy klasy](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="aa821-148">Zastąp istniejący kod hello w hello `BleConverterModule.cs` pliku przez kopiowanie i wklejanie hello następującego fragmentu kodu w Twojej `BleConverterModule.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="aa821-148">Replace hello existing code in hello `BleConverterModule.cs` file by copying and pasting hello following code snippet into your `BleConverterModule.cs` file.</span></span>

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

9. <span data-ttu-id="aa821-149">Zapisz plik hello naciskając `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="aa821-149">Save hello file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="aa821-150">Utwórz nowy plik o nazwie `Untitled-1` przez naciśnięcie przycisku hello `Ctrl`  +  `N` kluczy w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="aa821-150">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys as seen in hello following image:</span></span>

    ![Visual Studio Code nowy plik.](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="aa821-152">Witaj toodeserialize `JSON` obiektu otrzymane od hello symulowane `BLE` urządzenia, po kodu na powitania hello kopiowania `Untitled-1` okna edytora kodu w pliku.</span><span class="sxs-lookup"><span data-stu-id="aa821-152">toodeserialize hello `JSON` object that we receive from hello simulated `BLE` device, copy hello following code into hello `Untitled-1` file code editor window.</span></span> 

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

12. <span data-ttu-id="aa821-153">Zapisz plik hello jako `BleData.cs` naciskając `Ctrl`  +  `Shift`  +  `S` kluczy.</span><span class="sxs-lookup"><span data-stu-id="aa821-153">Save hello file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="aa821-154">Na powitania Zapisz jako okno dialogowe, w hello `Save as Type` menu rozwijanego wybierz `C# (*.cs;*.csx)` w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="aa821-154">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in hello following image:</span></span>

    ![Visual Studio Code Zapisz jako okna dialogowego](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="aa821-156">Utwórz nowy plik o nazwie `Untitled-1` przez naciśnięcie przycisku hello `Ctrl`  +  `N` kluczy.</span><span class="sxs-lookup"><span data-stu-id="aa821-156">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="aa821-157">Skopiuj i Wklej hello następującego fragmentu kodu na powitania `Untitled-1` pliku.</span><span class="sxs-lookup"><span data-stu-id="aa821-157">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> <span data-ttu-id="aa821-158">Ta klasa jest `Azure IoT Edge` moduł, który używamy toooutput hello danych otrzymywanych z naszych `BleConverterModule`.</span><span class="sxs-lookup"><span data-stu-id="aa821-158">This class is a `Azure IoT Edge` module, which we use toooutput hello data received from our `BleConverterModule`.</span></span>

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

15. <span data-ttu-id="aa821-159">Zapisz plik hello jako `DotNetPrinterModule.cs` naciskając `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="aa821-159">Save hello file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="aa821-160">Na powitania Zapisz jako okno dialogowe, w hello `Save as Type` menu rozwijanego wybierz `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="aa821-160">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="aa821-161">Utwórz nowy plik o nazwie `Untitled-1` przez naciśnięcie przycisku hello `Ctrl`  +  `N` kluczy.</span><span class="sxs-lookup"><span data-stu-id="aa821-161">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="aa821-162">Witaj toodeserialize `JSON` obiektu otrzymane od hello `BleConverterModule`, kopiowania i wklejania hello następujące fragment kodu do hello `Untitled-1` pliku.</span><span class="sxs-lookup"><span data-stu-id="aa821-162">toodeserialize hello `JSON` object that we receive from hello `BleConverterModule`, Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> 

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

18. <span data-ttu-id="aa821-163">Zapisz plik hello jako `BleConverterData.cs` naciskając `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="aa821-163">Save hello file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="aa821-164">Na powitania Zapisz jako okno dialogowe, w hello `Save as Type` menu rozwijanego wybierz `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="aa821-164">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="aa821-165">Utwórz nowy plik o nazwie `Untitled-1` przez naciśnięcie przycisku hello `Ctrl`  +  `N` kluczy.</span><span class="sxs-lookup"><span data-stu-id="aa821-165">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="aa821-166">Skopiuj i Wklej hello następującego fragmentu kodu na powitania `Untitled-1` pliku.</span><span class="sxs-lookup"><span data-stu-id="aa821-166">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

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

21. <span data-ttu-id="aa821-167">Zapisz plik hello jako `gw-config.json` naciskając `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="aa821-167">Save hello file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="aa821-168">Na powitania Zapisz jako okno dialogowe, w hello `Save as Type` menu rozwijanego wybierz `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span><span class="sxs-lookup"><span data-stu-id="aa821-168">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="aa821-169">Kopiowanie tooenable toohello pliku konfiguracji hello output katalogu, hello aktualizacji `IoTEdgeConverterModule.csproj` z hello następującego obiektu blob XML:</span><span class="sxs-lookup"><span data-stu-id="aa821-169">tooenable copying of hello configuration file toohello output directory, update hello `IoTEdgeConverterModule.csproj` with hello following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="aa821-170">Zaktualizowano Hello `IoTEdgeConverterModule.csproj` powinien wyglądać podobnie jak hello po obrazu:</span><span class="sxs-lookup"><span data-stu-id="aa821-170">hello updated `IoTEdgeConverterModule.csproj` should look like hello following image:</span></span>

    ![Visual Studio Code zaktualizować pliku .csproj](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="aa821-172">Utwórz nowy plik o nazwie `Untitled-1` przez naciśnięcie przycisku hello `Ctrl`  +  `N` kluczy.</span><span class="sxs-lookup"><span data-stu-id="aa821-172">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="aa821-173">Skopiuj i Wklej hello następującego fragmentu kodu na powitania `Untitled-1` pliku.</span><span class="sxs-lookup"><span data-stu-id="aa821-173">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="aa821-174">Zapisz plik hello jako `binplace.ps1` naciskając `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="aa821-174">Save hello file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="aa821-175">Na powitania Zapisz jako okno dialogowe, w hello `Save as Type` menu rozwijanego wybierz `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span><span class="sxs-lookup"><span data-stu-id="aa821-175">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="aa821-176">Tworzenie hello projektu przez naciśnięcie przycisku hello `Ctrl`  +  `Shift`  +  `B` kluczy.</span><span class="sxs-lookup"><span data-stu-id="aa821-176">Build hello project by pressing hello `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="aa821-177">Podczas kompilowania projektu hello na powitania po raz pierwszy, `Visual Studio Code` monit hello `No build task defined.` okna dialogowego w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="aa821-177">When you build hello project for hello first time, `Visual Studio Code` prompts you with hello `No build task defined.` dialog as seen in hello following image:</span></span>

    ![Zadanie kompilacji programu Visual Studio Code okna dialogowego](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="aa821-179">) kliknij hello `Configure Build Task` przycisku.</span><span class="sxs-lookup"><span data-stu-id="aa821-179">a) Click hello `Configure Build Task` button.</span></span>

    <span data-ttu-id="aa821-180">(b) w hello `Select a Task Runner` menu rozwijanego okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="aa821-180">b) In hello `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="aa821-181">Wybierz `.NET Core` w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="aa821-181">Select `.NET Core` as seen in hello following image:</span></span> 

    ![Visual Studio Code wybierz Okno zadań](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="aa821-183">hello c) kliknięcie przycisku `.NET Core` elementu tworzy hello `tasks.json` plików w sieci `.vscode` katalogu i otwiera plik w hello hello `code editor` okna.</span><span class="sxs-lookup"><span data-stu-id="aa821-183">c) Clicking hello `.NET Core` item creates hello `tasks.json` file in your `.vscode` directory and opens hello file in hello `code editor` window.</span></span> <span data-ttu-id="aa821-184">Nie jest toomodify nie konieczności ten plik, zamknij hello kartę.</span><span class="sxs-lookup"><span data-stu-id="aa821-184">There is no need toomodify this file, close hello tab.</span></span>

27.  <span data-ttu-id="aa821-185">Otwórz hello `Visual Studio Code` zintegrowane okno terminalu przez naciśnięcie przycisku hello `Ctrl`  +  `backtick` kluczy lub za pomocą menu hello `View`  ->  `Integrated Terminal` i typ **.\binplace.ps1**do hello `PowerShell` wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="aa821-185">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into hello `PowerShell` command prompt.</span></span> <span data-ttu-id="aa821-186">To polecenie powoduje skopiowanie wszystkich naszych zależności toohello katalogu wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="aa821-186">This command copies all our dependencies toohello output directory.</span></span>

28. <span data-ttu-id="aa821-187">Przejdź do katalogu wyjściowego projektów toohello w hello `Integrated Terminal` okna, wpisując **cd.\bin\Debug\netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="aa821-187">Navigate toohello projects output directory in hello `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="aa821-188">Uruchom hello przykładowy projekt, wpisując **. \gw.exe gw — config.json** do hello `Integrated Terminal` okno.</span><span class="sxs-lookup"><span data-stu-id="aa821-188">Run hello sample project by typing **.\gw.exe gw-config.json** into hello `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="aa821-189">Jeśli zostały wykonane kroki hello ściśle w tym samouczku, użytkownik powinien teraz korzystać z hello `Azure IoT Edge BLE Data Converter Module` przykładowy projekt w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="aa821-189">If you have followed hello steps in this tutorial closely, you should now be running hello `Azure IoT Edge BLE Data Converter Module` sample project as seen in hello following image:</span></span>
    
        ![Przykład symulowane urządzenie działa w programie Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="aa821-191">Jeśli chcesz, aby aplikacja hello tooterminate, naciśnij klawisz hello `<Enter>` klucza.</span><span class="sxs-lookup"><span data-stu-id="aa821-191">If you want tooterminate hello application, press hello `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="aa821-192">Nie zaleca się toouse `Ctrl`  +  `C` tooterminate hello `IoT Edge` bramy aplikacji (czyli **gw.exe**).</span><span class="sxs-lookup"><span data-stu-id="aa821-192">It is not recommended toouse `Ctrl` + `C` tooterminate hello `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="aa821-193">Ponieważ ta akcja może spowodować tooterminate procesu hello nieprawidłowo.</span><span class="sxs-lookup"><span data-stu-id="aa821-193">As this action may cause hello process tooterminate abnormally.</span></span>

