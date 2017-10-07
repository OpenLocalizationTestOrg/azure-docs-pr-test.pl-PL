---
title: "pliki aaaUpload z urządzeń tooAzure Centrum IoT z platformą .NET | Dokumentacja firmy Microsoft"
description: "Jak tooupload pliki z chmury toohello urządzenia przy użyciu urządzenia Azure IoT SDK dla platformy .NET. Przekazano pliki są przechowywane w kontenerze obiektu blob magazynu Azure."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: elioda
ms.openlocfilehash: 07d555f6ba8b067bbd3233bc8eebaa220ad2388b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a>Przekazywanie plików z chmury toohello urządzenie z Centrum IoT przy użyciu platformy .NET

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

W tym samouczku opiera się na powitania kodu w hello [wysyłać chmury do urządzenia z Centrum IoT](iot-hub-csharp-csharp-c2d.md) tooshow samouczka możesz jak toouse hello możliwości przekazywania pliku z Centrum IoT. Jak przedstawiono na:

- Bezpieczne udostępnianie urządzenia platformy Azure blob identyfikatora URI pobierania pliku.
- Użyj hello pliku hello Centrum IoT pliku przekazywania powiadomień tootrigger przetwarzania w sieci wewnętrznej aplikacji.

Witaj [Rozpoczynanie pracy z Centrum IoT](iot-hub-csharp-csharp-getstarted.md) i [wysyłać chmury do urządzenia z Centrum IoT](iot-hub-csharp-csharp-c2d.md) samouczki przedstawiają hello podstawowych urządzenia do chmury i chmury do urządzenia obsługi funkcji Centrum IoT. Witaj [wiadomości procesu urządzenia do chmury](iot-hub-csharp-csharp-process-d2c.md) samouczek przedstawia sposób tooreliably magazynu urządzenia do chmury wiadomości w magazynie obiektów blob platformy Azure. Jednak w niektórych scenariuszach nie można łatwo mapować hello dane, które urządzenia wysłać w wiadomości powitania od stosunkowo mały urządzenia do chmury, które akceptuje Centrum IoT. Na przykład:

* Duże pliki, które zawierają obrazów
* Filmy wideo
* Dane wibrację próbkowanych zgodnie o dużej częstotliwości
* Niektóre formularz wstępnie przetworzonych danych

Pliki te są zwykle partii przetwarzania w chmurze hello za pomocą narzędzi takich jak [fabryki danych Azure](../data-factory/index.md) lub hello [Hadoop](../hdinsight/index.md) stosu. Jeśli potrzebujesz tooupload pliki z urządzenia, można nadal używać hello bezpieczeństwa i niezawodności Centrum IoT.

Na końcu hello tego samouczka możesz uruchomić dwóch aplikacji konsoli .NET:

* **SimulatedDevice**, zmodyfikowanej wersji aplikacji hello utworzone w hello [wysyłać chmury do urządzenia z Centrum IoT](iot-hub-csharp-csharp-c2d.md) samouczka. Ta aplikacja będzie przekazywać toostorage plików, przy użyciu identyfikatora URI połączenia SAS udostępniane przez Centrum IoT.
* **ReadFileUploadNotification**, która odbiera powiadomienia o przekazywania plików z Centrum IoT.

> [!NOTE]
> Centrum IoT obsługuje wiele platform urządzeń i języków (w tym C, Java i Javascript) za pomocą urządzenia Azure IoT zestawów SDK. Zobacz toohello [Azure IoT Developer Center] instrukcje krok po kroku na temat tooconnect tooAzure Twojego urządzenia IoT Hub.

toocomplete tego samouczka należy hello następujące:

* Visual Studio 2015 lub Visual Studio 2017 r.
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>Przekaż plik z aplikacji przez urządzenia

W tej sekcji możesz zmodyfikować aplikację urządzenia hello utworzony w [wysyłać chmury do urządzenia z Centrum IoT](iot-hub-csharp-csharp-c2d.md) tooreceive komunikaty chmury do urządzenia z Centrum IoT hello.

1. W programie Visual Studio, kliknij prawym przyciskiem myszy hello **SimulatedDevice** projektu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **istniejący element**. Przejdź do pliku obrazu tooan i dołączyć go w projekcie. Ten samouczek zakłada nosi nazwę obrazu hello `image.jpg`.

1. Kliknij prawym przyciskiem myszy na powitania obrazu, a następnie kliknij przycisk **właściwości**. Upewnij się, że **skopiuj tooOutput katalogu** ustawiono zbyt**skopiuj zawsze**.

    ![][1]

1. W hello **Program.cs** plików, Dodaj następujące instrukcje u góry pliku hello hello hello:

    ```csharp
    using System.IO;
    ```

1. Dodaj następujące metody toohello hello **Program** klasy:

    ```csharp
    private static async void SendToBlobAsync()
    {
        string fileName = "image.jpg";
        Console.WriteLine("Uploading file: {0}", fileName);
        var watch = System.Diagnostics.Stopwatch.StartNew();

        using (var sourceData = new FileStream(@"image.jpg", FileMode.Open))
        {
            await deviceClient.UploadToBlobAsync(fileName, sourceData);
        }

        watch.Stop();
        Console.WriteLine("Time tooupload file: {0}ms\n", watch.ElapsedMilliseconds);
    }
    ```

    Witaj `UploadToBlobAsync` metoda przyjmuje w nazwie pliku hello i źródła strumienia toobe pliku hello przekazane i obsługuje hello toostorage przekazywania. Aplikacja konsoli Hello Wyświetla hello czas tooupload hello pliku.

1. Dodaj następujące metody w hello hello **Main** metody, bezpośrednio przed hello `Console.ReadLine()` wiersza:

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> Sake na prostotę w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych].

## <a name="receive-a-file-upload-notification"></a>Otrzymasz powiadomienie przekazywania pliku

W tej sekcji służy do pisania aplikacji konsoli .NET, który odbiera komunikaty powiadomień dotyczących przekazywania plików z Centrum IoT.

1. W bieżącym rozwiązaniu programu Visual Studio hello utworzyć projekt Visual C# systemu Windows przy użyciu hello **aplikacji konsoli** szablonu projektu. Nazwa projektu hello **ReadFileUploadNotification**.

    ![Nowy projekt w programie Visual Studio][2]

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ReadFileUploadNotification** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .

1. W hello **Menedżera pakietów NuGet** okna, wyszukiwanie **Microsoft.Azure.Devices**, kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.

    Ta akcja pobiera, instaluje i dodaje toohello odwołanie [pakiet NuGet zestawu SDK usługi Azure IoT] w hello **ReadFileUploadNotification** projektu.

1. W hello **Program.cs** plików, Dodaj następujące instrukcje u góry pliku hello hello hello:

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. Dodaj następujące pola toohello hello **Program** klasy. Zastąp hello symbol zastępczy wartości z ciągu połączenia Centrum IoT powitania od [Rozpoczynanie pracy z Centrum IoT]:

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. Dodaj następujące metody toohello hello **Program** klasy:

    ```csharp
    private async static void ReceiveFileUploadNotificationAsync()
    {
        var notificationReceiver = serviceClient.GetFileNotificationReceiver();

        Console.WriteLine("\nReceiving file upload notification from service");
        while (true)
        {
            var fileUploadNotification = await notificationReceiver.ReceiveAsync();
            if (fileUploadNotification == null) continue;

            Console.ForegroundColor = ConsoleColor.Yellow;
            Console.WriteLine("Received file upload noticiation: {0}", string.Join(", ", fileUploadNotification.BlobName));
            Console.ResetColor();

            await notificationReceiver.CompleteAsync(fileUploadNotification);
        }
    }
    ```

    Uwaga tego wzorca receive jest hello tej samej wiadomości chmury do urządzenia używane tooreceive jednego z hello aplikacji urządzenia.

1. Na koniec należy dodać następujące wiersze toohello hello **Main** metody:

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>Uruchamianie aplikacji hello

Teraz wszystko jest gotowe toorun hello aplikacji.

1. W programie Visual Studio, kliknij prawym przyciskiem myszy rozwiązanie, a następnie wybierz **projektów startowych ustawić**. Wybierz **wiele projektów startowych**, a następnie wybierz pozycję hello **Start** akcji **ReadFileUploadNotification** i **SimulatedDevice**.

1. Naciśnij klawisz **F5**. Należy zacząć obydwu aplikacji. Powinna zostać wyświetlona przekazywania hello zostało ukończone w jednej konsoli aplikacji i powiadomienie przekazywania hello odebranych przez hello innych aplikacji konsoli. Można użyć hello [portalu Azure] lub Eksploratora serwera w usłudze Visual Studio toocheck obecność hello hello przekazany plik na koncie magazynu Azure.

    ![][50]

## <a name="next-steps"></a>Następne kroki

W tym samouczku przedstawiono, jak plik hello toouse przekazać możliwości przekazywania plików toosimplify z urządzeń Centrum IoT. Można kontynuować scenariusze i funkcje Centrum IoT tooexplore hello następujące artykuły:

* [Programowo tworzenia Centrum IoT][lnk-create-hub]
* [Wprowadzenie tooC zestawu SDK][lnk-c-sdk]
* [Zestawy SDK Azure IoT][lnk-sdks]

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Symuluje urządzenia IoT krawędzi][lnk-iotedge]

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png

<!-- Links -->

[portalu Azure]: https://portal.azure.com/

[Azure IoT Developer Center]: http://www.azure.com/develop/iot

[obsługi błędów przejściowych]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[pakiet NuGet zestawu SDK usługi Azure IoT]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md
