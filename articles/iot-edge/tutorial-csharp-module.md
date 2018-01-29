---
title: "Moduł Azure IoT krawędzi C# | Dokumentacja firmy Microsoft"
description: "Utwórz moduł krawędzi IoT z kodem C# i wdróż je do urządzenia"
services: iot-edge
keywords: 
author: kgremban
manager: timlt
ms.author: v-jamebr
ms.date: 11/15/2017
ms.topic: article
ms.service: iot-edge
ms.openlocfilehash: 4fd84904fb264fc61d0059d389347e05839162d2
ms.sourcegitcommit: 79683e67911c3ab14bcae668f7551e57f3095425
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="develop-and-deploy-a-c-iot-edge-module-to-your-simulated-device---preview"></a>Tworzenie i wdrażanie modułu krawędzi IoT C# w symulowane urządzenie — w wersji preview

Moduły krawędzi IoT umożliwia wdrażanie kodu, który implementuje logiki biznesowej bezpośrednio do urządzenia IoT krawędzi. W tym samouczku przedstawiono sposób tworzenia i wdrażania moduł krawędzi IoT filtrujące danych czujnika. Użyjesz symulowane urządzenie brzegowe IoT utworzoną w programie IoT Edge Azure wdrożenia symulowanego urządzenia w [Windows] [ lnk-tutorial1-win] lub [Linux] [ lnk-tutorial1-lin]samouczki. Ten samouczek zawiera informacje na temat wykonywania następujących czynności:    

> [!div class="checklist"]
> * Użyj programu Visual Studio Code, aby utworzyć moduł krawędzi IoT .NET core 2.0 w oparciu
> * Użyj programu Visual Studio Code i Docker, aby utworzyć obraz docker i opublikować ją w rejestrze 
> * Wdrażanie modułu do Twojego urządzenia IoT krawędzi
> * Widok wygenerowany danych


Moduł IoT krawędzi, który możesz utworzyć w tym samouczku filtruje temperatury dane generowane przez urządzenie. Tylko wysyła komunikaty powyżej jeśli temperatura przekracza określoną wartość progową. Ten typ analizy na krawędzi jest przydatne w przypadku zmniejszenie ilości danych przekazane i przechowywane w chmurze. 

## <a name="prerequisites"></a>Wymagania wstępne

* Urządzenie brzegowe IoT Azure utworzoną w pierwszym samouczku lub Szybki Start.
* Parametry połączenia klucza podstawowego dla urządzenia usługi IoT Edge.  
* [Visual Studio Code](https://code.visualstudio.com/). 
* [Rozszerzenie krawędzi IoT Azure dla programu Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-edge). 
* [C# dla rozszerzenia Visual Studio Code (obsługiwane przez OmniSharp)](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp). 
* [Docker](https://docs.docker.com/engine/installation/) na tym samym komputerze, na którym Visual Studio Code. Community Edition (CE) jest wystarczająca dla tego samouczka. 
* [.NET core 2.0 SDK](https://www.microsoft.com/net/core#windowscmd). 

## <a name="create-a-container-registry"></a>Tworzenie rejestru kontenerów
W tym samouczku umożliwia rozszerzenie Azure IoT krawędzi kodzie VS utworzenie modułu i Utwórz **obrazu kontenera** z plików. A następnie Wypchnij tego obrazu, aby **rejestru** który przechowywanych i zarządzanych obrazów. Ponadto można wdrożyć obraz z rejestru do uruchomienia na urządzeniu IoT krawędzi.  

W tym samouczku, można użyć dowolnego rejestru zgodnego Docker. Są dwa popularne Docker rejestru usług dostępnych w chmurze [rejestru kontenera Azure](https://docs.microsoft.com/azure/container-registry/) i [Centrum Docker](https://docs.docker.com/docker-hub/repos/#viewing-repository-tags). W tym samouczku korzysta z rejestru kontenera platformy Azure. 

1. W [portalu Azure](https://portal.azure.com), wybierz pozycję **Utwórz zasób** > **kontenery** > **rejestru kontenera Azure** .
2. Nadaj nazwę rejestru, wybierz subskrypcję, wybierz grupę zasobów i ustawić jednostki SKU **podstawowe**. 
3. Wybierz pozycję **Utwórz**.
4. Po utworzeniu kontenera rejestru przejdź do niego i wybierz **klucze dostępu**. 
5. Przełącz **administrator** do **włączyć**.
6. Skopiuj wartości **logowania serwera**, **Username**, i **hasło**. Te wartości będą używane w dalszej części tego samouczka. 

## <a name="create-an-iot-edge-module-project"></a>Tworzenie projektu modułu krawędzi IoT
Pokaż następujące kroki należy jak utworzyć moduł krawędzi IoT na podstawie .NET core 2.0 przy użyciu programu Visual Studio Code i rozszerzenie Azure IoT krawędzi.
1. W programie Visual Studio Code, wybierz **widoku** > **zintegrowane terminali** otworzyć terminal zintegrowane kodzie VS.
3. W terminalu zintegrowanego, wprowadź następujące polecenie, aby zainstalować (lub zaktualizować) **AzureIoTEdgeModule** szablonu w dotnet:

    ```cmd/sh
    dotnet new -i Microsoft.Azure.IoT.Edge.Module
    ```

2. Tworzenie projektu dla nowego modułu. Poniższe polecenie tworzy folder projektu **FilterModule**, w bieżącym folderze roboczych:

    ```cmd/sh
    dotnet new aziotedgemodule -n FilterModule
    ```
 
3. Wybierz **pliku** > **Otwórz Folder**.
4. Przejdź do **FilterModule** folder i kliknij przycisk **wybierz Folder** otworzyć projektu w kodzie VS.
5. W kodzie VS explorer, kliknij przycisk **Program.cs** go otworzyć.

   ![Otwórz plik Program.cs][1]

6. W górnej części **FilterModule** przestrzeni nazw, Dodaj trzy `using` instrukcje dla typów używanych w późniejszym czasie na:

    ```csharp
    using System.Collections.Generic;     // for KeyValuePair<>
    using Microsoft.Azure.Devices.Shared; // for TwinCollection
    using Newtonsoft.Json;                // for JsonConvert
    ```

6. Dodaj `temperatureThreshold` zmienną **Program** klasy. Ta zmienna Określa wartość, której może przekraczać zmierzone temperatury dane do wysłania do Centrum IoT. 

    ```csharp
    static int temperatureThreshold { get; set; } = 25;
    ```

7. Dodaj `MessageBody`, `Machine`, i `Ambient` klasy do **Program** klasy. Te klasy definiują oczekiwano elementu schema dla treści wiadomości przychodzących.

    ```csharp
    class MessageBody
    {
        public Machine machine {get;set;}
        public Ambient ambient {get; set;}
        public string timeCreated {get; set;}
    }
    class Machine
    {
       public double temperature {get; set;}
       public double pressure {get; set;}         
    }
    class Ambient
    {
       public double temperature {get; set;}
       public int humidity {get; set;}         
    }
    ```

8. W **Init** metoda, kod tworzy i konfiguruje **DeviceClient** obiektu. Ten obiekt umożliwia modułu do nawiązania połączenia lokalnego środowiska uruchomieniowego Azure IoT krawędzi do wysyłania i odbierania wiadomości. Parametry połączenia używane w **Init** metody został dostarczony do modułu przez środowisko uruchomieniowe IoT krawędzi. Po utworzeniu **DeviceClient**, kod odczytuje TemperatureThreshold dwie modułu odpowiednie właściwości i rejestruje wywołanie zwrotne do odbierania wiadomości z Centrum IoT krawędzi za pośrednictwem **input1**punktu końcowego. Zastąp `SetInputMessageHandlerAsync` metody z nową i Dodaj `SetDesiredPropertyUpdateCallbackAsync` metodę dla żądanej właściwości aktualizacji. Aby to zrobić, Zamień ostatni wiersz **Init** metodę z następującym kodem:

    ```csharp
    // Register callback to be called when a message is received by the module
    // await ioTHubModuleClient.SetImputMessageHandlerAsync("input1", PipeMessage, iotHubModuleClient);

    // Read TemperatureThreshold from Module Twin Desired Properties
    var moduleTwin = await ioTHubModuleClient.GetTwinAsync();
    var moduleTwinCollection = moduleTwin.Properties.Desired;
    if (moduleTwinCollection["TemperatureThreshold"] != null)
    {
        temperatureThreshold = moduleTwinCollection["TemperatureThreshold"];
    }

    // Attach callback for Twin desired properties updates
    await ioTHubModuleClient.SetDesiredPropertyUpdateCallbackAsync(onDesiredPropertiesUpdate, null);

    // Register callback to be called when a message is received by the module
    await ioTHubModuleClient.SetInputMessageHandlerAsync("input1", FilterMessages, ioTHubModuleClient);
    ```

9. Dodaj `onDesiredPropertiesUpdate` metodę **Program** klasy. Ta metoda odbiera aktualizacje na odpowiednie właściwości z dwie modułu i aktualizuje **temperatureThreshold** ze zmienną. Wszystkie moduły mają własne dwie moduł, który umożliwia skonfigurowanie z kodem uruchomionym wewnątrz modułu bezpośrednio z chmury.

    ```csharp
    static Task onDesiredPropertiesUpdate(TwinCollection desiredProperties, object userContext)
    {
        try
        {
            Console.WriteLine("Desired property change:");
            Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));

            if (desiredProperties["TemperatureThreshold"]!=null)
                temperatureThreshold = desiredProperties["TemperatureThreshold"];

        }
        catch (AggregateException ex)
        {
            foreach (Exception exception in ex.InnerExceptions)
            {
                Console.WriteLine();
                Console.WriteLine("Error when receiving desired property: {0}", exception);
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error when receiving desired property: {0}", ex.Message);
        }
        return Task.CompletedTask;
    }
    ```

10. Zastąp `PipeMessage` metody z `FilterMessages` metody. Ta metoda jest wywoływana, gdy moduł odbiera komunikat z Centrum IoT krawędzi. Odfiltrowuje wiadomości, które zgłosiły temperatury poniżej progu temperatura określonego przez dwie modułu. Dodano również **MessageType** właściwości komunikat z wartością ustawioną na **alertu**. 

    ```csharp
    static async Task<MessageResponse> FilterMessages(Message message, object userContext)
    {
        int counterValue = Interlocked.Increment(ref counter);

        try {
            DeviceClient deviceClient = (DeviceClient)userContext;

            byte[] messageBytes = message.GetBytes();
            string messageString = Encoding.UTF8.GetString(messageBytes);
            Console.WriteLine($"Received message {counterValue}: [{messageString}]");

            // Get message body
            var messageBody = JsonConvert.DeserializeObject<MessageBody>(messageString);

            if (messageBody != null && messageBody.machine.temperature > temperatureThreshold)
            {
                Console.WriteLine($"Machine temperature {messageBody.machine.temperature} " +
                    $"exceeds threshold {temperatureThreshold}");
                var filteredMessage = new Message(messageBytes);
                foreach (KeyValuePair<string, string> prop in message.Properties)
                {
                    filteredMessage.Properties.Add(prop.Key, prop.Value);
                }

                filteredMessage.Properties.Add("MessageType", "Alert");
                await deviceClient.SendEventAsync("output1", filteredMessage);
            }

            // Indicate that the message treatment is completed
            return MessageResponse.Completed;
        }
        catch (AggregateException ex)
        {
            foreach (Exception exception in ex.InnerExceptions)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", exception);
            }
            // Indicate that the message treatment is not completed
            DeviceClient deviceClient = (DeviceClient)userContext;
            return MessageResponse.Abandoned;
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
            // Indicate that the message treatment is not completed
            DeviceClient deviceClient = (DeviceClient)userContext;
            return MessageResponse.Abandoned;
        }
    }
    ```

11. Aby skompilować projekt, kliknij prawym przyciskiem myszy **FilterModule.csproj** plików w Eksploratorze i kliknij przycisk **krawędzi IoT Tworzenie modułu**. Ten proces kompiluje modułu i eksportuje dane binarne i jego zależności w folderze, który jest używany do tworzenia obrazu Docker.

   ![Utworzenie modułu krawędzi IoT][2]

## <a name="create-a-docker-image-and-publish-it-to-your-registry"></a>Tworzenie obrazu Docker i publikowanie go do rejestru

1. W Eksploratorze kodzie VS rozwiń **Docker** folderu. Następnie rozwiń folder dla danej platformy kontenera albo **linux x64** lub **windows nano**.

   ![Wybierz platformę kontenera Docker][3]

2. Kliknij prawym przyciskiem myszy **plik Dockerfile** plik i kliknij przycisk **krawędzi IoT Tworzenie modułu Docker obrazu**. 
3. W **wybierz Folder** okna, przejdź do albo wprowadź `./bin/Debug/netcoreapp2.0/publish`. Kliknij przycisk **wybierz Folder jako EXE_DIR**.
4. W polu tekstowym wyskakujących w górnej części okna kodu programu VS wprowadź nazwę obrazu. Na przykład: `<your container registry address>/filtermodule:latest`. Adres rejestru kontenera jest taki sam jak serwer logowania, które zostały skopiowane z rejestru. Powinna być w formie `<your container registry name>.azurecr.io`.
5. Zaloguj się do Docker, wprowadzając następujące polecenie w kodzie VS terminal zintegrowane: 
     
   ```csh/sh
   docker login -u <username> -p <password> <Login server>
   ```
        
   Użyj nazwy użytkownika, hasło i serwer logowania, skopiowany z rejestru kontenera platformy Azure podczas jego tworzenia.

3. Wypchnij obrazu do repozytorium Docker. Wybierz **widoku** > **palety polecenia** i wyszukaj **krawędzi: Push krawędzi IoT modułu Docker obrazu** polecenia menu. Wprowadź nazwę obrazu w polu tekstowym wyskakujących w górnej części okna kodu programu VS. Użyj takiej samej nazwy obraz, którego użyto w kroku 4.

## <a name="add-registry-credentials-to-edge-runtime"></a>Dodawanie poświadczeń rejestru do środowiska wykonawczego krawędzi
Dodaj poświadczenia do rejestru do środowiska wykonawczego Edge na komputerze, na którym są uruchomione Twoje urządzenie brzegowe. Te poświadczenia zapewniają dostęp środowiska uruchomieniowego do ściągnięcia kontenera. 

- W systemie Windows uruchom następujące polecenie:
    
    ```cmd/sh
    iotedgectl login --address <your container registry address> --username <username> --password <password> 
    ```

- Dla systemu Linux uruchom następujące polecenie:
    
    ```cmd/sh
    sudo iotedgectl login --address <your container registry address> --username <username> --password <password> 
    ```

## <a name="run-the-solution"></a>Uruchamianie rozwiązania

1. W [portalu Azure](https://portal.azure.com), przejdź do Centrum IoT.
2. Przejdź do pozycji **IoT Edge (wersja zapoznawcza)** i wybierz urządzenie usługi IoT Edge.
3. Wybierz **ustawić modułów**. 
2. Sprawdź, czy **tempSensor** modułu jest wypełniane automatycznie. Jeśli nie, należy dodać ją za pomocą następujących czynności:
    1. Wybierz **Dodaj moduł krawędzi IoT**.
    2. W **nazwa** wprowadź `tempSensor`.
    3. W **identyfikatora URI obrazu** wprowadź `microsoft/azureiotedge-simulated-temperature-sensor:1.0-preview`.
    4. Pozostaw innych ustawień bez zmian i kliknij przycisk **zapisać**.
9. Dodaj **filterModule** moduł, który został utworzony w poprzednich sekcjach. 
    1. Wybierz **Dodaj moduł krawędzi IoT**.
    2. W **nazwa** wprowadź `filterModule`.
    3. W **identyfikatora URI obrazu** wprowadź swój adres obrazu, na przykład `<your container registry address>/filtermodule:latest`.
    4. Sprawdź **włączyć** , dzięki czemu można edytować dwie modułu. 
    5. Zastąp dane JSON w polu tekstowym dla modułu dwie następujące JSON: 

        ```json
        {
           "properties.desired":{
              "TemperatureThreshold":25
           }
        }
        ```
 
    6. Kliknij pozycję **Zapisz**.
12. Kliknij przycisk **Dalej**.
13. W **Określ tras** kroku, skopiuj kod JSON poniżej w polu tekstowym. Moduły opublikować wszystkie komunikaty do środowiska wykonawczego krawędzi. Deklaracyjne reguły w środowisku uruchomieniowym definiują, do których przepływu wiadomości. W tym samouczku należy na dwa sposoby. Pierwszy trasy transportu wiadomości z czujnika temperatury w module filtru za pośrednictwem punktu końcowego "input1", który jest punkt końcowy, który został skonfigurowany z **FilterMessages** programu obsługi. Drugi trasy transportu wiadomości z modułem filtru do Centrum IoT. W tej trasy `upstream` jest specjalne lokalizacji docelowej, która informuje krawędzi koncentratora do wysyłania komunikatów do Centrum IoT. 

    ```json
    {
       "routes":{
          "sensorToFilter":"FROM /messages/modules/tempSensor/outputs/temperatureOutput INTO BrokeredEndpoint(\"/modules/filterModule/inputs/input1\")",
          "filterToIoTHub":"FROM /messages/modules/filterModule/outputs/output1 INTO $upstream"
       }
    }
    ```

4. Kliknij przycisk **Dalej**.
5. W **szablon przeglądu** kroku, kliknij przycisk **przesyłania**. 
6. Wróć do strony szczegółów urządzenia IoT krawędzi, a następnie kliknij przycisk **Odśwież**. Powinien zostać wyświetlony nowy **filtermodule** uruchomiona wraz z **tempSensor** modułu i **środowiska uruchomieniowego krawędzi IoT**. 

## <a name="view-generated-data"></a>Widok wygenerowany danych

Aby monitorować urządzenia do chmury wiadomości wysyłane z urządzenia IoT krawędzi do Centrum IoT:
1. Rozszerzenia Azure IoT Toolkit należy skonfigurować parametry połączenia Centrum IoT: 
    1. Otwórz Eksploratora kodzie VS wybierając **widoku** > **Explorer**. 
    3. W Eksploratorze kliknij **urządzenia IOT HUB** , a następnie kliknij przycisk **...** . Kliknij przycisk **ustawić parametry połączenia Centrum IoT** , a następnie wprowadź parametry połączenia dla Centrum IoT, które urządzenia IoT krawędzi łączy w wyskakującym oknie. 

        Aby znaleźć ciąg połączenia, kliknij Kafelek Centrum IoT w portalu Azure, a następnie kliknij przycisk **zasady dostępu współużytkowanego**. W **zasady dostępu współużytkowanego**, kliknij przycisk **iothubowner** zasad i skopiuj połączenia Centrum IoT ciąg w **iothubowner** okna.   

1. Do monitorowania danych otrzymywanych przez Centrum IoT, wybierz **widoku** > **palety polecenia** i wyszukaj **IoT: rozpocząć monitorowanie komunikat D2C** polecenia menu. 
2. Aby zatrzymać monitorowanie danych, należy użyć **IoT: zatrzymać monitorowanie komunikat D2C** polecenia menu. 

## <a name="next-steps"></a>Kolejne kroki

W tym samouczku utworzony moduł IoT krawędzi, który zawiera kod, aby filtrować nieprzetworzone dane generowane przez urządzenia IoT krawędzi. Można kontynuować do jednej z następujących samouczków, aby uzyskać informacje o innych metod, które ułatwiają krawędź IoT Azure możesz przekształcić w danych biznesowych na krawędzi.

> [!div class="nextstepaction"]
> [Wdrażanie funkcji platformy Azure jako moduł](tutorial-deploy-function.md)
> [wdrożenia usługi Azure Stream Analytics jako moduł](tutorial-deploy-stream-analytics.md)


<!-- Links -->
[lnk-tutorial1-win]: tutorial-simulate-device-windows.md
[lnk-tutorial1-lin]: tutorial-simulate-device-linux.md

<!-- Images -->
[1]: ./media/tutorial-csharp-module/programcs.png
[2]: ./media/tutorial-csharp-module/build-module.png
[3]: ./media/tutorial-csharp-module/docker-os.png
