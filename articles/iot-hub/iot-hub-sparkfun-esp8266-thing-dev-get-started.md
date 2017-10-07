---
title: "toocloud aaaESP8266 — Połącz deweloperów operacją ESP8266 Sparkfun tooAzure Centrum IoT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup i połącz deweloperów operacją ESP8266 Sparkfun tooAzure Centrum IoT dla niego toosend danych toohello chmury Azure platforma w tym samouczku."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a>Połącz tooAzure Sparkfun ESP8266 operacją deweloperów Centrum IoT w chmurze hello

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![połączenie między DHT22, co deweloperów i Centrum IoT](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a>Będzie wykonywać

Połącz Centrum IoT tooan Sparkfun ESP8266 operacją deweloperów, zostanie utworzony. Następnie uruchom przykładową aplikację na ESP8266 toocollect temperatury i wilgotności danych z czujnika DHT22. Na koniec Wyślij Centrum IoT tooyour danych czujnika hello.

> [!NOTE]
> Jeśli używasz innych tablice ESP8266 nadal należy wykonać te kroki tooconnect on tooyour Centrum IoT. W zależności od tablicy hello ESP8266 używasz, może być konieczne tooreconfigure hello `LED_PIN`. Na przykład, jeśli używasz ESP8266 z AI Thinker, możesz zmienić go z `0` zbyt`2`. Zestaw nie ma jeszcze?: kliknij [tutaj](http://azure.com/iotstarterkits)

## <a name="what-you-will-learn"></a>Co dowiesz się

* Jak toocreate Centrum IoT i zarejestruj urządzenie na rzecz odchyleń
* Jak tooconnect deweloperów operacją z czujnika hello i komputera.
* Jak toocollect dane czujników, uruchamiając na rzecz odchyleń przykładowej aplikacji
* Jak toosend hello Centrum IoT tooyour danych czujnika.

## <a name="what-you-will-need"></a>Dane będą potrzebne

![Części potrzebne w samouczku hello](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete tej operacji, należy po części z Twojej deweloperów element startowy hello:

* Witaj deweloperów operacją ESP8266 Sparkfun tablicy.
* TooType Micro USB kabla A USB.

Należy również następujące powitania dla swojego środowiska programowania:

* Aktywna subskrypcja platformy Azure. Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.
* Mac lub komputera z systemem Windows lub Ubuntu.
* Sieci bezprzewodowej dla deweloperów operacją ESP8266 Sparkfun tooconnect do.
* Internet połączenia toodownload hello narzędzia do konfiguracji.
* [Arduino IDE](https://www.arduino.cc/en/main/software) wersji 1.6.8 (lub nowsza), wcześniejszych wersjach nie będzie działać z biblioteką AzureIoT hello.

Witaj następujące elementy są opcjonalne w przypadku, gdy nie masz czujnika. Istnieje również opcja hello przy użyciu danych czujnika symulowane.

* Adafruit DHT22 temperatury i wilgotności czujnika.
* Breadboard.
* M/M zworek przewodów.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a>Uzyskuj dostęp do deweloperów operacją ESP8266 hello czujników i komputera

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a>Czujnik temperatury i wilgotności DHT22 połączyć tooESP8266 operacją deweloperów

Użyj hello breadboard i zworek przewodów toomake hello połączenia w następujący sposób. Jeśli nie masz czujnika, Pomiń tę sekcję, ponieważ można użyć danych czujnika symulowane.

![Odwołanie do połączenia](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

Dla czujnik numery PIN użyjemy hello następujących połączeń:

| Start (czujnik)           | Końcowy (tablica)           | Kolor kabel   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 27F)            | 3V (8A kodu Pin)           | Czerwony kabel     |
| DANE (Pin 28F)           | Interfejs GPIO 2 (9A kodu Pin)       | Białe kabel    |
| GND (Pin 30F)            | GND (7J kodu Pin)          | Czarne kabel   |


- Aby uzyskać więcej informacji, zobacz: [Instalatora czujnik DHT22](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) i [specyfikacji Sparkfun ESP8266 operacją deweloperów](https://www.sparkfun.com/products/13711)

Teraz deweloperów operacją ESP8266 Twojego Sparkfun powinny być połączone z czujnika pracy.

![Uzyskuj dht22 ESP8266 operacją deweloperów](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a>Podłącz komputer tooyour Sparkfun ESP8266 operacją deweloperów

Użyj hello Micro USB tooType A USB kabel tooconnect deweloperów operacją ESP8266 Sparkfun tooyour komputera w następujący sposób.

![Podłącz komputer tooyour huzzah piór](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a>Dodaj uprawnienia portu szeregowego — tylko Ubuntu

Jeśli używasz Ubuntu, upewnij się, że zwykłego użytkownika ma toooperate uprawnienia hello na powitania USB portu z Sparkfun ESP8266 operacją odchyleń tooadd portu szeregowego uprawnienia do zwykłego użytkownika, wykonaj następujące kroki:

1. Uruchom następujące polecenia w terminalu hello:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Pojawia się jeden z następujących danych wyjściowych hello:

   * crw-rw---xxxxxxxx uucp głównego 1
   * crw-rw---xxxxxxxx inicjowania połączeń głównego 1

   W danych wyjściowych hello zauważyć `uucp` lub `dialout` czyli hello grupy Nazwa właściciela hello portu USB.

1. Dodaj grupę toohello użytkowników hello, uruchamiając następujące polecenie hello:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`jest nazwa właściciela grupy hello uzyskanego w poprzednim kroku hello. `<username>`to nazwa użytkownika Ubuntu.

1. Wyloguj się Ubuntu i jego ponowne zalogowanie hello zmiany tootake efektu.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Zbierać dane czujników oraz wysyłać je tooyour Centrum IoT

W tej sekcji Wdrażanie i uruchom przykładową aplikację na Sparkfun ESP8266 operacją odchyleń Hello przykładowej aplikacji miganie hello LED na Sparkfun ESP8266 operacją deweloperów i wysyła hello temperatury i wilgotności dane zbierane z hello DHT22 czujnik tooyour Centrum IoT.

### <a name="get-hello-sample-application-from-github"></a>Pobierz hello przykładowej aplikacji z usługi GitHub

Witaj przykładowej aplikacji znajduje się w witrynie GitHub. Klonuj repozytorium przykładowej hello, zawierający hello przykładowej aplikacji z usługi GitHub. repozytorium przykładowej hello tooclone, wykonaj następujące kroki:

1. Otwórz wiersz polecenia lub okno terminalu.
1. Przejdź tooa folder docelowy toobe aplikacji przykładowej hello przechowywane.
1. Uruchom następujące polecenie hello:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

Instalacja pakietu powitania dla deweloperów operacją ESP8266 Sparkfun w Arduino IDE:

1. Otwórz folder hello przechowywania hello przykładowej aplikacji.
1. Otwórz plik app.ino hello w folderze aplikacji hello Arduino IDE.

   ![Otwórz aplikację przykładową hello w arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. W hello Arduino IDE, kliknij przycisk **pliku** > **preferencje**.
1. W hello **preferencje** okna dialogowego, kliknij przycisk Dalej toohello ikona hello **dodatkowych adresów URL Menedżera tablice** pola tekstowego.
1. W oknie podręcznym hello, wprowadź hello następującego adresu URL, a następnie kliknij przycisk **OK**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![adres url pakietu tooa punktu arduino IDE](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. W hello **preferencji** okno dialogowe, kliknij przycisk **OK**.
1. Kliknij przycisk **narzędzia** > **tablicy** > **Menedżera tablice**, a następnie wyszukaj esp8266.
   Należy zainstalować ESP8266 przy użyciu wersji 2.2.0 lub nowszej.

   ![Pakiet esp8266 Hello jest zainstalowany](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. Kliknij przycisk **narzędzia** > **tablicy** > **Sparkfun ESP8266 operacją deweloperów**.

### <a name="install-necessary-libraries"></a>Zainstaluj wymagane biblioteki

1. W hello Arduino IDE, kliknij przycisk **szkicu** > **obejmują biblioteki** > **zarządzanie bibliotekami**.
1. Wyszukiwanie hello następujące nazwy bibliotek jeden po drugim. Dla każdej biblioteki hello możesz znaleźć, kliknij przycisk **zainstalować**.
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>Nie masz rzeczywistych czujnik DHT22?

Hello przykładowej aplikacji można symulować danych temperatury i wilgotności, w przypadku, gdy nie ma rzeczywistego czujnik DHT22. dane toouse symulowane tooenable hello przykładowej aplikacji, wykonaj następujące kroki:

1. Otwórz hello `config.h` pliku w hello `app` folderu.
1. Znajdź powitania po wierszu kodu i zmień wartość hello z `false` zbyt`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![Konfigurowanie hello przykładowych aplikacji toouse symulowane danych](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. Zapisz z `Control-s`.

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a>Wdrażanie hello przykładowej aplikacji tooSparkfun ESP8266 operacją deweloperów

1. W hello Arduino IDE, kliknij przycisk **narzędzie** > **portu**, a następnie kliknij przycisk portu szeregowego hello na Sparkfun ESP8266 operacją odchyleń
1. Kliknij przycisk **szkicu** > **przekazać** toobuild i wdrażanie hello przykładowej aplikacji tooSparkfun odchyleń operacją ESP8266

> [!Note]
> Jeśli używasz macOS można prawdopodobnie Zobacz hello następujące komunikaty podczas przekazywania. `warning: espcomm_sync failed`,`error: espcomm_open failed`. Otwórz okno programu ternimal i Zakończ poniżej akcje toosolve ten problem.
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a>Wprowadź swoje poświadczenia

Po pomyślnym ukończeniu przekazywania hello wykonaj tooenter kroki hello poświadczeń:

1. W hello Arduino IDE, kliknij przycisk **narzędzia** > **Serial Monitor**.
1. W oknie Monitora serial hello Zwróć uwagę Witaj dwie listy rozwijane na powitania prawym dolnym rogu.
1. Wybierz **nie zakończenia wiersza** powitania po lewej stronie listy rozwijanej.
1. Wybierz **transmisji 115200** dla hello bezpośrednio z listy.
1. W polu wejściowym hello znajdujący się u góry okna monitora serial hello hello, wprowadź hello następujących informacji, jeśli zostanie wyświetlona prośba tooprovide je, a następnie kliknij przycisk **wysyłania**.
   * Identyfikator SSID sieci Wi-Fi
   * Hasło sieci Wi-Fi
   * Ciąg połączenia urządzenia

> [!Note]
> Witaj poświadczeń informacje są przechowywane w pamięci EEPROM z Sparkfun ESP8266 operacją odchyleń hello Po kliknięciu przycisku resetowania hello na powitania tablicy Sparkfun ESP8266 operacją deweloperów hello przykładowej aplikacji zapyta, jeśli chcesz uzyskać hello tooerase. Wprowadź `Y` informacji hello toohave wymazane, a monit tooprovide hello informacje ponownie.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Sprawdź, czy hello Przykładowa aplikacja działa prawidłowo

Jeśli widzisz hello następujące dane wyjściowe z okna monitora serial hello i hello migający LED na Sparkfun ESP8266 operacją deweloperów, hello Przykładowa aplikacja działa prawidłowo.

![ostateczne dane wyjściowe w arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Następne kroki

Pomyślnie połączony z Centrum IoT tooyour Sparkfun ESP8266 operacją deweloperów i wysyłane z Centrum IoT tooyour danych czujnika hello przechwytywane. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
