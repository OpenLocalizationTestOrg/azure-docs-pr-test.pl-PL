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
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a><span data-ttu-id="b0480-104">Przekazywanie plików z chmury toohello urządzenie z Centrum IoT przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="b0480-104">Upload files from your device toohello cloud with IoT Hub using .NET</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="b0480-105">W tym samouczku opiera się na powitania kodu w hello [wysyłać chmury do urządzenia z Centrum IoT](iot-hub-csharp-csharp-c2d.md) tooshow samouczka możesz jak toouse hello możliwości przekazywania pliku z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b0480-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial tooshow you how toouse hello file upload capabilities of IoT Hub.</span></span> <span data-ttu-id="b0480-106">Jak przedstawiono na:</span><span class="sxs-lookup"><span data-stu-id="b0480-106">It shows you how to:</span></span>

- <span data-ttu-id="b0480-107">Bezpieczne udostępnianie urządzenia platformy Azure blob identyfikatora URI pobierania pliku.</span><span class="sxs-lookup"><span data-stu-id="b0480-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="b0480-108">Użyj hello pliku hello Centrum IoT pliku przekazywania powiadomień tootrigger przetwarzania w sieci wewnętrznej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b0480-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="b0480-109">Witaj [Rozpoczynanie pracy z Centrum IoT](iot-hub-csharp-csharp-getstarted.md) i [wysyłać chmury do urządzenia z Centrum IoT](iot-hub-csharp-csharp-c2d.md) samouczki przedstawiają hello podstawowych urządzenia do chmury i chmury do urządzenia obsługi funkcji Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b0480-109">hello [Get started with IoT Hub](iot-hub-csharp-csharp-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="b0480-110">Witaj [wiadomości procesu urządzenia do chmury](iot-hub-csharp-csharp-process-d2c.md) samouczek przedstawia sposób tooreliably magazynu urządzenia do chmury wiadomości w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b0480-110">hello [Process Device-to-Cloud messages](iot-hub-csharp-csharp-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="b0480-111">Jednak w niektórych scenariuszach nie można łatwo mapować hello dane, które urządzenia wysłać w wiadomości powitania od stosunkowo mały urządzenia do chmury, które akceptuje Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b0480-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="b0480-112">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="b0480-112">For example:</span></span>

* <span data-ttu-id="b0480-113">Duże pliki, które zawierają obrazów</span><span class="sxs-lookup"><span data-stu-id="b0480-113">Large files that contain images</span></span>
* <span data-ttu-id="b0480-114">Filmy wideo</span><span class="sxs-lookup"><span data-stu-id="b0480-114">Videos</span></span>
* <span data-ttu-id="b0480-115">Dane wibrację próbkowanych zgodnie o dużej częstotliwości</span><span class="sxs-lookup"><span data-stu-id="b0480-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="b0480-116">Niektóre formularz wstępnie przetworzonych danych</span><span class="sxs-lookup"><span data-stu-id="b0480-116">Some form of preprocessed data</span></span>

<span data-ttu-id="b0480-117">Pliki te są zwykle partii przetwarzania w chmurze hello za pomocą narzędzi takich jak [fabryki danych Azure](../data-factory/index.md) lub hello [Hadoop](../hdinsight/index.md) stosu.</span><span class="sxs-lookup"><span data-stu-id="b0480-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="b0480-118">Jeśli potrzebujesz tooupload pliki z urządzenia, można nadal używać hello bezpieczeństwa i niezawodności Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b0480-118">When you need tooupload files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="b0480-119">Na końcu hello tego samouczka możesz uruchomić dwóch aplikacji konsoli .NET:</span><span class="sxs-lookup"><span data-stu-id="b0480-119">At hello end of this tutorial you run two .NET console apps:</span></span>

* <span data-ttu-id="b0480-120">**SimulatedDevice**, zmodyfikowanej wersji aplikacji hello utworzone w hello [wysyłać chmury do urządzenia z Centrum IoT](iot-hub-csharp-csharp-c2d.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="b0480-120">**SimulatedDevice**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial.</span></span> <span data-ttu-id="b0480-121">Ta aplikacja będzie przekazywać toostorage plików, przy użyciu identyfikatora URI połączenia SAS udostępniane przez Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b0480-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="b0480-122">**ReadFileUploadNotification**, która odbiera powiadomienia o przekazywania plików z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b0480-122">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="b0480-123">Centrum IoT obsługuje wiele platform urządzeń i języków (w tym C, Java i Javascript) za pomocą urządzenia Azure IoT zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="b0480-123">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="b0480-124">Zobacz toohello [Azure IoT Developer Center] instrukcje krok po kroku na temat tooconnect tooAzure Twojego urządzenia IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b0480-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="b0480-125">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="b0480-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="b0480-126">Visual Studio 2015 lub Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="b0480-126">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="b0480-127">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b0480-127">An active Azure account.</span></span> <span data-ttu-id="b0480-128">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="b0480-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="b0480-129">Przekaż plik z aplikacji przez urządzenia</span><span class="sxs-lookup"><span data-stu-id="b0480-129">Upload a file from a device app</span></span>

<span data-ttu-id="b0480-130">W tej sekcji możesz zmodyfikować aplikację urządzenia hello utworzony w [wysyłać chmury do urządzenia z Centrum IoT](iot-hub-csharp-csharp-c2d.md) tooreceive komunikaty chmury do urządzenia z Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="b0480-130">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="b0480-131">W programie Visual Studio, kliknij prawym przyciskiem myszy hello **SimulatedDevice** projektu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **istniejący element**.</span><span class="sxs-lookup"><span data-stu-id="b0480-131">In Visual Studio, right-click hello **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span></span> <span data-ttu-id="b0480-132">Przejdź do pliku obrazu tooan i dołączyć go w projekcie.</span><span class="sxs-lookup"><span data-stu-id="b0480-132">Navigate tooan image file and include it in your project.</span></span> <span data-ttu-id="b0480-133">Ten samouczek zakłada nosi nazwę obrazu hello `image.jpg`.</span><span class="sxs-lookup"><span data-stu-id="b0480-133">This tutorial assumes hello image is named `image.jpg`.</span></span>

1. <span data-ttu-id="b0480-134">Kliknij prawym przyciskiem myszy na powitania obrazu, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="b0480-134">Right-click on hello image, and then click **Properties**.</span></span> <span data-ttu-id="b0480-135">Upewnij się, że **skopiuj tooOutput katalogu** ustawiono zbyt**skopiuj zawsze**.</span><span class="sxs-lookup"><span data-stu-id="b0480-135">Make sure that **Copy tooOutput Directory** is set too**Copy always**.</span></span>

    ![][1]

1. <span data-ttu-id="b0480-136">W hello **Program.cs** plików, Dodaj następujące instrukcje u góry pliku hello hello hello:</span><span class="sxs-lookup"><span data-stu-id="b0480-136">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using System.IO;
    ```

1. <span data-ttu-id="b0480-137">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="b0480-137">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="b0480-138">Witaj `UploadToBlobAsync` metoda przyjmuje w nazwie pliku hello i źródła strumienia toobe pliku hello przekazane i obsługuje hello toostorage przekazywania.</span><span class="sxs-lookup"><span data-stu-id="b0480-138">hello `UploadToBlobAsync` method takes in hello file name and stream source of hello file toobe uploaded and handles hello upload toostorage.</span></span> <span data-ttu-id="b0480-139">Aplikacja konsoli Hello Wyświetla hello czas tooupload hello pliku.</span><span class="sxs-lookup"><span data-stu-id="b0480-139">hello console app displays hello time it takes tooupload hello file.</span></span>

1. <span data-ttu-id="b0480-140">Dodaj następujące metody w hello hello **Main** metody, bezpośrednio przed hello `Console.ReadLine()` wiersza:</span><span class="sxs-lookup"><span data-stu-id="b0480-140">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> <span data-ttu-id="b0480-141">Sake na prostotę w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="b0480-141">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b0480-142">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych].</span><span class="sxs-lookup"><span data-stu-id="b0480-142">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="b0480-143">Otrzymasz powiadomienie przekazywania pliku</span><span class="sxs-lookup"><span data-stu-id="b0480-143">Receive a file upload notification</span></span>

<span data-ttu-id="b0480-144">W tej sekcji służy do pisania aplikacji konsoli .NET, który odbiera komunikaty powiadomień dotyczących przekazywania plików z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b0480-144">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span></span>

1. <span data-ttu-id="b0480-145">W bieżącym rozwiązaniu programu Visual Studio hello utworzyć projekt Visual C# systemu Windows przy użyciu hello **aplikacji konsoli** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="b0480-145">In hello current Visual Studio solution, create a Visual C# Windows project by using hello **Console Application** project template.</span></span> <span data-ttu-id="b0480-146">Nazwa projektu hello **ReadFileUploadNotification**.</span><span class="sxs-lookup"><span data-stu-id="b0480-146">Name hello project **ReadFileUploadNotification**.</span></span>

    ![Nowy projekt w programie Visual Studio][2]

1. <span data-ttu-id="b0480-148">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ReadFileUploadNotification** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="b0480-148">In Solution Explorer, right-click hello **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span></span>

1. <span data-ttu-id="b0480-149">W hello **Menedżera pakietów NuGet** okna, wyszukiwanie **Microsoft.Azure.Devices**, kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="b0480-149">In hello **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span>

    <span data-ttu-id="b0480-150">Ta akcja pobiera, instaluje i dodaje toohello odwołanie [pakiet NuGet zestawu SDK usługi Azure IoT] w hello **ReadFileUploadNotification** projektu.</span><span class="sxs-lookup"><span data-stu-id="b0480-150">This action downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package] in hello **ReadFileUploadNotification** project.</span></span>

1. <span data-ttu-id="b0480-151">W hello **Program.cs** plików, Dodaj następujące instrukcje u góry pliku hello hello hello:</span><span class="sxs-lookup"><span data-stu-id="b0480-151">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. <span data-ttu-id="b0480-152">Dodaj następujące pola toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="b0480-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="b0480-153">Zastąp hello symbol zastępczy wartości z ciągu połączenia Centrum IoT powitania od [Rozpoczynanie pracy z Centrum IoT]:</span><span class="sxs-lookup"><span data-stu-id="b0480-153">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. <span data-ttu-id="b0480-154">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="b0480-154">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="b0480-155">Uwaga tego wzorca receive jest hello tej samej wiadomości chmury do urządzenia używane tooreceive jednego z hello aplikacji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b0480-155">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>

1. <span data-ttu-id="b0480-156">Na koniec należy dodać następujące wiersze toohello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="b0480-156">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="b0480-157">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="b0480-157">Run hello applications</span></span>

<span data-ttu-id="b0480-158">Teraz wszystko jest gotowe toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b0480-158">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="b0480-159">W programie Visual Studio, kliknij prawym przyciskiem myszy rozwiązanie, a następnie wybierz **projektów startowych ustawić**.</span><span class="sxs-lookup"><span data-stu-id="b0480-159">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span></span> <span data-ttu-id="b0480-160">Wybierz **wiele projektów startowych**, a następnie wybierz pozycję hello **Start** akcji **ReadFileUploadNotification** i **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="b0480-160">Select **Multiple startup projects**, then select hello **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span></span>

1. <span data-ttu-id="b0480-161">Naciśnij klawisz **F5**.</span><span class="sxs-lookup"><span data-stu-id="b0480-161">Press **F5**.</span></span> <span data-ttu-id="b0480-162">Należy zacząć obydwu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b0480-162">Both applications should start.</span></span> <span data-ttu-id="b0480-163">Powinna zostać wyświetlona przekazywania hello zostało ukończone w jednej konsoli aplikacji i powiadomienie przekazywania hello odebranych przez hello innych aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="b0480-163">You should see hello upload completed in one console app and hello upload notification message received by hello other console app.</span></span> <span data-ttu-id="b0480-164">Można użyć hello [portalu Azure] lub Eksploratora serwera w usłudze Visual Studio toocheck obecność hello hello przekazany plik na koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="b0480-164">You can use hello [Azure portal] or Visual Studio Server Explorer toocheck for hello presence of hello uploaded file in your Azure Storage account.</span></span>

    ![][50]

## <a name="next-steps"></a><span data-ttu-id="b0480-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b0480-165">Next steps</span></span>

<span data-ttu-id="b0480-166">W tym samouczku przedstawiono, jak plik hello toouse przekazać możliwości przekazywania plików toosimplify z urządzeń Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b0480-166">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="b0480-167">Można kontynuować scenariusze i funkcje Centrum IoT tooexplore hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="b0480-167">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="b0480-168">[Programowo tworzenia Centrum IoT][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="b0480-168">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="b0480-169">[Wprowadzenie tooC zestawu SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="b0480-169">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="b0480-170">[Zestawy SDK Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="b0480-170">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="b0480-171">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="b0480-171">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b0480-172">[Symuluje urządzenia IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="b0480-172">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

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
