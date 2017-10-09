---
title: "aaaProcess wiadomości urządzenia do chmury Azure IoT Hub (Java) | Dokumentacja firmy Microsoft"
description: "Jak tooprocess Centrum IoT wiadomości urządzenia do chmury przy użyciu reguł routingu oraz niestandardowe punkty końcowe toodispatch komunikatów tooother usług zaplecza."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: bd9af5f9-a740-4780-a2a6-8c0e2752cf48
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.openlocfilehash: 084e84e721ca4297c4d7d6cb06a43b0bed9bce85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a>Przetwarzanie wiadomości urządzenia do chmury Centrum IoT (Java)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

Centrum IoT Azure jest w pełni zarządzaną usługę, która zapewnia niezawodne i bezpieczną komunikację dwukierunkową między milionów urządzeń i rozwiązanie zaplecza. Innych samouczków ([Rozpoczynanie pracy z Centrum IoT] i [wysyłać chmury do urządzenia z Centrum IoT][lnk-c2d]) pokazują, jak toouse hello podstawowe urządzenia do chmury i chmury do urządzenia Obsługa wiadomości funkcji Centrum IoT.

W tym samouczku opiera się na powitania kodu pokazano hello [Rozpoczynanie pracy z Centrum IoT] samouczek i pokazuje, jak toouse wiadomości routingu wiadomości urządzenia do chmury tooprocess w sposób skalowalny. Samouczek Hello przedstawiono, jak komunikaty tooprocess, które wymagają natychmiastowego działania z rozwiązania hello wewnętrzna baza danych. Na przykład urządzenie może wysłać komunikat alarmu, które wyzwala Wstawianie biletu do systemu CRM. Z kolei wiadomości punktu danych źródła danych po prostu do aparatu analizy. Na przykład dane telemetryczne temperatury z urządzenia, które jest przechowywane w celu późniejszej analizy toobe jest komunikat punktu danych.

Na końcu hello tego samouczka możesz uruchomić trzech aplikacji Java w konsoli:

* **Symulowane urządzenie**, zmodyfikowanej wersji aplikacji hello utworzone w hello [Rozpoczynanie pracy z Centrum IoT] samouczek, wysyła komunikaty urządzenia do chmury punktu danych co sekundę i interaktywne urządzenia do chmury wiadomości co 10 Liczba sekund. Ta aplikacja używa toocommunicate protokołu AMQP hello z Centrum IoT.
* **Odczyt — d2c — liczba komunikatów** wyświetla dane telemetryczne hello wysyłane przez aplikację na urządzeniu.
* **Odczyt krytyczne kolejki** usuwania kolejki krytycznych wiadomości powitania od toohello dołączony kolejki usługi Service Bus hello Centrum IoT.

> [!NOTE]
> Centrum IoT obsługuje zestawu SDK dla wielu platform urządzeń i języków, w tym C, Java i JavaScript. Aby uzyskać instrukcje dotyczące sposobu tooreplace hello urządzenia w ramach tego samouczka z urządzenia fizycznego i tooconnect tooan urządzenia IoT Hub, zobacz temat hello [Azure IoT Developer Center].

toocomplete tego samouczka należy hello następujące:

* Pełną wersję pracy hello [Rozpoczynanie pracy z Centrum IoT] samouczka.
* Witaj najnowszych [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Aktywne konto platformy Azure. (Jeśli nie masz konta, możesz utworzyć [bezpłatne konto] [lnk bezpłatnych wersji próbnych] w zaledwie kilka minut.)

Powinien mieć niektóre podstawową wiedzę na temat [usługi Azure Storage] i [Azure Service Bus].

## <a name="send-interactive-messages-from-a-device-app"></a>Wysyłanie wiadomości interaktywne z aplikacji przez urządzenia
W tej sekcji możesz zmodyfikować aplikację urządzenia hello utworzony w hello [Rozpoczynanie pracy z Centrum IoT] toooccasionally samouczka Wyślij wiadomości, które wymagają natychmiastowego przetwarzania.

1. Przy użyciu pliku simulated-device\src\main\java\com\mycompany\app\App.java hello tooopen edytora tekstu. Ten plik zawiera kod hello hello **symulowane urządzenie** aplikacji utworzony w hello [Rozpoczynanie pracy z Centrum IoT] samouczka.

2. Zastąp hello **MessageSender** klasy z hello następującego kodu:

    ```java
    private static class MessageSender implements Runnable {

        public void run()  {
            try {
                double minTemperature = 20;
                double minHumidity = 60;
                Random rand = new Random();

                while (true) {
                    String msgStr;
                    Message msg;
                    if (new Random().nextDouble() > 0.7) {
                        msgStr = "This is a critical message.";
                        msg = new Message(msgStr);
                        msg.setProperty("level", "critical");
                    } else {
                        double currentTemperature = minTemperature + rand.nextDouble() * 15;
                        double currentHumidity = minHumidity + rand.nextDouble() * 20; 
                        TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
                        telemetryDataPoint.deviceId = deviceId;
                        telemetryDataPoint.temperature = currentTemperature;
                        telemetryDataPoint.humidity = currentHumidity;

                        msgStr = telemetryDataPoint.serialize();
                        msg = new Message(msgStr);
                    }
                    
                    System.out.println("Sending: " + msgStr);

                    Object lockobj = new Object();
                    EventCallback callback = new EventCallback();
                    client.sendEventAsync(msg, callback, lockobj);

                    synchronized (lockobj) {
                        lockobj.wait();
                    }
                    Thread.sleep(1000);
                }
            } catch (InterruptedException e) {
                System.out.println("Finished.");
            }
        }
    }
    ```
   
    Ta metoda losowo dodaje właściwość hello `"level": "critical"` toomessages wysyłane przez urządzenie hello, która symuluje komunikat, który wymaga natychmiastowego działania przez zaplecza aplikacji hello. Aplikacja Hello przekazuje informacje w oknie dialogowym właściwości wiadomość hello zamiast, w treści wiadomości powitania, dzięki tym Centrum IoT można kierować docelowy prawidłowego komunikatu toohello wiadomość hello.
   
   > [!NOTE]
   > Można użyć komunikatów właściwości tooroute komunikatów dla różnych scenariuszy, w tym przetwarzanie dodatkowo toohello aktywnej ścieżki przykładzie chłodni path.

2. Zapisz i zamknij plik simulated-device\src\main\java\com\mycompany\app\App.java hello.

    > [!NOTE]
    > Dla zapewnienia hello prostotę w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania wykładniczego wycofywania, zgodnie z sugestią podaną w artykuł w witrynie MSDN hello np. [obsługi błędów przejściowych].

3. Witaj toobuild **symulowane urządzenie** aplikacji za pomocą programu Maven, wykonaj następujące polecenie w wierszu polecenia hello w folderze symulowane urządzenie hello hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a>Dodaj kolejki tooyour IoT hub i tras wiadomości tooit

W tej sekcji Tworzenie kolejki usługi Service Bus, podłącz go tooyour Centrum IoT i skonfigurować IoT Centrum toosend wiadomości toohello kolejki na podstawie obecności hello właściwości na wiadomość powitania. Aby uzyskać więcej informacji o sposobie tooprocess komunikaty z kolejek usługi Service Bus, zobacz [Rozpoczynanie pracy z kolejkami][lnk-sb-queues-java].

1. Tworzenie kolejki usługi Service Bus, zgodnie z opisem w [Rozpoczynanie pracy z kolejkami][lnk-sb-queues-java]. Zanotuj nazwę przestrzeni nazw i kolejki hello.

2. Witaj w portalu Azure, Otwórz Centrum IoT i kliknij przycisk **punkty końcowe**.

    ![Punkty końcowe Centrum IoT][30]

3. W hello **punkty końcowe** bloku, kliknij przycisk **Dodaj** na hello top tooadd Centrum IoT tooyour kolejki. Punkt końcowy hello nazwa **CriticalQueue** i użyj hello listach rozwijanych tooselect **kolejki usługi Service Bus**hello przestrzeń nazw magistrali usług, w której znajduje się kolejki i hello nazwę kolejki. Gdy wszystko będzie gotowe, kliknij przycisk **zapisać** u dołu hello.

    ![Dodawanie punktu końcowego][31]

4. Teraz kliknij **tras** w Centrum IoT. Kliknij przycisk **Dodaj** u góry hello toocreate bloku hello reguły routingu kieruje komunikaty toohello kolejki można tylko dodać. Wybierz **DeviceTelemetry** hello źródłem danych. Wprowadź `level="critical"` hello warunkiem i wybierz polecenie kolejki hello właśnie został dodany jako punkt końcowy niestandardowych jako hello punkt końcowy reguły routingu. Gdy wszystko będzie gotowe, kliknij przycisk **zapisać** u dołu hello.

    ![Dodawanie trasy][32]

    Upewnij się, że trasy rezerwowy hello ustawiono zbyt**ON**. To ustawienie jest hello domyślną konfigurację Centrum IoT.

    ![Trasy rezerwowej][33]

## <a name="optional-read-from-hello-queue-endpoint"></a>(Opcjonalnie) Odczyt z hello punkt końcowy z kolejki

Możesz opcjonalnie przeczytać wiadomości powitania z punkt końcowy kolejki hello, wykonując następujące instrukcje hello w [Rozpoczynanie pracy z kolejkami][lnk-sb-queues-java]. Nazwa aplikacji hello **odczytu krytycznych kolejki**.

## <a name="run-hello-applications"></a>Uruchamianie aplikacji hello

Teraz wszystko jest gotowe toorun hello trzech aplikacji.

1. Witaj toorun **odczytu — d2c — liczba komunikatów** aplikacji, w wierszu polecenia lub powłoki przejdź do folderu d2c odczytu toohello i wykonywanie hello następujące polecenie:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Uruchom odczytu — d2c — liczba komunikatów][readd2c]

2. Witaj toorun **odczytu krytycznych kolejki** aplikacji, w wierszu polecenia lub powłoki przejdź do folderu odczytu krytycznych kolejki toohello i wykonywanie hello następujące polecenie:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Uruchom odczytu — krytyczne — liczba komunikatów][readqueue]

3. Witaj toorun **symulowane urządzenie** aplikacji, w wierszu polecenia lub powłoki Przejdź toohello folderu symulowane urządzenie i wykonaj hello następujące polecenie:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Uruchom symulowane urządzenie][simulateddevice]

## <a name="next-steps"></a>Następne kroki

W tym samouczku przedstawiono sposób tooreliably wysyłania wiadomości urządzenia do chmury przy użyciu funkcji routingu wiadomość hello Centrum IoT.

Witaj [jak komunikaty toosend chmury do urządzenia z Centrum IoT] [ lnk-c2d] pokazuje, jak toosend wiadomości tooyour przez urządzenia z zaplecza rozwiązania.

Przykłady toosee kompletnych rozwiązań end-to-end korzystających z Centrum IoT, zobacz [pakiet IoT Azure][lnk-suite].

toolearn więcej informacji na temat tworzenia rozwiązań z Centrum IoT, zobacz hello [Centrum IoT — przewodnik dewelopera].

Zobacz toolearn więcej informacji na temat routing komunikatów w Centrum IoT [wysyłania i odbierania wiadomości z Centrum IoT][lnk-devguide-messaging].

<!-- Images. -->
<!-- TODO: UPDATE PICTURES -->
[simulateddevice]: ./media/iot-hub-java-java-process-d2c/runsimulateddevice.png
[readd2c]: ./media/iot-hub-java-java-process-d2c/runprocessinteractive.png
[readqueue]: ./media/iot-hub-java-java-process-d2c/runprocessd2c.png

[30]: ./media/iot-hub-java-java-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-java-java-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-java-java-process-d2c/route-creation.png
[33]: ./media/iot-hub-java-java-process-d2c/fallback-route.png

<!-- Links -->

[lnk-sb-queues-java]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md

[usługi Azure Storage]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/

[Centrum IoT — przewodnik dewelopera]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Rozpoczynanie pracy z Centrum IoT]: iot-hub-java-java-getstarted.md
[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot
[obsługi błędów przejściowych]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[Obsługa błędu przejściowego]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
