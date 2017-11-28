---
title: "Utwórz moduł Azure IoT krawędzi języku C# | Dokumentacja firmy Microsoft"
description: "W tym samouczku ilustrację jak napisać cz modułu konwertera danych przy użyciu najnowszych pakietów NuGet krawędzi IoT Azure, programu Visual Studio Code i C#."
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
ms.openlocfilehash: 7175ffc8de2c043593d61143b402484d33e4a8cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="e6d35-104">Utwórz moduł Azure IoT krawędzi z C & #x23;</span><span class="sxs-lookup"><span data-stu-id="e6d35-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="e6d35-105">Jak utworzyć moduł, dla których są wyświetlane w tym samouczku `Azure IoT Edge` przy użyciu `Visual Studio Code` i `C#`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-105">This tutorial showcases how to create a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="e6d35-106">W tym samouczku będziemy przeprowadzenie konfiguracji środowiska i jak napisać [cz](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) modułu konwertera danych przy użyciu najnowszych `Azure IoT Edge NuGet` pakietów.</span><span class="sxs-lookup"><span data-stu-id="e6d35-106">In this tutorial, we walk through environment set-up and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="e6d35-107">Ten samouczek używa `.NET Core SDK`, który obsługuje zgodności między platformami.</span><span class="sxs-lookup"><span data-stu-id="e6d35-107">This tutorial is using the `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="e6d35-108">Następujące samouczek jest przeznaczony przy użyciu `Windows 10` systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="e6d35-108">The following tutorial is written using the `Windows 10` operating system.</span></span> <span data-ttu-id="e6d35-109">Niektóre polecenia w tym samouczku mogą być różne w zależności od Twojego `development environment`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-109">Some of the commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e6d35-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e6d35-110">Prerequisites</span></span>

<span data-ttu-id="e6d35-111">W tej sekcji możemy konfiguracji środowiska pod kątem `Azure IoT Edge` programowanie modułu.</span><span class="sxs-lookup"><span data-stu-id="e6d35-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="e6d35-112">Dotyczy ona obu **64-bitowym systemie Windows** i **64-bitowego systemu Linux (8 Ubuntu/Debian)** systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="e6d35-112">It applies to both **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="e6d35-113">Następujące oprogramowanie jest wymagane:</span><span class="sxs-lookup"><span data-stu-id="e6d35-113">The following software is required:</span></span>

- [<span data-ttu-id="e6d35-114">Klient Git</span><span class="sxs-lookup"><span data-stu-id="e6d35-114">Git Client</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="e6d35-115">Zestaw SDK dla platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="e6d35-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="e6d35-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e6d35-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="e6d35-117">Nie trzeba sklonować repozytorium dla tego przykładu, jednak cały kod przykładowy omówione w tym samouczku znajduje się w następujących repozytorium:</span><span class="sxs-lookup"><span data-stu-id="e6d35-117">You do not need to clone the repo for this sample, however all of the sample code discussed in this tutorial is located in the following repository:</span></span>

- <span data-ttu-id="e6d35-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="e6d35-119">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="e6d35-119">Getting started</span></span>

1. <span data-ttu-id="e6d35-120">Zainstaluj `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="e6d35-121">Zainstaluj `Visual Studio Code` i `C# extension` z witryny Marketplace kodu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e6d35-121">Install `Visual Studio Code` and the `C# extension` from the Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="e6d35-122">Wyświetlić [krótki samouczek wideo](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) o tym, jak rozpocząć pracę przy użyciu `Visual Studio Code` i `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how to get started using `Visual Studio Code` and the `.NET Core SDK`.</span></span>

## <a name="creating-the-azure-iot-edge-converter-module"></a><span data-ttu-id="e6d35-123">Tworzenie modułu konwertera krawędzi IoT Azure</span><span class="sxs-lookup"><span data-stu-id="e6d35-123">Creating the Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="e6d35-124">Zainicjuj nowy `.NET Core` klasy projektu biblioteki C#:</span><span class="sxs-lookup"><span data-stu-id="e6d35-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="e6d35-125">Otwórz okno wiersza polecenia (`Windows + R` -> `cmd` -> `enter`).</span><span class="sxs-lookup"><span data-stu-id="e6d35-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="e6d35-126">Przejdź do folderu, w którym chcesz utworzyć `C#` projektu.</span><span class="sxs-lookup"><span data-stu-id="e6d35-126">Navigate to the folder where you'd like to create the `C#` project.</span></span>
    - <span data-ttu-id="e6d35-127">Typ **dotnet nowej biblioteki klas -o IoTEdgeConverterModule -f netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="e6d35-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="e6d35-128">To polecenie tworzy pustą klasę o nazwie `Class1.cs` w katalogu projektów.</span><span class="sxs-lookup"><span data-stu-id="e6d35-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="e6d35-129">Przejdź do folderu, w którym właśnie utworzyliśmy projektu biblioteki klas, wpisując **cd IoTEdgeConverterModule**.</span><span class="sxs-lookup"><span data-stu-id="e6d35-129">Navigate to the folder where we just created the class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="e6d35-130">Otwórz projekt w `Visual Studio Code` , wpisując **kodu.**.</span><span class="sxs-lookup"><span data-stu-id="e6d35-130">Open the project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="e6d35-131">Po otwarciu projektu w `Visual Studio Code`, kliknij **IoTEdgeConverterModule.csproj** można otworzyć pliku, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="e6d35-131">Once the project is opened in `Visual Studio Code`, click on the **IoTEdgeConverterModule.csproj** to open the file as shown in the following image:</span></span>

    ![Okno edycji w usłudze Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="e6d35-133">Wstaw `XML` pokazano poniższy fragment kodu od zamknięcia obiektu blob `PropertyGroup` znacznika i zamykania `Project` tagów; wiersz sześć w poprzednim obrazu i Zapisz plik naciskając `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-133">Insert the `XML` blob shown in the following code snippet between the closing `PropertyGroup` tag and the closing `Project` tag; line six in the preceding image and save the file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="e6d35-134">Po zapisaniu `.csproj` pliku `Visual Studio Code` powinien monit o `unresolved dependencies` okna dialogowego, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="e6d35-134">Once you save the `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in the following image:</span></span> 

    ![Okno dialogowe programu Visual Studio Code przywracania zależności](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="e6d35-136">) kliknij `Restore` Aby przywrócić wszystkie odwołania w projektach `.csproj` w tym pliku `PackageReferences` dodaliśmy.</span><span class="sxs-lookup"><span data-stu-id="e6d35-136">a) Click `Restore` to restore all of the references in the projects `.csproj` file including the `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="e6d35-137">(b) `Visual Studio Code` automatycznie tworzy `project.assets.json` pliku w projektach `obj` folderu.</span><span class="sxs-lookup"><span data-stu-id="e6d35-137">b) `Visual Studio Code` automatically creates the `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="e6d35-138">Ten plik zawiera informacje o zależności projektu, aby szybciej kolejnych operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="e6d35-138">This file contains information about your project's dependencies to make subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="e6d35-139">`.NET Core Tools`znajdują się teraz na podstawie programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="e6d35-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="e6d35-140">Co oznacza, że `.csproj` plik projektu jest tworzony zamiast `project.json`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="e6d35-141">Jeśli `Visual Studio Code` Monituj użytkownika o jest prawidłowy, możemy go ręcznie.</span><span class="sxs-lookup"><span data-stu-id="e6d35-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="e6d35-142">Otwórz `Visual Studio Code` zintegrowane okno terminalu, naciskając klawisz `Ctrl`  +  `backtick` kluczy lub przy użyciu menu `View`  ->  `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-142">Open the `Visual Studio Code` integrated terminal window by pressing the `Ctrl` + `backtick` keys or using the menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="e6d35-143">W `Integrated Terminal` typ okna **przywracania dotnet**.</span><span class="sxs-lookup"><span data-stu-id="e6d35-143">In the `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="e6d35-144">Zmień nazwę `Class1.cs` pliku `BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-144">Rename the `Class1.cs` file to `BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="e6d35-145">) Aby zmienić nazwę pliku najpierw kliknąć plik, naciśnij klawisz `F2` klucza.</span><span class="sxs-lookup"><span data-stu-id="e6d35-145">a) To rename the file first click on the file then press the `F2` key.</span></span>
    
    <span data-ttu-id="e6d35-146">(b) wpisz nazwę nowego **BleConverterModule**, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="e6d35-146">b) Type in the new name **BleConverterModule**, as seen in the following image:</span></span>

    ![Visual Studio Code zmiana nazwy klasy](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="e6d35-148">Zastąp istniejący kod w `BleConverterModule.cs` plik, kopiując i wklejając następujący fragment kodu do Twojej `BleConverterModule.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="e6d35-148">Replace the existing code in the `BleConverterModule.cs` file by copying and pasting the following code snippet into your `BleConverterModule.cs` file.</span></span>

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

9. <span data-ttu-id="e6d35-149">Zapisz plik, naciskając klawisz `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-149">Save the file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="e6d35-150">Utwórz nowy plik o nazwie `Untitled-1` naciskając `Ctrl`  +  `N` kluczy, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="e6d35-150">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys as seen in the following image:</span></span>

    ![Visual Studio Code nowy plik.](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="e6d35-152">Do deserializacji `JSON` obiektu otrzymane od symulowane `BLE` urządzenie, skopiuj następujący kod do `Untitled-1` okna edytora pliku kodu.</span><span class="sxs-lookup"><span data-stu-id="e6d35-152">To deserialize the `JSON` object that we receive from the simulated `BLE` device, copy the following code into the `Untitled-1` file code editor window.</span></span> 

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

12. <span data-ttu-id="e6d35-153">Zapisz plik jako `BleData.cs` naciskając `Ctrl`  +  `Shift`  +  `S` kluczy.</span><span class="sxs-lookup"><span data-stu-id="e6d35-153">Save the file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="e6d35-154">Na Zapisz jako okno dialogowe w `Save as Type` menu rozwijanego wybierz `C# (*.cs;*.csx)` jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="e6d35-154">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in the following image:</span></span>

    ![Visual Studio Code Zapisz jako okna dialogowego](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="e6d35-156">Utwórz nowy plik o nazwie `Untitled-1` naciskając `Ctrl`  +  `N` kluczy.</span><span class="sxs-lookup"><span data-stu-id="e6d35-156">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="e6d35-157">Skopiuj i wklej poniższy fragment kodu do `Untitled-1` pliku.</span><span class="sxs-lookup"><span data-stu-id="e6d35-157">Copy and paste the following code snippet into the `Untitled-1` file.</span></span> <span data-ttu-id="e6d35-158">Ta klasa jest `Azure IoT Edge` moduł, który używamy danych wyjściowych danych otrzymywanych z naszych `BleConverterModule`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-158">This class is a `Azure IoT Edge` module, which we use to output the data received from our `BleConverterModule`.</span></span>

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

15. <span data-ttu-id="e6d35-159">Zapisz plik jako `DotNetPrinterModule.cs` naciskając `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-159">Save the file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="e6d35-160">Na Zapisz jako okno dialogowe w `Save as Type` menu rozwijanego wybierz `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-160">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="e6d35-161">Utwórz nowy plik o nazwie `Untitled-1` naciskając `Ctrl`  +  `N` kluczy.</span><span class="sxs-lookup"><span data-stu-id="e6d35-161">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="e6d35-162">Do deserializacji `JSON` obiektu otrzymane od `BleConverterModule`, Kopiuj i wklej poniższy kod fragment do `Untitled-1` pliku.</span><span class="sxs-lookup"><span data-stu-id="e6d35-162">To deserialize the `JSON` object that we receive from the `BleConverterModule`, Copy and paste the following code snippet into the `Untitled-1` file.</span></span> 

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

18. <span data-ttu-id="e6d35-163">Zapisz plik jako `BleConverterData.cs` naciskając `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-163">Save the file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="e6d35-164">Na Zapisz jako okno dialogowe w `Save as Type` menu rozwijanego wybierz `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-164">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="e6d35-165">Utwórz nowy plik o nazwie `Untitled-1` naciskając `Ctrl`  +  `N` kluczy.</span><span class="sxs-lookup"><span data-stu-id="e6d35-165">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="e6d35-166">Skopiuj i wklej poniższy fragment kodu do `Untitled-1` pliku.</span><span class="sxs-lookup"><span data-stu-id="e6d35-166">Copy and paste the following code snippet into the `Untitled-1` file.</span></span>

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

21. <span data-ttu-id="e6d35-167">Zapisz plik jako `gw-config.json` naciskając `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-167">Save the file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="e6d35-168">Na Zapisz jako okno dialogowe w `Save as Type` menu rozwijanego wybierz `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-168">On the save as dialog box, in the `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="e6d35-169">Aby umożliwić kopiowanie pliku konfiguracji do katalogu wyjściowego, należy zaktualizować `IoTEdgeConverterModule.csproj` przy użyciu następującego obiektu blob XML:</span><span class="sxs-lookup"><span data-stu-id="e6d35-169">To enable copying of the configuration file to the output directory, update the `IoTEdgeConverterModule.csproj` with the following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="e6d35-170">Zaktualizowany interfejs `IoTEdgeConverterModule.csproj` powinno wyglądać podobnie do poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="e6d35-170">The updated `IoTEdgeConverterModule.csproj` should look like the following image:</span></span>

    ![Visual Studio Code zaktualizować pliku .csproj](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="e6d35-172">Utwórz nowy plik o nazwie `Untitled-1` naciskając `Ctrl`  +  `N` kluczy.</span><span class="sxs-lookup"><span data-stu-id="e6d35-172">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="e6d35-173">Skopiuj i wklej poniższy fragment kodu do `Untitled-1` pliku.</span><span class="sxs-lookup"><span data-stu-id="e6d35-173">Copy and paste the following code snippet into the `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="e6d35-174">Zapisz plik jako `binplace.ps1` naciskając `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-174">Save the file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="e6d35-175">Na Zapisz jako okno dialogowe w `Save as Type` menu rozwijanego wybierz `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span><span class="sxs-lookup"><span data-stu-id="e6d35-175">On the save as dialog box, in the `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="e6d35-176">Tworzenie projektu przez naciśnięcie przycisku `Ctrl`  +  `Shift`  +  `B` kluczy.</span><span class="sxs-lookup"><span data-stu-id="e6d35-176">Build the project by pressing the `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="e6d35-177">Podczas kompilowania projektu po raz pierwszy, `Visual Studio Code` monituje o `No build task defined.` okna dialogowego, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="e6d35-177">When you build the project for the first time, `Visual Studio Code` prompts you with the `No build task defined.` dialog as seen in the following image:</span></span>

    ![Zadanie kompilacji programu Visual Studio Code okna dialogowego](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="e6d35-179">) kliknij `Configure Build Task` przycisku.</span><span class="sxs-lookup"><span data-stu-id="e6d35-179">a) Click the `Configure Build Task` button.</span></span>

    <span data-ttu-id="e6d35-180">(b) w `Select a Task Runner` menu rozwijanego okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e6d35-180">b) In the `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="e6d35-181">Wybierz `.NET Core` jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="e6d35-181">Select `.NET Core` as seen in the following image:</span></span> 

    ![Visual Studio Code wybierz Okno zadań](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="e6d35-183">Kliknięcie przycisku c) `.NET Core` tworzy element `tasks.json` plików w sieci `.vscode` katalogu i otwarcie pliku w `code editor` okna.</span><span class="sxs-lookup"><span data-stu-id="e6d35-183">c) Clicking the `.NET Core` item creates the `tasks.json` file in your `.vscode` directory and opens the file in the `code editor` window.</span></span> <span data-ttu-id="e6d35-184">Nie istnieje potrzeba do modyfikowania tego pliku, zamknij karcie.</span><span class="sxs-lookup"><span data-stu-id="e6d35-184">There is no need to modify this file, close the tab.</span></span>

27.  <span data-ttu-id="e6d35-185">Otwórz `Visual Studio Code` zintegrowane okno terminalu, naciskając klawisz `Ctrl`  +  `backtick` kluczy lub przy użyciu menu `View`  ->  `Integrated Terminal` i typ **.\binplace.ps1** do `PowerShell` wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e6d35-185">Open the `Visual Studio Code` integrated terminal window by pressing the `Ctrl` + `backtick` keys or using the menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into the `PowerShell` command prompt.</span></span> <span data-ttu-id="e6d35-186">To polecenie powoduje skopiowanie wszystkich naszych zależności do katalogu wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="e6d35-186">This command copies all our dependencies to the output directory.</span></span>

28. <span data-ttu-id="e6d35-187">Przejdź do katalogu wyjściowego projekty w `Integrated Terminal` okna, wpisując **cd.\bin\Debug\netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="e6d35-187">Navigate to the projects output directory in the `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="e6d35-188">Uruchom przykładowy projekt, wpisując **. \gw.exe gw — config.json** do `Integrated Terminal` okno.</span><span class="sxs-lookup"><span data-stu-id="e6d35-188">Run the sample project by typing **.\gw.exe gw-config.json** into the `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="e6d35-189">Jeśli zostały wykonane kroki ściśle w tym samouczku, teraz powinny być uruchomiono `Azure IoT Edge BLE Data Converter Module` przykładowy projekt, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="e6d35-189">If you have followed the steps in this tutorial closely, you should now be running the `Azure IoT Edge BLE Data Converter Module` sample project as seen in the following image:</span></span>
    
        ![Przykład symulowane urządzenie działa w programie Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="e6d35-191">Jeśli chcesz zakończyć tę aplikację, naciśnij klawisz `<Enter>` klucza.</span><span class="sxs-lookup"><span data-stu-id="e6d35-191">If you want to terminate the application, press the `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="e6d35-192">Nie zaleca się używania `Ctrl`  +  `C` zakończenie `IoT Edge` bramy aplikacji (czyli **gw.exe**).</span><span class="sxs-lookup"><span data-stu-id="e6d35-192">It is not recommended to use `Ctrl` + `C` to terminate the `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="e6d35-193">Ponieważ ta akcja może spowodować przerwanie wyjątkowo procesu.</span><span class="sxs-lookup"><span data-stu-id="e6d35-193">As this action may cause the process to terminate abnormally.</span></span>

