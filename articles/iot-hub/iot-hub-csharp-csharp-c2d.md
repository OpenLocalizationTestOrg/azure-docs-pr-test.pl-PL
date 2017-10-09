---
title: "komunikaty aaaCloud do urządzenia z Centrum IoT Azure (.NET) | Dokumentacja firmy Microsoft"
description: "Jak chmury urządzenia toosend komunikatów tooa urządzenia z Centrum Azure IoT przy użyciu hello Azure IoT SDK dla platformy .NET. Modyfikowanie komunikatów chmury do urządzenia urządzenia aplikacji tooreceive i modyfikowanie aplikacji zaplecza toosend hello chmury do urządzenia komunikatów."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: f6a7618b164d95c8ddaf28943f244aeeb568217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a><span data-ttu-id="4ddab-104">Wysyłanie wiadomości z hello chmury tooyour urządzenia z Centrum IoT (.NET)</span><span class="sxs-lookup"><span data-stu-id="4ddab-104">Send messages from hello cloud tooyour device with IoT Hub (.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="4ddab-105">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="4ddab-105">Introduction</span></span>
<span data-ttu-id="4ddab-106">Centrum IoT Azure jest w pełni zarządzaną usługę, która umożliwia włączanie i niezawodności komunikację dwukierunkową między milionów urządzeń i zaplecze rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="4ddab-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="4ddab-107">Witaj [Rozpoczynanie pracy z Centrum IoT] samouczek pokazuje, jak udostępnić tożsamość urządzenia w nim toocreate Centrum IoT i kodu aplikacji urządzenia, który wysyła komunikaty urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="4ddab-107">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="4ddab-108">W tym samouczku opiera się na [Rozpoczynanie pracy z Centrum IoT].</span><span class="sxs-lookup"><span data-stu-id="4ddab-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="4ddab-109">Jak przedstawiono na:</span><span class="sxs-lookup"><span data-stu-id="4ddab-109">It shows you how to:</span></span>

* <span data-ttu-id="4ddab-110">Z z zaplecza rozwiązania należy wysłać pojedyncze urządzenie tooa wiadomości chmury do urządzenia za pośrednictwem Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="4ddab-110">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="4ddab-111">Komunikaty chmury do urządzenia na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="4ddab-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="4ddab-112">Z sieci zaplecza rozwiązania, żądania potwierdzenia dostarczenia (*opinii*) dla wiadomości wysyłane tooa urządzenie z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="4ddab-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="4ddab-113">Więcej informacji na temat wiadomości chmury do urządzenia można znaleźć w hello [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="4ddab-113">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="4ddab-114">Na końcu hello tego samouczka możesz uruchomić dwóch aplikacji konsoli .NET:</span><span class="sxs-lookup"><span data-stu-id="4ddab-114">At hello end of this tutorial, you run two .NET console apps:</span></span>

* <span data-ttu-id="4ddab-115">**SimulatedDevice**, zmodyfikowanej wersji aplikacji hello utworzone w [Rozpoczynanie pracy z Centrum IoT], która łączy się z Centrum IoT tooyour i odbiera komunikaty chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4ddab-115">**SimulatedDevice**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="4ddab-116">**SendCloudToDevice**, który wysyła aplikacji urządzenia toohello komunikat chmury do urządzenia, za pośrednictwem Centrum IoT i następnie odbiera jego potwierdzenie dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="4ddab-116">**SendCloudToDevice**, which sends a cloud-to-device message toohello device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="4ddab-117">Centrum IoT obsługuje zestawu SDK dla wielu platform urządzeń i języków (w tym C, Java i Javascript) za pośrednictwem [urządzenia Azure IoT SDK].</span><span class="sxs-lookup"><span data-stu-id="4ddab-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through [Azure IoT device SDKs].</span></span> <span data-ttu-id="4ddab-118">Instrukcje krok po kroku dotyczące tooconnect samouczek toothis urządzenia kodu i zazwyczaj tooAzure Centrum IoT, zobacz temat hello [Centrum IoT — przewodnik dewelopera].</span><span class="sxs-lookup"><span data-stu-id="4ddab-118">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [IoT Hub developer guide].</span></span>
> 
> 

<span data-ttu-id="4ddab-119">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="4ddab-119">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="4ddab-120">Visual Studio 2015 lub Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="4ddab-120">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="4ddab-121">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4ddab-121">An active Azure account.</span></span> <span data-ttu-id="4ddab-122">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="4ddab-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-device-app"></a><span data-ttu-id="4ddab-123">Odbieranie komunikatów w aplikacji urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="4ddab-123">Receive messages in hello device app</span></span>
<span data-ttu-id="4ddab-124">W tej sekcji będzie zmodyfikować utworzonego w aplikacji urządzenia hello [Rozpoczynanie pracy z Centrum IoT] tooreceive komunikaty chmury do urządzenia z Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="4ddab-124">In this section, you'll modify hello device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="4ddab-125">W programie Visual Studio w hello **SimulatedDevice** projekt, Dodaj następujące metody toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="4ddab-125">In Visual Studio, in hello **SimulatedDevice** project, add hello following method toohello **Program** class.</span></span>
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud toodevice messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    <span data-ttu-id="4ddab-126">Witaj `ReceiveAsync` — metoda asynchronicznie zwraca wiadomość hello odebrane w czasie hello otrzymał hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4ddab-126">hello `ReceiveAsync` method asynchronously returns hello received message at hello time that it is received by hello device.</span></span> <span data-ttu-id="4ddab-127">Zwraca *null* po upływie limitu czasu specifiable (w tym przypadku używana jest domyślna hello minutę).</span><span class="sxs-lookup"><span data-stu-id="4ddab-127">It returns *null* after a specifiable timeout period (in this case, hello default of one minute is used).</span></span> <span data-ttu-id="4ddab-128">Gdy aplikacja hello odbiera *null*, powinno być kontynuowane toowait nowe wiadomości.</span><span class="sxs-lookup"><span data-stu-id="4ddab-128">When hello app receives a *null*, it should continue toowait for new messages.</span></span> <span data-ttu-id="4ddab-129">To wymaganie dotyczy hello Przyczyna hello `if (receivedMessage == null) continue` wiersza.</span><span class="sxs-lookup"><span data-stu-id="4ddab-129">This requirement is hello reason for hello `if (receivedMessage == null) continue` line.</span></span>
   
    <span data-ttu-id="4ddab-130">Witaj wywołanie za`CompleteAsync()` powiadamia Centrum IoT tę wiadomość hello został pomyślnie przetworzony.</span><span class="sxs-lookup"><span data-stu-id="4ddab-130">hello call too`CompleteAsync()` notifies IoT Hub that hello message has been successfully processed.</span></span> <span data-ttu-id="4ddab-131">wiadomości powitania można bezpiecznie usunąć z kolejki urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="4ddab-131">hello message can be safely removed from hello device queue.</span></span> <span data-ttu-id="4ddab-132">Jeśli coś się stało, aplikacja urządzenia hello uniemożliwił ukończenie przetwarzania hello wiadomość hello, Centrum IoT dostarcza ją ponownie.</span><span class="sxs-lookup"><span data-stu-id="4ddab-132">If something happened that prevented hello device app from completing hello processing of hello message, IoT Hub delivers it again.</span></span> <span data-ttu-id="4ddab-133">Ważne jest, następnie wiadomość przetwarzania logiki w aplikacji urządzenia hello jest *idempotentności*, dzięki czemu odbieranie tworzy wiele razy tę samą wiadomość hello hello takiego samego wyniku.</span><span class="sxs-lookup"><span data-stu-id="4ddab-133">It is then important that message processing logic in hello device app is *idempotent*, so that receiving hello same message multiple times produces hello same result.</span></span> <span data-ttu-id="4ddab-134">Aplikację można również tymczasowo abandon wiadomości, co prowadzi do Centrum IoT, zachowując wiadomość hello w kolejce hello do użytku w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="4ddab-134">An application can also temporarily abandon a message, which results in IoT hub retaining hello message in hello queue for future consumption.</span></span> <span data-ttu-id="4ddab-135">Lub aplikacji hello można odrzucić wiadomości, które trwale usuwa hello wiadomości z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="4ddab-135">Or, hello application can reject a message, which permanently removes hello message from hello queue.</span></span> <span data-ttu-id="4ddab-136">Aby uzyskać więcej informacji na temat cyklu życia chmury do urządzenia wiadomość hello Zobacz hello [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="4ddab-136">For more information about hello cloud-to-device message lifecycle, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4ddab-137">Korzystając z protokołu HTTP zamiast MQTT lub AMQP jako transportu, hello `ReceiveAsync` metoda zwraca natychmiast.</span><span class="sxs-lookup"><span data-stu-id="4ddab-137">When using HTTP instead of MQTT or AMQP as a transport, hello `ReceiveAsync` method returns immediately.</span></span> <span data-ttu-id="4ddab-138">wzorzec Hello obsługiwane komunikatów chmury do urządzenia z protokołu HTTP jest sporadycznie podłączone urządzenia Sprawdź komunikaty rzadko (mniej niż co 25 minut).</span><span class="sxs-lookup"><span data-stu-id="4ddab-138">hello supported pattern for cloud-to-device messages with HTTP is intermittently connected devices that check for messages infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="4ddab-139">Wystawianie więcej HTTP odbiera wyników w Centrum IoT ograniczania przepustowości hello żądania.</span><span class="sxs-lookup"><span data-stu-id="4ddab-139">Issuing more HTTP receives results in IoT Hub throttling hello requests.</span></span> <span data-ttu-id="4ddab-140">Aby uzyskać więcej informacji o różnicach hello MQTT, AMQP i HTTP pomocy technicznej i ograniczania Centrum IoT, zobacz hello [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="4ddab-140">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 
2. <span data-ttu-id="4ddab-141">Dodaj następujące metody w hello hello **Main** metody, bezpośrednio przed hello `Console.ReadLine()` wiersza:</span><span class="sxs-lookup"><span data-stu-id="4ddab-141">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>
   
        ReceiveC2dAsync();

> [!NOTE]
> <span data-ttu-id="4ddab-142">Sake na prostotę w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="4ddab-142">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="4ddab-143">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych].</span><span class="sxs-lookup"><span data-stu-id="4ddab-143">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="4ddab-144">Wyślij wiadomość chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="4ddab-144">Send a cloud-to-device message</span></span>
<span data-ttu-id="4ddab-145">W tej sekcji służy do pisania aplikacji konsoli .NET, który wysyła wiadomości chmury do urządzenia toohello urządzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4ddab-145">In this section, you write a .NET console app that sends cloud-to-device messages toohello device app.</span></span>

1. <span data-ttu-id="4ddab-146">W bieżącym rozwiązaniu programu Visual Studio hello utworzyć projekt Visual C# pulpitu aplikacji przy użyciu hello **aplikacji konsoli** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="4ddab-146">In hello current Visual Studio solution, create a Visual C# Desktop App project by using hello **Console Application** project template.</span></span> <span data-ttu-id="4ddab-147">Nazwa projektu hello **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="4ddab-147">Name hello project **SendCloudToDevice**.</span></span>
   
    ![Nowy projekt w programie Visual Studio][20]
2. <span data-ttu-id="4ddab-149">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy rozwiązanie hello, a następnie kliknij przycisk **Zarządzaj pakietami NuGet rozwiązania...** .</span><span class="sxs-lookup"><span data-stu-id="4ddab-149">In Solution Explorer, right-click hello solution, and then click **Manage NuGet Packages for Solution...**.</span></span> 
   
    <span data-ttu-id="4ddab-150">Ta akcja powoduje otwarcie hello **Zarządzaj pakietami NuGet** okna.</span><span class="sxs-lookup"><span data-stu-id="4ddab-150">This action opens hello **Manage NuGet Packages** window.</span></span>
3. <span data-ttu-id="4ddab-151">Wyszukaj **Microsoft.Azure.Devices**, kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="4ddab-151">Search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span> 
   
    <span data-ttu-id="4ddab-152">To spowoduje pobranie, instaluje i dodaje toohello odwołanie [pakiet NuGet zestawu SDK usługi Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="4ddab-152">This downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package].</span></span>

4. <span data-ttu-id="4ddab-153">Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="4ddab-153">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="4ddab-154">Dodaj następujące pola toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="4ddab-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="4ddab-155">Zastąp hello symbol zastępczy wartości z ciągu połączenia Centrum IoT hello z [Rozpoczynanie pracy z Centrum IoT]:</span><span class="sxs-lookup"><span data-stu-id="4ddab-155">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="4ddab-156">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="4ddab-156">Add hello following method toohello **Program** class:</span></span>
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    <span data-ttu-id="4ddab-157">Ta metoda wysyła nowe urządzenie toohello chmury do urządzenia komunikatu o identyfikatorze hello `myFirstDevice`.</span><span class="sxs-lookup"><span data-stu-id="4ddab-157">This method sends a new cloud-to-device message toohello device with hello ID, `myFirstDevice`.</span></span> <span data-ttu-id="4ddab-158">Ten parametr należy zmienić tylko wtedy, gdy zostanie zmodyfikowana przez hello używany w [Rozpoczynanie pracy z Centrum IoT].</span><span class="sxs-lookup"><span data-stu-id="4ddab-158">Change this parameter only if you modified it from hello one used in [Get started with IoT Hub].</span></span>
7. <span data-ttu-id="4ddab-159">Na koniec należy dodać następujące wiersze toohello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="4ddab-159">Finally, add hello following lines toohello **Main** method:</span></span>
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="4ddab-160">Z poziomu programu Visual Studio kliknij rozwiązanie prawym przyciskiem myszy i wybierz **projektów startowych ustawić...** . Wybierz **wiele projektów startowych**, a następnie wybierz pozycję hello **Start** akcji **ReadDeviceToCloudMessages**, **SimulatedDevice**, i **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="4ddab-160">From within Visual Studio, right-click your solution, and select **Set StartUp projects...**. Select **Multiple startup projects**, then select hello **Start** action for **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **SendCloudToDevice**.</span></span>
9. <span data-ttu-id="4ddab-161">Naciśnij klawisz **F5**.</span><span class="sxs-lookup"><span data-stu-id="4ddab-161">Press **F5**.</span></span> <span data-ttu-id="4ddab-162">Należy uruchomić wszystkie trzy aplikacje.</span><span class="sxs-lookup"><span data-stu-id="4ddab-162">All three applications should start.</span></span> <span data-ttu-id="4ddab-163">Wybierz hello **SendCloudToDevice** systemu windows, a następnie naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="4ddab-163">Select hello **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="4ddab-164">Powinna zostać wyświetlona wiadomość hello odbierane przez hello aplikacji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4ddab-164">You should see hello message being received by hello device app.</span></span>
   
   ![Odbieranie komunikatów aplikacji][21]

## <a name="receive-delivery-feedback"></a><span data-ttu-id="4ddab-166">Otrzymasz dostarczania opinię</span><span class="sxs-lookup"><span data-stu-id="4ddab-166">Receive delivery feedback</span></span>
<span data-ttu-id="4ddab-167">Jest możliwe toorequest dostarczania (lub wygaśnięcia) potwierdzeń z Centrum IoT dla każdego komunikatu chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4ddab-167">It is possible toorequest delivery (or expiration) acknowledgements from IoT Hub for each cloud-to-device message.</span></span> <span data-ttu-id="4ddab-168">Ta opcja umożliwia hello rozwiązania zaplecza tooeasily informuje logiki ponawiania próby lub kompensacji.</span><span class="sxs-lookup"><span data-stu-id="4ddab-168">This option enables hello solution back end tooeasily inform retry or compensation logic.</span></span> <span data-ttu-id="4ddab-169">Aby uzyskać więcej informacji dotyczących opinii chmury do urządzenia, zobacz hello [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="4ddab-169">For more information about cloud-to-device feedback, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="4ddab-170">W tej sekcji możesz zmodyfikować hello **SendCloudToDevice** opinii o toorequest aplikacji i otrzymywać Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="4ddab-170">In this section, you modify hello **SendCloudToDevice** app toorequest feedback, and receive it from IoT Hub.</span></span>

1. <span data-ttu-id="4ddab-171">W programie Visual Studio w hello **SendCloudToDevice** projekt, Dodaj następujące metody toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="4ddab-171">In Visual Studio, in hello **SendCloudToDevice** project, add hello following method toohello **Program** class.</span></span>
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    <span data-ttu-id="4ddab-172">Uwaga tego wzorca receive jest hello tej samej wiadomości chmury do urządzenia używane tooreceive jednego z hello aplikacji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4ddab-172">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>
2. <span data-ttu-id="4ddab-173">Dodaj następujące metody w hello hello **Main** metody bezpośrednio po hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` wiersza:</span><span class="sxs-lookup"><span data-stu-id="4ddab-173">Add hello following method in hello **Main** method, right after hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` line:</span></span>
   
        ReceiveFeedbackAsync();
3. <span data-ttu-id="4ddab-174">toorequest opinię dotyczącą hello dostarczenia komunikatu chmura urządzenie, masz toospecify właściwość w hello **SendCloudToDeviceMessageAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="4ddab-174">toorequest feedback for hello delivery of your cloud-to-device message, you have toospecify a property in hello **SendCloudToDeviceMessageAsync** method.</span></span> <span data-ttu-id="4ddab-175">Dodaj następującego wiersza, bezpośrednio po hello hello `var commandMessage = new Message(...);` wiersza:</span><span class="sxs-lookup"><span data-stu-id="4ddab-175">Add hello following line, right after hello `var commandMessage = new Message(...);` line:</span></span>
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. <span data-ttu-id="4ddab-176">Uruchamianie aplikacji hello naciskając **F5**.</span><span class="sxs-lookup"><span data-stu-id="4ddab-176">Run hello apps by pressing **F5**.</span></span> <span data-ttu-id="4ddab-177">Powinny zostać wyświetlone wszystkie trzy aplikacje start.</span><span class="sxs-lookup"><span data-stu-id="4ddab-177">You should see all three applications start.</span></span> <span data-ttu-id="4ddab-178">Wybierz hello **SendCloudToDevice** systemu windows, a następnie naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="4ddab-178">Select hello **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="4ddab-179">Powinny pojawić się hello wiadomości odbierane przez hello aplikacji urządzenia, a po kilku sekundach, hello wiadomość odbierane przez użytkownika **SendCloudToDevice** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4ddab-179">You should see hello message being received by hello device app, and after a few seconds, hello feedback message being received by your **SendCloudToDevice** application.</span></span>
   
   ![Odbieranie komunikatów aplikacji][22]

> [!NOTE]
> <span data-ttu-id="4ddab-181">Sake na prostotę w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="4ddab-181">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="4ddab-182">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych].</span><span class="sxs-lookup"><span data-stu-id="4ddab-182">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4ddab-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4ddab-183">Next steps</span></span>
<span data-ttu-id="4ddab-184">W tym samouczku można przedstawiono sposób toosend i odbierania wiadomości chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4ddab-184">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="4ddab-185">Przykłady toosee kompletnych rozwiązań end-to-end korzystających z Centrum IoT, zobacz [pakiet IoT Azure].</span><span class="sxs-lookup"><span data-stu-id="4ddab-185">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="4ddab-186">toolearn więcej informacji na temat tworzenia rozwiązań z Centrum IoT, zobacz hello [Centrum IoT — przewodnik dewelopera].</span><span class="sxs-lookup"><span data-stu-id="4ddab-186">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[pakiet NuGet zestawu SDK usługi Azure IoT]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[obsługi błędów przejściowych]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[Centrum IoT — przewodnik dewelopera]: iot-hub-devguide.md
[Rozpoczynanie pracy z Centrum IoT]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[pakiet IoT Azure]: https://docs.microsoft.com/en-us/azure/iot-suite/
[urządzenia Azure IoT SDK]: iot-hub-devguide-sdks.md