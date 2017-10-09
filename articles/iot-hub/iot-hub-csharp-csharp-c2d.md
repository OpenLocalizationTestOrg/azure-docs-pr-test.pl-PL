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
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a>Wysyłanie wiadomości z hello chmury tooyour urządzenia z Centrum IoT (.NET)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>Wprowadzenie
Centrum IoT Azure jest w pełni zarządzaną usługę, która umożliwia włączanie i niezawodności komunikację dwukierunkową między milionów urządzeń i zaplecze rozwiązania. Witaj [Rozpoczynanie pracy z Centrum IoT] samouczek pokazuje, jak udostępnić tożsamość urządzenia w nim toocreate Centrum IoT i kodu aplikacji urządzenia, który wysyła komunikaty urządzenia do chmury.

W tym samouczku opiera się na [Rozpoczynanie pracy z Centrum IoT]. Jak przedstawiono na:

* Z z zaplecza rozwiązania należy wysłać pojedyncze urządzenie tooa wiadomości chmury do urządzenia za pośrednictwem Centrum IoT.
* Komunikaty chmury do urządzenia na urządzeniu.
* Z sieci zaplecza rozwiązania, żądania potwierdzenia dostarczenia (*opinii*) dla wiadomości wysyłane tooa urządzenie z Centrum IoT.

Więcej informacji na temat wiadomości chmury do urządzenia można znaleźć w hello [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].

Na końcu hello tego samouczka możesz uruchomić dwóch aplikacji konsoli .NET:

* **SimulatedDevice**, zmodyfikowanej wersji aplikacji hello utworzone w [Rozpoczynanie pracy z Centrum IoT], która łączy się z Centrum IoT tooyour i odbiera komunikaty chmury do urządzenia.
* **SendCloudToDevice**, który wysyła aplikacji urządzenia toohello komunikat chmury do urządzenia, za pośrednictwem Centrum IoT i następnie odbiera jego potwierdzenie dostarczenia.

> [!NOTE]
> Centrum IoT obsługuje zestawu SDK dla wielu platform urządzeń i języków (w tym C, Java i Javascript) za pośrednictwem [urządzenia Azure IoT SDK]. Instrukcje krok po kroku dotyczące tooconnect samouczek toothis urządzenia kodu i zazwyczaj tooAzure Centrum IoT, zobacz temat hello [Centrum IoT — przewodnik dewelopera].
> 
> 

toocomplete tego samouczka należy hello następujące:

* Visual Studio 2015 lub Visual Studio 2017 r.
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

## <a name="receive-messages-in-hello-device-app"></a>Odbieranie komunikatów w aplikacji urządzenia hello
W tej sekcji będzie zmodyfikować utworzonego w aplikacji urządzenia hello [Rozpoczynanie pracy z Centrum IoT] tooreceive komunikaty chmury do urządzenia z Centrum IoT hello.

1. W programie Visual Studio w hello **SimulatedDevice** projekt, Dodaj następujące metody toohello hello **Program** klasy.
   
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
   
    Witaj `ReceiveAsync` — metoda asynchronicznie zwraca wiadomość hello odebrane w czasie hello otrzymał hello urządzenia. Zwraca *null* po upływie limitu czasu specifiable (w tym przypadku używana jest domyślna hello minutę). Gdy aplikacja hello odbiera *null*, powinno być kontynuowane toowait nowe wiadomości. To wymaganie dotyczy hello Przyczyna hello `if (receivedMessage == null) continue` wiersza.
   
    Witaj wywołanie za`CompleteAsync()` powiadamia Centrum IoT tę wiadomość hello został pomyślnie przetworzony. wiadomości powitania można bezpiecznie usunąć z kolejki urządzenia hello. Jeśli coś się stało, aplikacja urządzenia hello uniemożliwił ukończenie przetwarzania hello wiadomość hello, Centrum IoT dostarcza ją ponownie. Ważne jest, następnie wiadomość przetwarzania logiki w aplikacji urządzenia hello jest *idempotentności*, dzięki czemu odbieranie tworzy wiele razy tę samą wiadomość hello hello takiego samego wyniku. Aplikację można również tymczasowo abandon wiadomości, co prowadzi do Centrum IoT, zachowując wiadomość hello w kolejce hello do użytku w przyszłości. Lub aplikacji hello można odrzucić wiadomości, które trwale usuwa hello wiadomości z kolejki hello. Aby uzyskać więcej informacji na temat cyklu życia chmury do urządzenia wiadomość hello Zobacz hello [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].
   
   > [!NOTE]
   > Korzystając z protokołu HTTP zamiast MQTT lub AMQP jako transportu, hello `ReceiveAsync` metoda zwraca natychmiast. wzorzec Hello obsługiwane komunikatów chmury do urządzenia z protokołu HTTP jest sporadycznie podłączone urządzenia Sprawdź komunikaty rzadko (mniej niż co 25 minut). Wystawianie więcej HTTP odbiera wyników w Centrum IoT ograniczania przepustowości hello żądania. Aby uzyskać więcej informacji o różnicach hello MQTT, AMQP i HTTP pomocy technicznej i ograniczania Centrum IoT, zobacz hello [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].
   > 
   > 
2. Dodaj następujące metody w hello hello **Main** metody, bezpośrednio przed hello `Console.ReadLine()` wiersza:
   
        ReceiveC2dAsync();

> [!NOTE]
> Sake na prostotę w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych].
> 
> 

## <a name="send-a-cloud-to-device-message"></a>Wyślij wiadomość chmury do urządzenia
W tej sekcji służy do pisania aplikacji konsoli .NET, który wysyła wiadomości chmury do urządzenia toohello urządzenia aplikacji.

1. W bieżącym rozwiązaniu programu Visual Studio hello utworzyć projekt Visual C# pulpitu aplikacji przy użyciu hello **aplikacji konsoli** szablonu projektu. Nazwa projektu hello **SendCloudToDevice**.
   
    ![Nowy projekt w programie Visual Studio][20]
2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy rozwiązanie hello, a następnie kliknij przycisk **Zarządzaj pakietami NuGet rozwiązania...** . 
   
    Ta akcja powoduje otwarcie hello **Zarządzaj pakietami NuGet** okna.
3. Wyszukaj **Microsoft.Azure.Devices**, kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello. 
   
    To spowoduje pobranie, instaluje i dodaje toohello odwołanie [pakiet NuGet zestawu SDK usługi Azure IoT].

4. Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:
   
        using Microsoft.Azure.Devices;
5. Dodaj następujące pola toohello hello **Program** klasy. Zastąp hello symbol zastępczy wartości z ciągu połączenia Centrum IoT hello z [Rozpoczynanie pracy z Centrum IoT]:
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Dodaj następujące metody toohello hello **Program** klasy:
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    Ta metoda wysyła nowe urządzenie toohello chmury do urządzenia komunikatu o identyfikatorze hello `myFirstDevice`. Ten parametr należy zmienić tylko wtedy, gdy zostanie zmodyfikowana przez hello używany w [Rozpoczynanie pracy z Centrum IoT].
7. Na koniec należy dodać następujące wiersze toohello hello **Main** metody:
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. Z poziomu programu Visual Studio kliknij rozwiązanie prawym przyciskiem myszy i wybierz **projektów startowych ustawić...** . Wybierz **wiele projektów startowych**, a następnie wybierz pozycję hello **Start** akcji **ReadDeviceToCloudMessages**, **SimulatedDevice**, i **SendCloudToDevice**.
9. Naciśnij klawisz **F5**. Należy uruchomić wszystkie trzy aplikacje. Wybierz hello **SendCloudToDevice** systemu windows, a następnie naciśnij klawisz **Enter**. Powinna zostać wyświetlona wiadomość hello odbierane przez hello aplikacji urządzenia.
   
   ![Odbieranie komunikatów aplikacji][21]

## <a name="receive-delivery-feedback"></a>Otrzymasz dostarczania opinię
Jest możliwe toorequest dostarczania (lub wygaśnięcia) potwierdzeń z Centrum IoT dla każdego komunikatu chmury do urządzenia. Ta opcja umożliwia hello rozwiązania zaplecza tooeasily informuje logiki ponawiania próby lub kompensacji. Aby uzyskać więcej informacji dotyczących opinii chmury do urządzenia, zobacz hello [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].

W tej sekcji możesz zmodyfikować hello **SendCloudToDevice** opinii o toorequest aplikacji i otrzymywać Centrum IoT.

1. W programie Visual Studio w hello **SendCloudToDevice** projekt, Dodaj następujące metody toohello hello **Program** klasy.
   
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
   
    Uwaga tego wzorca receive jest hello tej samej wiadomości chmury do urządzenia używane tooreceive jednego z hello aplikacji urządzenia.
2. Dodaj następujące metody w hello hello **Main** metody bezpośrednio po hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` wiersza:
   
        ReceiveFeedbackAsync();
3. toorequest opinię dotyczącą hello dostarczenia komunikatu chmura urządzenie, masz toospecify właściwość w hello **SendCloudToDeviceMessageAsync** metody. Dodaj następującego wiersza, bezpośrednio po hello hello `var commandMessage = new Message(...);` wiersza:
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. Uruchamianie aplikacji hello naciskając **F5**. Powinny zostać wyświetlone wszystkie trzy aplikacje start. Wybierz hello **SendCloudToDevice** systemu windows, a następnie naciśnij klawisz **Enter**. Powinny pojawić się hello wiadomości odbierane przez hello aplikacji urządzenia, a po kilku sekundach, hello wiadomość odbierane przez użytkownika **SendCloudToDevice** aplikacji.
   
   ![Odbieranie komunikatów aplikacji][22]

> [!NOTE]
> Sake na prostotę w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych].
> 
> 

## <a name="next-steps"></a>Następne kroki
W tym samouczku można przedstawiono sposób toosend i odbierania wiadomości chmury do urządzenia. 

Przykłady toosee kompletnych rozwiązań end-to-end korzystających z Centrum IoT, zobacz [pakiet IoT Azure].

toolearn więcej informacji na temat tworzenia rozwiązań z Centrum IoT, zobacz hello [Centrum IoT — przewodnik dewelopera].

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