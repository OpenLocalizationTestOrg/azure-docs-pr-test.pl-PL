---
title: "komunikaty aaaCloud do urządzenia z Centrum IoT Azure (Java) | Dokumentacja firmy Microsoft"
description: "Jak chmury urządzenia toosend komunikatów tooa urządzenia z Centrum Azure IoT przy użyciu hello Azure IoT SDK dla języka Java. Modyfikowanie komunikatów chmury do urządzenia symulowane urządzenie aplikacji tooreceive i modyfikowanie aplikacji zaplecza toosend hello chmury do urządzenia komunikatów."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7f785ea8-e7c2-40c5-87ef-96525e9b9e1e
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: 8721f18428c849ed9a04aa2e45c65605c3e38101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a>Wysyłanie komunikatów chmury do urządzenia z Centrum IoT (Java)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

Centrum IoT Azure jest w pełni zarządzaną usługę, która umożliwia włączanie i niezawodności komunikację dwukierunkową między milionów urządzeń i zaplecze rozwiązania. Witaj [Rozpoczynanie pracy z Centrum IoT] samouczek pokazuje, jak udostępnić tożsamość urządzenia w nim toocreate Centrum IoT i kodu aplikacji symulowane urządzenie, który wysyła wiadomości urządzenia do chmury.

W tym samouczku opiera się na [Rozpoczynanie pracy z Centrum IoT]. Jak przedstawiono na:

* Z z zaplecza rozwiązania należy wysłać pojedyncze urządzenie tooa wiadomości chmury do urządzenia za pośrednictwem Centrum IoT.
* Komunikaty chmury do urządzenia na urządzeniu.
* Z sieci zaplecza rozwiązania, żądania potwierdzenia dostarczenia (*opinii*) dla wiadomości wysyłane tooa urządzenie z Centrum IoT.

Więcej informacji na temat wiadomości chmury do urządzenia można znaleźć w hello [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].

Na końcu hello tego samouczka możesz uruchomić dwie aplikacje konsoli Java:

* **Symulowane urządzenie**, zmodyfikowanej wersji aplikacji hello utworzone w [Rozpoczynanie pracy z Centrum IoT], która łączy się z Centrum IoT tooyour i odbiera komunikaty chmury do urządzenia.
* **send — c2d — liczba komunikatów**, który wysyła aplikacji symulowane urządzenie toohello komunikat chmury do urządzenia, za pośrednictwem Centrum IoT i następnie odbiera jego potwierdzenia dostarczenia.

> [!NOTE]
> Centrum IoT obsługuje zestawu SDK dla wielu platform urządzeń i języków (w tym C, Java i Javascript) za pośrednictwem zestawy SDK urządzenia Azure IoT. Instrukcje krok po kroku dotyczące tooconnect samouczek toothis urządzenia kodu i zazwyczaj tooAzure Centrum IoT, zobacz temat hello [Azure IoT Developer Center].

toocomplete tego samouczka należy hello następujące:

* Pełną wersję pracy hello [Rozpoczynanie pracy z Centrum IoT](iot-hub-java-java-getstarted.md) lub [wiadomości urządzenia do chmury Centrum IoT procesu](iot-hub-java-java-process-d2c.md) samouczka.
* Witaj najnowszych [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

## <a name="receive-messages-in-hello-simulated-device-app"></a>Odbieranie komunikatów w aplikacji symulowane urządzenie hello

W tej sekcji możesz zmodyfikować aplikację symulowane urządzenie hello utworzony w [Rozpoczynanie pracy z Centrum IoT] tooreceive komunikaty chmury do urządzenia z Centrum IoT hello.

1. Za pomocą edytora tekstu, otwórz plik simulated-device\src\main\java\com\mycompany\app\App.java hello.

2. Dodaj następujące hello **MessageCallback** jak zagnieżdżone klasa wewnątrz hello **aplikacji** klasy. Witaj **wykonania** metoda jest wywoływana, gdy urządzenie hello otrzyma komunikat z Centrum IoT. W tym przykładzie urządzenia hello zawsze powiadamia o Centrum IoT hello o zakończeniu wiadomość hello:

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. Modyfikowanie hello **głównego** toocreate — metoda **AppMessageCallback** hello wystąpienia i wywołanie **setMessageCallback** metoda przed jego otwarciem powitania klienta w następujący sposób:

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > Witaj w przypadku wybrania protokołu HTTP zamiast MQTT lub AMQP jako transportu hello **DeviceClient** wystąpienia sprawdza, czy komunikaty z Centrum IoT rzadko (mniej niż co 25 minut). Aby uzyskać więcej informacji o różnicach hello MQTT, AMQP i HTTP pomocy technicznej i ograniczania Centrum IoT, zobacz hello [Centrum IoT — przewodnik dewelopera][IoT Hub developer guide - C2D].

4. Witaj toobuild **symulowane urządzenie** aplikacji za pomocą programu Maven, wykonaj następujące polecenie w wierszu polecenia hello w folderze symulowane urządzenie hello hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a>Wyślij wiadomość chmury do urządzenia

W tej sekcji utworzysz aplikację konsoli języka Java, która wysyła komunikaty chmury do urządzenia toohello symulowane urządzenie aplikacji. Należy hello identyfikator urządzenia urządzenia hello dodane w hello [Rozpoczynanie pracy z Centrum IoT] samouczka. Centrum, które można znaleźć w hello muszą zostać hello parametry połączenia Centrum IoT [portalu Azure].

1. Utwórz projekt Maven o nazwie **wysyłania — c2d — liczba komunikatów** przy użyciu hello następujące polecenie z wiersza polecenia. Należy zauważyć, że to polecenie jest pojedynczą, długie polecenie:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Wierszu polecenia przejdź toohello nowy folder wysyłania — c2d — liczba komunikatów.

3. Za pomocą edytora tekstu, otwórz plik pom.xml hello w folderze wysyłać c2d-wiadomości powitania i dodaj następujące zależności toohello hello **zależności** węzła. Dodawanie zależności hello umożliwia toouse hello **Centrum iothub-java--klient usługi** pakiet w Twojej toocommunicate aplikacji z usługą Centrum IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > Możesz sprawdzić hello najnowszą wersję **klienta w przypadku usługi iot** przy użyciu [wyszukiwania Maven][lnk-maven-service-search].

4. Zapisz i zamknij plik pom.xml hello.

5. Za pomocą edytora tekstu, otwórz plik send-c2d-messages\src\main\java\com\mycompany\app\App.java hello.

6. Dodaj następujące hello **zaimportować** instrukcje toohello pliku:

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy, zastępując **{yourhubconnectionstring}** i **{yourdeviceid}** hello wartości z dostrzeżone wcześniej:

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. Zastąp hello **głównego** metody z hello następującego kodu. Ten kod łączy z Centrum IoT tooyour, wysyła komunikat tooyour urządzenia i czeka na potwierdzenie tę wiadomość hello odebrane i przetwarzanie urządzenia hello:
   
    ```java
    public static void main(String[] args) throws IOException,
        URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(
        connectionString, protocol);
   
      if (serviceClient != null) {
        serviceClient.open();
        FeedbackReceiver feedbackReceiver = serviceClient
          .getFeedbackReceiver();
        if (feedbackReceiver != null) feedbackReceiver.open();
   
        Message messageToSend = new Message("Cloud toodevice message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent toodevice");
   
        FeedbackBatch feedbackBatch = feedbackReceiver.receive(10000);
        if (feedbackBatch != null) {
          System.out.println("Message feedback received, feedback time: "
            + feedbackBatch.getEnqueuedTimeUtc().toString());
        }
   
        if (feedbackReceiver != null) feedbackReceiver.close();
        serviceClient.close();
      }
    }
    ```

    > [!NOTE]
    > Sake na prostotę w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych].


9. Witaj toobuild **symulowane urządzenie** aplikacji za pomocą programu Maven, wykonaj następujące polecenie w wierszu polecenia hello w folderze symulowane urządzenie hello hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Uruchamianie aplikacji hello

Wszystko jest teraz gotowy toorun hello aplikacji.

1. W wierszu polecenia w folderze symulowane urządzenie hello Uruchom powitania po toobegin polecenie wysyłania danych telemetrycznych tooyour IoT hub i toolisten komunikatów chmury do urządzenia wysyłane z Centrum:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Uruchamianie aplikacji symulowane urządzenie hello][img-simulated-device]

2. W wierszu polecenia w folderze wysyłać c2d-wiadomości powitania uruchom następujące polecenie toosend hello komunikatu chmura urządzenie i oczekiwania na potwierdzenie opinii:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Uruchom wiadomość hello polecenia toosend powitania chmury do urządzenia][img-send-command]

## <a name="next-steps"></a>Następne kroki

W tym samouczku można przedstawiono sposób toosend i odbierania wiadomości chmury do urządzenia. 

Przykłady toosee kompletnych rozwiązań end-to-end korzystających z Centrum IoT, zobacz [pakiet IoT Azure].

toolearn więcej informacji na temat tworzenia rozwiązań z Centrum IoT, zobacz hello [Centrum IoT — przewodnik dewelopera].

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

[Rozpoczynanie pracy z Centrum IoT]: iot-hub-java-java-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[Centrum IoT — przewodnik dewelopera]: iot-hub-devguide.md
[Azure IoT Developer Center]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
[obsługi błędów przejściowych]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[portalu Azure]: https://portal.azure.com
[pakiet IoT Azure]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22