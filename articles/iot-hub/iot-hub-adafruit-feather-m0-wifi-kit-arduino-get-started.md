---
title: "M0 toocloud: połączenia Wi-Fi piór M0 tooAzure Centrum IoT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset Konfigurowanie i połączenia sieci Wi-Fi Adafruit piór M0 tooAzure Centrum IoT toosend danych toohello chmury Azure platforma w tym samouczku."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a>Połączenia sieci Wi-Fi Adafruit piór M0 tooAzure Centrum IoT w chmurze hello
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Połączenie między BME280, M0 piór sieci Wi-Fi i Centrum IoT](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

W tym samouczku Rozpocznij od uczenia hello podstawowe informacje dotyczące pracy z tablicy Arduino. Następnie dowiesz się, jak połączyć tooseamlessly chmury toohello urządzeń przy użyciu [Centrum IoT Azure](iot-hub-what-is-iot-hub.md).

## <a name="what-you-do"></a>Co zrobić

Połącz Centrum IoT tooan Adafruit piór M0 sieci Wi-Fi, który utworzono. Następnie można uruchomić przykładową aplikację na M0 sieci Wi-Fi toocollect hello temperatury i wilgotności danych z BME280. Ponadto możesz wysłać Centrum IoT tooyour danych czujnika hello.


## <a name="what-you-learn"></a>Omawiane zagadnienia

* Jak toocreate Centrum IoT i rejestrowanie urządzenia dla M0 piór sieci Wi-Fi
* Jak tooconnect M0 piór sieci Wi-Fi z czujnika hello i komputera
* Jak dane czujników toocollect uruchamiając przykładową aplikację na M0 piór sieci Wi-Fi
* Jak toosend hello Centrum IoT tooyour danych czujnika

## <a name="what-you-need"></a>Co jest potrzebne

![Części potrzebne w samouczku hello](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete tej operacji, należy powitania po części z Twojej startowy piór M0 sieci Wi-Fi:

* Witaj tablicy M0 piór sieci Wi-Fi
* TooType Micro USB kabla A USB

Należy również następujące elementy dla środowiska deweloperskiego hello:

* Aktywna subskrypcja platformy Azure. Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.
* Mac lub komputera z systemem Windows lub Ubuntu.
* Sieć bezprzewodową tooconnect M0 piór sieci Wi-Fi do.
* Internet połączenia toodownload hello narzędzie konfiguracji.
* [Arduino IDE](https://www.arduino.cc/en/main/software) wersji 1.6.8 lub nowszej. Starszych wersjach nie działają z biblioteki Azure IoT Hub hello.

Jeśli nie masz czujnika hello następujące elementy są opcjonalne. Istnieje również opcja hello przy użyciu danych czujnika symulowanego:

* Czujnik temperatury i wilgotności BME280
* Breadboard
* Przewodów zworek M/M

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a>Połącz M0 piór sieci Wi-Fi z czujnika hello i komputera
W tej sekcji można podłączyć hello czujników tooyour tablicy. Następnie podłącz w komputerze tooyour urządzenia dla dalszego użytku.

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a>Połącz DHT22 temperatury i wilgotności czujnik tooFeather M0 sieci Wi-Fi

Użyj hello breadboard i zworek przewodów toomake hello połączenia. Jeśli nie masz czujnika, Pomiń tę sekcję, ponieważ można użyć danych czujnika symulowane.

![Odwołanie do połączenia](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


Czujnik numery PIN użyć hello następujących połączeń:


| Start (czujnik)           | Końcowy (tablica)            | Kolor kabel   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 27A)            | 3V (3A kodu Pin)            | Czerwony kabel     |
| GND (Pin 29A)            | GND (6A kodu Pin)           | Czarne kabel   |
| SCK (Pin 30A)            | SCK (Pin 12A)          | Żółty kabel  |
| SDO (Pin 31A)            | MI (Pin 14A)           | Białe kabel   |
| SDI (Pin 32A)            | M0 (Pin 13A)           | Niebieski kabel    |
| CS (Pin 33A)             | Interfejs GPIO 5 (Pin 15J)       | Kabel pomarańczowy  |

Aby uzyskać więcej informacji, zobacz [Adafruit BME280 wilgotności + barometryczne wykorzystania podgrupach czujnik temperatury](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) i [wyprowadzenia styków sieci Wi-Fi Adafruit piór M0](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).



Teraz sieci Wi-Fi M0 piór powinny być połączone z czujnika pracy.

![Uzyskuj DHT22 Huzzah piór](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a>Podłącz komputer tooyour M0 piór sieci Wi-Fi

Użyć hello Micro USB tooType A USB kabel tooconnect M0 piór sieci Wi-Fi tooyour komputera, jak pokazano:

![Podłącz komputer tooyour Huzzah piór](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Dodaj uprawnienia portu szeregowego (tylko Ubuntu)

Jeśli używasz Ubuntu, upewnij się, że masz toooperate uprawnienia hello na powitania USB portu z piór M0 sieci Wi-Fi. tooadd uprawnienia portu szeregowego, wykonaj następujące kroki:


1. W terminalu uruchom następujące polecenia hello:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Pojawia się jeden z następujących danych wyjściowych hello:

   * crw-rw---xxxxxxxx uucp głównego 1
   * crw-rw---xxxxxxxx inicjowania połączeń głównego 1

   W danych wyjściowych hello, zwróć uwagę, że `uucp` lub `dialout` jest nazwa właściciela grupy hello hello portu USB.

2. tooadd hello toohello grupy użytkowników, uruchom następujące polecenie hello:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   W poprzednim kroku hello uzyskać nazwę właściciela grupy hello `<group-owner-name>`. Nazwa użytkownika Ubuntu jest `<username>`.

3. Dla tooappear zmiany hello Wyloguj się Ubuntu i zaloguj ponownie.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Zbierać dane czujników oraz wysyłać je tooyour Centrum IoT

W tej sekcji Wdróż i uruchom przykładową aplikację na M0 piór sieci Wi-Fi. Witaj przykładowej aplikacji sprawia, że hello migania LED na M0 piór sieci Wi-Fi. Następnie wysyła hello temperatury i wilgotności dane zbierane z hello BME280 czujnik tooyour Centrum IoT.

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a>Pobierz hello przykładowej aplikacji z usługi GitHub i przygotowanie hello Arduino IDE

Witaj przykładowej aplikacji znajduje się w witrynie GitHub. Klonuj repozytorium przykładowej hello, zawierający hello przykładowej aplikacji z usługi GitHub. repozytorium przykładowej hello tooclone, wykonaj następujące kroki:

1. Otwórz wiersz polecenia lub okno terminalu.

2. Przejdź tooa folder docelowy toobe aplikacji przykładowej hello przechowywane.
3. Uruchom następujące polecenie hello:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a>Zainstaluj pakiet powitania dla M0 piór sieci Wi-Fi w hello Arduino IDE

1. Otwórz folder hello przechowywania hello przykładowej aplikacji.

2. Otwórz plik app.ino hello w folderze aplikacji hello hello Arduino IDE.

   ![Otwórz aplikację przykładową hello w Arduino IDE](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. Kliknij przycisk **pliku** > **preferencje** (system Windows/Linux) lub **Arduino** > **preferencje** (Mac) i skopiuj i Wklej hello poniższe łącze do hello **dodatkowych adresów URL Menedżera tablice** opcji hello preferencje Arduino IDE.
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. Kliknij przycisk **narzędzia** > **tablicy** > **Menedżera tablice**, a następnie zainstaluj hello `Arduino SAMD Boards` wersji `1.6.2` lub nowszej. 

1. Następnie w tym samym oknie Witaj, zainstaluj `Adafruit SAMD Boards` tooadd hello tablicy pliku definicji pakietu.

   ![Pakiet esp8266 Hello jest zainstalowany](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. Kliknij przycisk **narzędzia** > **tablicy** > **Adafruit M0 sieci Wi-Fi**.

5. Zainstaluj sterowniki (tylko dla systemu Windows). Po podłączeniu M0 piór sieci Wi-Fi, może być konieczne tooinstall sterownika. Kliknij przycisk [hello łącze na stronie sieci Web hello](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload hello sterownik Instalatora. Wykonaj hello kroki tooinstall hello sterowniki, które mają.

### <a name="install-necessary-libraries"></a>Zainstaluj wymagane biblioteki

1. W hello Arduino IDE, kliknij przycisk **szkicu** > **obejmują biblioteki** > **zarządzanie bibliotekami**.

2. Wyszukiwanie hello następujące nazwy bibliotek jeden po drugim. Dla każdej biblioteki można znaleźć, kliknij przycisk **zainstalować**:

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. Ręcznie zainstaluj `Adafruit_WINC1500`. Przejdź za[tej witryny sieci Web](https://github.com/adafruit/Adafruit_WINC1500) i kliknij przycisk **klonowania lub pobierania** > **Pobierz ZIP**. Następnie w środowiskiem IDE Arduino go za**szkicu** > **obejmują biblioteki** > **dodać .zip biblioteki** i Dodaj plik zip hello.

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a>Użyj hello przykładowej aplikacji, jeśli nie masz rzeczywistych czujnik BME280

Jeśli nie masz rzeczywistych czujnik BME280 hello przykładowej aplikacji można symulować temperatury i wilgotności danych. tooset zapasowych danych toouse symulowane hello przykładowej aplikacji, wykonaj następujące kroki:

1. Otwórz hello `config.h` pliku w hello `app` folderu.

2. Znajdź powitania po wierszu kodu i zmień wartość hello z `false` zbyt`true`:

   ```c
   define SIMULATED_DATA true
   ```
   ![Konfigurowanie hello przykładowych aplikacji toouse symulowane danych](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. Zapisz plik hello z `Control-s`.

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a>Wdrażanie hello przykładowej aplikacji tooFeather M0 sieci Wi-Fi

1. W hello Arduino IDE, kliknij przycisk **narzędzie** > **portu**, a następnie kliknij przycisk portu szeregowego hello M0 piór sieci Wi-Fi.

2. Kliknij przycisk **szkicu** > **przekazać** toobuild i wdrażanie hello przykładowej aplikacji tooFeather M0 sieci Wi-Fi.

### <a name="enter-your-credentials"></a>Wprowadź swoje poświadczenia

Po pomyślnym ukończeniu przekazywania hello wykonaj te kroki tooenter poświadczeń:

1. W hello Arduino IDE, kliknij przycisk **narzędzia** > **Serial Monitor**.

2. W hello prawym dolnym rogu okna monitora serial hello, wybierz **nie zakończenia wiersza** na liście rozwijanej hello powitania po lewej stronie.
3. Wybierz **transmisji 115200** na liście rozwijanej hello na powitania prawo.
4. W polu wejściowym hello u góry hello, wprowadź hello następujących informacji, jeśli masz pytanie tooprovide i kliknij przycisk **wysyłania**:

   * Identyfikator SSID sieci Wi-Fi
   * Hasło sieci Wi-Fi
   * Ciąg połączenia urządzenia

> [!Note]
> informacje poświadczeń Hello są przechowywane w pamięci EEPROM piór M0 WiFi hello. Jeśli klikniesz przycisk reset hello na powitania tablicy M0 piór sieci Wi-Fi, hello przykładowej aplikacji pyta użytkownika tooerase hello informacji. Wprowadź `Y` tooerase hello informacji. Monit tooprovide hello informacji po raz drugi.

### <a name="verify-that-hello-sample-application-is-running-successfully"></a>Sprawdź, czy hello Przykładowa aplikacja działa prawidłowo

Jeśli widzisz hello następujące dane wyjściowe z okna monitora serial hello i hello migający LED na piór M0 Wi-Fi, hello Przykładowa aplikacja działa prawidłowo:

![Ostateczne dane wyjściowe w Arduino IDE](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a>Następne kroki

Pomyślnie połączony Centrum IoT tooyour M0 piór sieci Wi-Fi i wysyłane z Centrum IoT tooyour danych czujnika hello przechwytywane. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

