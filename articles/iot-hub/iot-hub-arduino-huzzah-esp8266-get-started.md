---
title: "toocloud aaaESP8266 — Połącz ESP8266 HUZZAH piór tooAzure Centrum IoT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup i połącz toosend danych toohello chmury Azure platforma Adafruit piór HUZZAH ESP8266 tooAzure Centrum IoT na jej w tym samouczku."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a>Połącz tooAzure Adafruit piór HUZZAH ESP8266 Centrum IoT w chmurze hello

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Połączenie między DHT22 ESP8266 HUZZAH piór i Centrum IoT](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a>Co zrobić


Połącz Centrum IoT tooan Adafruit piór HUZZAH ESP8266 utworzony. Następnie możesz uruchomić przykładową aplikację na ESP8266 toocollect hello temperatury i wilgotności danych z czujnika DHT22. Ponadto możesz wysłać Centrum IoT tooyour danych czujnika hello.

> [!NOTE]
> Jeśli używasz innych tablice ESP8266 nadal należy wykonać te kroki tooconnect on tooyour Centrum IoT. W zależności od tablicy hello ESP8266 używasz, może być konieczne tooreconfigure hello `LED_PIN`. Na przykład, jeśli używasz ESP8266 z AI Thinker, można zmienić go z `0` zbyt`2`. Nie masz jeszcze zestawu? Uzyskanie hello [witryny sieci Web Azure](http://azure.com/iotstarterkits).




## <a name="what-you-learn"></a>Omawiane zagadnienia

* Jak toocreate Centrum IoT i rejestrowanie urządzenia dla ESP8266 HUZZAH piór
* Jak tooconnect ESP8266 HUZZAH piór z czujnika hello i komputera
* Jak dane czujników toocollect uruchamiając przykładową aplikację na ESP8266 HUZZAH piór
* Jak toosend hello Centrum IoT tooyour danych czujnika

## <a name="what-you-need"></a>Co jest potrzebne

![Części potrzebne w samouczku hello](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete tej operacji, należy po części z Twojej piór HUZZAH ESP8266 Starter Kit hello:

* Witaj tablicy ESP8266 HUZZAH piór
* TooType Micro USB kabla A USB

Należy również następujące elementy dla środowiska deweloperskiego hello:

* Aktywna subskrypcja platformy Azure. Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.
* Mac lub komputera z systemem Windows lub Ubuntu.
* Sieci bezprzewodowej dla tooconnect ESP8266 HUZZAH piór do.
* Internet połączenia toodownload hello narzędzia do konfiguracji.
* [Arduino IDE](https://www.arduino.cc/en/main/software) wersji 1.6.8 lub nowszej. Starszych wersjach nie działają z hello AzureIoT biblioteki.

Witaj następujące elementy są opcjonalne w przypadku, gdy nie masz czujnika. Istnieje również opcja hello przy użyciu danych czujnika symulowane.

* Czujnik temperatury i wilgotności Adafruit DHT22
* Breadboard
* Przewodów zworek M/M


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a>Uzyskuj dostęp do ESP8266 HUZZAH piór hello czujników i komputera
W tej sekcji można podłączyć hello czujników tooyour tablicy. Następnie podłącz w komputerze tooyour urządzenia dla dalszego użytku.
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a>Połącz DHT22 temperatury i wilgotności czujnik tooFeather HUZZAH ESP8266

Użyj hello breadboard i zworek przewodów toomake hello połączenia w następujący sposób. Jeśli nie masz czujnika, Pomiń tę sekcję, ponieważ można użyć danych czujnika symulowane.

![Odwołanie do połączenia](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


Czujnik numery PIN użyć hello następujących połączeń:


| Start (czujnik)           | Końcowy (tablica)           | Kolor kabel   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 31F)            | 3V (przypiąć 58H)           | Czerwony kabel     |
| DANE (Pin 32F)           | Interfejs GPIO 2 (Pin 46A)       | Niebieski kabel    |
| GND (Pin 34F)            | GND (PIn 56I)          | Czarne kabel   |

Aby uzyskać więcej informacji, zobacz [Instalatora czujnik Adafruit DHT22](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) i [wyprowadzenia Adafruit piór HUZZAH Esp8266 styków](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).



Teraz ESP8266 Huzzah Twojego piór powinny być połączone z czujnika pracy.

![Uzyskuj DHT22 Huzzah piór](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a>Podłącz komputer tooyour ESP8266 HUZZAH piór

Jak pokazano w następnym, należy użyć hello Micro USB tooType A USB kabel tooconnect ESP8266 HUZZAH piór tooyour komputera.

![Podłącz komputer tooyour Huzzah piór](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Dodaj uprawnienia portu szeregowego (tylko Ubuntu)


Jeśli używasz Ubuntu, upewnij się, że masz toooperate uprawnienia hello na powitania USB portu z piór HUZZAH ESP8266. tooadd uprawnienia portu szeregowego, wykonaj następujące kroki:


1. Uruchom następujące polecenia w terminalu hello:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Pojawia się jeden z następujących danych wyjściowych hello:

   * crw-rw---xxxxxxxx uucp głównego 1
   * crw-rw---xxxxxxxx inicjowania połączeń głównego 1

   W danych wyjściowych hello, zwróć uwagę, że `uucp` lub `dialout` jest nazwa właściciela grupy hello hello portu USB.

1. Dodaj grupę toohello użytkowników hello, uruchamiając następujące polecenie hello:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`jest nazwa właściciela grupy hello uzyskanego w poprzednim kroku hello. `<username>`to nazwa użytkownika Ubuntu.

1. Wylogować się z Ubuntu, a następnie zaloguj ponownie na powitania tooappear zmiany.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Zbierać dane czujników oraz wysyłać je tooyour Centrum IoT

W tej sekcji Wdróż i uruchom przykładową aplikację na ESP8266 HUZZAH piór. Hello przykładowej aplikacji miganie hello LED na ESP8266 HUZZAH piór i wysyła hello temperatury i wilgotności dane zbierane z hello DHT22 czujnik tooyour Centrum IoT.

### <a name="get-hello-sample-application-from-github"></a>Pobierz hello przykładowej aplikacji z usługi GitHub

Witaj przykładowej aplikacji znajduje się w witrynie GitHub. Klonuj repozytorium przykładowej hello, zawierający hello przykładowej aplikacji z usługi GitHub. repozytorium przykładowej hello tooclone, wykonaj następujące kroki:

1. Otwórz wiersz polecenia lub okno terminalu.
1. Przejdź tooa folder docelowy toobe aplikacji przykładowej hello przechowywane.
1. Uruchom następujące polecenie hello:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

Instalacja pakietu powitania dla ESP8266 HUZZAH piór w Arduino IDE hello:

1. Otwórz folder hello przechowywania hello przykładowej aplikacji.
1. Otwórz plik app.ino hello w folderze aplikacji hello hello Arduino IDE.

   ![Otwórz aplikację przykładową hello w Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. W hello Arduino IDE, kliknij przycisk **pliku** > **preferencje**.
1. W hello **preferencje** okna dialogowego, kliknij przycisk Dalej toohello ikona hello **dodatkowych adresów URL Menedżera tablice** pole.
1. W oknie podręcznym hello, wprowadź hello następującego adresu URL, a następnie kliknij przycisk **OK**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Adres url pakietu tooa punktu Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. W hello **preferencji** okno dialogowe, kliknij przycisk **OK**.
1. Kliknij przycisk **narzędzia** > **tablicy** > **Menedżera tablice**, a następnie wyszukaj esp8266.

   Tablice Menedżera wskazuje, że ESP8266 przy użyciu wersji 2.2.0 lub nowszej jest zainstalowane.

   ![Pakiet esp8266 Hello jest zainstalowany](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. Kliknij przycisk **narzędzia** > **tablicy** > **Adafruit HUZZAH ESP8266**.

### <a name="install-necessary-libraries"></a>Zainstaluj wymagane biblioteki

1. W hello Arduino IDE, kliknij przycisk **szkicu** > **obejmują biblioteki** > **zarządzanie bibliotekami**.
1. Wyszukiwanie hello następujące nazwy bibliotek jeden po drugim. Dla każdej biblioteki można znaleźć, kliknij przycisk **zainstalować**.
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>Nie masz rzeczywistych czujnik DHT22?

Hello przykładowej aplikacji można symulować danych temperatury i wilgotności, w przypadku, gdy nie ma rzeczywistego czujnik DHT22. tooset zapasowych danych toouse symulowane hello przykładowej aplikacji, wykonaj następujące kroki:

1. Otwórz hello `config.h` pliku w hello `app` folderu.
1. Znajdź powitania po wierszu kodu i zmień wartość hello z `false` zbyt`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![Konfigurowanie hello przykładowych aplikacji toouse symulowane danych](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. Zapisz plik hello z `Control-s`.

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a>Wdrażanie hello przykładowej aplikacji tooFeather HUZZAH ESP8266

1. W hello Arduino IDE, kliknij przycisk **narzędzie** > **portu**, a następnie kliknij przycisk portu szeregowego hello ESP8266 HUZZAH piór.
1. Kliknij przycisk **szkicu** > **przekazać** toobuild i wdrażanie hello przykładowej aplikacji tooFeather HUZZAH ESP8266.

### <a name="enter-your-credentials"></a>Wprowadź swoje poświadczenia

Po pomyślnym ukończeniu przekazywania hello wykonaj te kroki tooenter poświadczeń:

1. W hello Arduino IDE, kliknij przycisk **narzędzia** > **Serial Monitor**.
1. W oknie Monitora serial hello Zwróć uwagę hello dwóch list rozwijanych w hello prawym dolnym rogu.
1. Wybierz **nie zakończenia wiersza** powitania po lewej stronie listy rozwijanej.
1. Wybierz **transmisji 115200** dla hello bezpośrednio z listy.
1. W polu wejściowym hello znajdujący się u góry okna monitora serial hello hello, wprowadź hello następujących informacji, jeśli zostanie wyświetlona prośba tooprovide je, a następnie kliknij przycisk **wysyłania**.
   * Identyfikator SSID sieci Wi-Fi
   * Hasło sieci Wi-Fi
   * Ciąg połączenia urządzenia

> [!Note]
> informacje poświadczeń Hello są przechowywane w pamięci EEPROM piór HUZZAH ESP8266 hello. Jeśli klikniesz przycisk reset hello na powitania tablicy ESP8266 HUZZAH piór hello przykładowej aplikacji pyta użytkownika tooerase hello informacji. Wprowadź `Y` informacji hello toohave wymazane. Zostanie wyświetlona prośba tooprovide hello informacji po raz drugi.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Sprawdź, czy hello Przykładowa aplikacja działa prawidłowo

Jeśli widzisz hello następujące dane wyjściowe z okna monitora serial hello i hello migający LED na piór HUZZAH ESP8266, hello Przykładowa aplikacja działa prawidłowo.

![Ostateczne dane wyjściowe w Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Następne kroki

Pomyślnie połączony z Centrum IoT tooyour ESP8266 HUZZAH piór i wysyłane z Centrum IoT tooyour danych czujnika hello przechwytywane. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

