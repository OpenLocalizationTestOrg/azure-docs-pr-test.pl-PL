---
title: "aaaRaspberry Pi toocloud (Node.js) - Połącz Pi malina tooAzure Centrum IoT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup i połącz Pi malina tooAzure Centrum IoT platformy Pi malina toosend danych toohello chmury Azure w tym samouczku."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot malinowe pi malinowe pi iot hub malinowe pi wysyłania danych toocloud malinowe pi toocloud"
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 57a15ab3984021a9c18ff0aa1316a4d4c6ebdec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a>Połącz tooAzure Pi malina Centrum IoT (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

W tym samouczku Rozpocznij od uczenia hello podstawowe informacje dotyczące pracy z Pi malina, który działa Raspbian. Następnie dowiesz się, jak połączyć tooseamlessly chmury toohello urządzeń przy użyciu [Centrum IoT Azure](iot-hub-what-is-iot-hub.md). Dla przykładów Windows 10 IoT Core Przejdź toohello [Centrum deweloperów systemu Windows](http://www.windowsondevices.com/).

Nie masz jeszcze zestawu? Spróbuj [symulatora online Pi malina](iot-hub-raspberry-pi-web-simulator-get-started.md). Lub kupowanie nowej kit [tutaj](https://azure.microsoft.com/develop/iot/starter-kits).


## <a name="what-you-do"></a>Co zrobić

* Tworzenie Centrum IoT.
* Zarejestruj urządzenie pi w Centrum IoT.
* Instalator malinowe Pi.
* Uruchom przykładową aplikację w Centrum IoT tooyour danych czujnika toosend Pi.

Połącz Centrum IoT tooan Pi malina utworzony. Następnie możesz uruchomić przykładową aplikację na Pi toocollect temperatury i wilgotności danych z czujnika BME280. Ponadto możesz wysłać Centrum IoT tooyour danych czujnika hello.

## <a name="what-you-learn"></a>Omawiane zagadnienia

* Jak toocreate Centrum Azure IoT i uzyskać nowy ciąg połączenia urządzenia.
* Jak tooconnect Pi z czujnika BME280.
* Jak dane czujników toocollect uruchamiając przykładową aplikację na Pi.
* Jak Centrum IoT tooyour danych czujnika toosend.

## <a name="what-you-need"></a>Co jest potrzebne

![Co jest potrzebne](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* Witaj malina Pi 2 lub 3 Pi malina tablicy.
* Aktywna subskrypcja platformy Azure. Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.
* Monitor, klawiatura USB i myszy łączących tooPi.
* Mac lub komputer z systemem Windows lub Linux.
* Połączenie internetowe.
* 16 GB lub powyżej karty microSD.
* USB SD karty sieciowej lub microSD karty tooburn hello obraz systemu operacyjnego na karcie microSD hello.
* 5 volt potęgą 2-amp dostarczyć hello stopy 6 micro kabla USB.

Witaj, następujące elementy są opcjonalne:

* Złożony Adafruit BME280 temperatury, wykorzystania i wilgotności czujnika.
* Breadboard.
* 6 F/M zworek przewodów.
* Rozproszona LED 10 mm.


> [!NOTE] 
Te elementy są opcjonalne, ponieważ obsługa przykładowy kod hello symulowane danych czujnika.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a>Konfiguracja malinowe Pi

### <a name="install-hello-raspbian-operating-system-for-pi"></a>Instalowanie systemu operacyjnego Raspbian hello pi

Przygotuj karty microSD hello instalacji hello Raspbian obrazu.

1. Pobierz Raspbian.
   1. [Pobierz Joasia Raspbian z pulpitem](https://www.raspberrypi.org/downloads/raspbian/) (pliku .zip hello).
   1. Wyodrębnij hello Raspbian obrazu tooa folderu na komputerze.
1. Instalowanie karty microSD toohello Raspbian.
   1. [Pobierz i zainstaluj narzędzie palnika karty Etcher SD hello](https://etcher.io/).
   1. Uruchom Etcher i wybierz hello Raspbian obrazu, który został wyodrębniony w kroku 1.
   1. Wybierz dysk karty microSD hello. Należy pamiętać, że Etcher może już wybrane hello poprawnego dysku.
   1. Kliknij kartę microSD toohello Raspbian Flash tooinstall.
   1. Karta microSD hello należy usunąć z komputera po zakończeniu instalacji. Jest karta microSD hello bezpieczne tooremove bezpośrednio, ponieważ Etcher automatycznie wysuwa lub odinstalowuje karta microSD powitania po zakończeniu.
   1. Włóż kartę microSD hello do Pi.

### <a name="enable-ssh-and-i2c"></a>Włącz SSH i I2C

1. Połącz Pi toohello monitora, klawiatury i myszy, uruchom Pi, a następnie zaloguj Raspbian przy użyciu `pi` hello nazwy użytkownika i `raspberry` jako hello hasła.
1. Kliknij ikonę malinowe hello > **preferencje** > **malina Pi konfiguracji**.

   ![Witaj Raspbian preferencji menu](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. Na powitania **interfejsów** ustaw **I2C** i **SSH** za**włączyć**, a następnie kliknij przycisk **OK**. Jeśli nie masz fizycznych czujników i danych czujnika toouse symulowane, ten krok jest opcjonalny.

   ![Włącz I2C i SSH na malinowe Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH i I2C można znaleźć więcej dokumentacji na [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) i [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).

### <a name="connect-hello-sensor-toopi"></a>Połącz hello czujnik tooPi

Użyj hello breadboard i zworek przewodów tooconnect LED i BME280 tooPi. Jeśli nie masz czujnik hello [pominąć tę sekcję](#connect-pi-to-the-network).

![Witaj Pi malina i czujnik połączenia](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

Czujnik Hello BME280 może zbierać dane temperatury i wilgotności. I hello LED będzie blink w przypadku komunikacji między urządzenia i hello chmury. 

Czujnik numery PIN użyć hello następujących połączeń:

| Uruchom (czujnik & LED)     | Końcowy (tablica)            | Kolor kabel   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin: 5 GB/S)             | 3, 3V PWR (Pin 1)       | Białe kabel   |
| GND (Pin 7 GB/S)             | GND (Pin 6)            | Brązowy kabel   |
| SDI (Pin 10 GB/S)            | I2C1 SDA (Pin 3)       | Czerwony kabel     |
| SCK (Pin 8 GB/S)             | I2C1 SCL (Pin 5)       | Kabel pomarańczowy  |
| VDD LED (Pin 18F)        | Interfejs GPIO 24 (Pin 18)       | Białe kabel   |
| GND LED (Pin 17F)        | GND (Pin 20)           | Czarne kabel   |

Kliknij przycisk tooview [malina Pi 2 i 3 mapowania kodu Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) użytkownikowi.

Po nawiązaniu połączenia pomyślnie tooyour BME280 Pi malina, należy go jak poniżej obrazu.

![Pi połączonych i BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a>Łączenie z siecią toohello Pi

Włącz Pi przy użyciu kabla USB micro hello i hello zasilania. Użyj hello Ethernet kabel tooconnect Pi tooyour przewodowej sieci lub wykonaj hello [instrukcji hello Foundation Pi malina](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect sieci bezprzewodowej tooyour Pi. Po Twoje Pi został pomyślnie połączono toohello sieci, należy tootake wiadomości powitania [adres IP Twojego Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).

![Toowired połączonych sieci](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> Upewnij się, że Pi jest połączonych toohello sam sieci jako komputera. Na przykład, jeśli komputer jest połączony tooa sieci bezprzewodowej podczas Pi jest połączonych tooa ich z przewodową siecią, może nie być wyświetlana hello IP adres hello devdisco w danych wyjściowych.

## <a name="run-a-sample-application-on-pi"></a>Uruchom przykładową aplikację na Pi

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a>Sklonuj przykładową aplikację i zainstalować wstępnie wymagane pakiety hello

1. Użyj jednej z hello poniższych klientów SSH z tooyour tooconnect Pi malina Twojego hosta komputera.
   
   **Użytkownicy systemu Windows**
   1. Pobierz i zainstaluj [PuTTY](http://www.putty.org/) dla systemu Windows. 
   1. Skopiuj adres IP hello sekcji Pi do hello hosta nazwę (lub adres IP) i wybierz SSH jako hello typu połączenia.
   
   ![Programu puTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   **Mac i Ubuntu użytkowników**
   
   Przy użyciu wbudowanego klienta SSH hello na Ubuntu lub macOS. Może być konieczne toorun `ssh pi@<ip address of pi>` tooconnect Pi za pośrednictwem protokołu SSH.
   > [!NOTE] 
   Witaj domyślna nazwa użytkownika to `pi` , a hasło hello jest `raspberry`.

1. Zainstaluj środowisko Node.js i NPM tooyour Pi.
   
   Najpierw należy sprawdzić środowisko Node.js w wersji z hello następujące polecenia. 
   
   ```bash
   node -v
   ```

   Jeśli wersja hello jest starsza niż 4.x lub nie nie Node.js na Twoje Pi, uruchom następujące polecenie tooinstall hello, lub zaktualizuj Node.js.

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. Klonowanie hello przykładowej aplikacji, uruchamiając następujące polecenie hello:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. Zainstaluj wszystkie pakiety za hello następujące polecenia. Zawiera urządzenia Azure IoT SDK, czujnik BME280 biblioteki i Biblioteka dołączenie Pi.

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   Może upłynąć kilka minut toofinish tego procesu instalacji, w zależności od połączenia sieciowego.

### <a name="configure-hello-sample-application"></a>Skonfiguruj hello przykładowej aplikacji

1. Otwórz plik konfiguracji hello, uruchamiając następujące polecenia hello:

   ```bash
   nano config.json
   ```

   ![Plik konfiguracji](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   Istnieją dwa elementy w tym pliku mogą configurate. Witaj najpierw jest `interval`, który definiuje hello interwał (w milisekundach) między dwa komunikaty, które wysyłają toocloud. Witaj drugi `simulatedData`, czyli wartość logiczną parametru czy toouse symulowane dane czujników, czy nie.

   Jeśli użytkownik **nie ma czujnik hello**Ustaw hello `simulatedData` wartość zbyt`true` toomake hello przykładowej aplikacji tworzenia i używania danych czujnika symulowane.

1. Zapisz i zamknij naciskając formantu O > Enter > Control X.

### <a name="run-hello-sample-application"></a>Uruchom hello przykładowej aplikacji

Uruchom aplikację przykładową hello, uruchamiając następujące polecenie hello:

   ```bash
   sudo node index.js '<YOUR AZURE IOT HUB DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   Upewnij się, możesz kopiowania i wklejania ciąg połączenia urządzenia hello w apostrofy hello.


Powinien pojawić się następujące hello output, że pokazuje hello wiadomości powitania i danych czujnika, które są wysyłane tooyour Centrum IoT.

![Dane wyjściowe - wysyłane z Centrum IoT tooyour Pi malina dane czujników](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a>Następne kroki

Uruchomiono przykładowych danych czujnika toocollect aplikacji i wysyłać je tooyour Centrum IoT. wiadomości powitania toosee Twojego Pi malina został wysłany tooyour IoT hub lub wysyłania wiadomości tooyour Pi malina za pomocą interfejsu wiersza polecenia, zobacz hello [Zarządzaj chmury urządzenia wiadomości z Centrum iothub explorer samouczek](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
