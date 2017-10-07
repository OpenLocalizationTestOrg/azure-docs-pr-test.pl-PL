---
title: "aaaRaspberry Pi toocloud (C) - Połącz Pi malina tooAzure Centrum IoT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup i połącz Pi malina tooAzure Centrum IoT platformy Pi malina toosend danych toohello chmury Azure w tym samouczku."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot malinowe pi malinowe pi iot hub malinowe pi wysyłania danych toocloud malinowe pi toocloud"
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05086890458e196d7fdc87a53fcabb9386245d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-c"></a>Połącz Pi malina tooAzure IoT Hub (C)

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

![Co jest potrzebne](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

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

### <a name="enable-ssh-and-spi"></a>Włącz SSH i SPI

1. Połącz Pi toohello monitora, klawiatury i myszy, uruchom Pi, a następnie zaloguj Raspbian przy użyciu `pi` hello nazwy użytkownika i `raspberry` jako hello hasła.
1. Kliknij ikonę malinowe hello > **preferencje** > **malina Pi konfiguracji**.

   ![Witaj Raspbian preferencji menu](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. Na powitania **interfejsów** ustaw **SPI** i **SSH** za**włączyć**, a następnie kliknij przycisk **OK**. Jeśli nie masz fizycznych czujników i danych czujnika toouse symulowane, ten krok jest opcjonalny.

   ![Włącz SPI i SSH na malinowe Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH i SPI, można znaleźć więcej dokumentacji na [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) i [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).

### <a name="connect-hello-sensor-toopi"></a>Połącz hello czujnik tooPi

Użyj hello breadboard i zworek przewodów tooconnect LED i BME280 tooPi. Jeśli nie masz czujnik hello [pominąć tę sekcję](#connect-pi-to-the-network).

![Witaj Pi malina i czujnik połączenia](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

Czujnik Hello BME280 może zbierać dane temperatury i wilgotności. I hello LED będzie blink w przypadku komunikacji między urządzenia i hello chmury. 

Czujnik numery PIN użyć hello następujących połączeń:

| Uruchom (czujnik & LED)     | Końcowy (tablica)            | Kolor kabel   |
| -----------------------  | ---------------------- | ------------: |
| VDD LED (Pin: 5 GB/S)         | Interfejs GPIO 4 (Pin 7)         | Białe kabel   |
| GND LED (Pin 6 GB/S)         | GND (Pin 6)            | Czarne kabel   |
| VDD (Pin 18F)            | 3, 3V PWR (Pin 17)      | Białe kabel   |
| GND (Pin 20F)            | GND (Pin 20)           | Czarne kabel   |
| SCK (Pin 21F)            | SPI0 SCLK (Pin 23)     | Kabel pomarańczowy  |
| SDO (Pin 22F)            | SPI0 MISO (Pin 21)     | Żółty kabel  |
| SDI (Pin 23F)            | SPI0 MOSI (Pin 19)     | Zielony kabel   |
| CS (Pin 24F)             | SPI0 CS (Pin 24)       | Niebieski kabel    |

Kliknij przycisk tooview [malina Pi 2 i 3 mapowania kodu Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) użytkownikowi.

Po nawiązaniu połączenia pomyślnie tooyour BME280 Pi malina, należy go jak poniżej obrazu.

![Pi połączonych i BME280](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a>Łączenie z siecią toohello Pi

Włącz Pi przy użyciu kabla USB micro hello i hello zasilania. Użyj hello Ethernet kabel tooconnect Pi tooyour przewodowej sieci lub wykonaj hello [instrukcji hello Foundation Pi malina](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect sieci bezprzewodowej tooyour Pi. Po Twoje Pi został pomyślnie połączono toohello sieci, należy tootake wiadomości powitania [adres IP Twojego Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).

![Toowired połączonych sieci](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a>Uruchom przykładową aplikację na Pi

### <a name="install-hello-prerequisite-packages"></a>Zainstaluj wstępnie wymagane pakiety hello

1. Użyj jednej z hello poniższych klientów SSH z tooyour tooconnect Pi malina Twojego hosta komputera.
   
   **Użytkownicy systemu Windows**
   1. Pobierz i zainstaluj [PuTTY](http://www.putty.org/) dla systemu Windows. 
   1. Skopiuj adres IP hello sekcji Pi do hello hosta nazwę (lub adres IP) i wybierz SSH jako hello typu połączenia.
   
   ![Programu puTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   **Mac i Ubuntu użytkowników**
   
   Przy użyciu wbudowanego klienta SSH hello na Ubuntu lub macOS. Może być konieczne toorun `ssh pi@<ip address of pi>` tooconnect Pi za pośrednictwem protokołu SSH.
   > [!NOTE] 
   Witaj domyślna nazwa użytkownika to `pi` , a hasło hello jest `raspberry`.

1. Instalowanie wymagań wstępnych pakietów hello hello zestawu SDK usługi Microsoft Azure IoT urządzenia C i Cmake, uruchamiając następujące polecenia hello:

   ```bash
   grep -q -F 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   grep -q -F 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA6A393E4C2257F
   sudo apt-get update
   sudo apt-get install -y azure-iot-sdk-c-dev cmake libcurl4-openssl-dev git-core
   git clone git://git.drogon.net/wiringPi
   cd ./wiringPi
   ./build
   ```


### <a name="configure-hello-sample-application"></a>Skonfiguruj hello przykładowej aplikacji

1. Klonowanie hello przykładowej aplikacji, uruchamiając następujące polecenie hello:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. Otwórz plik konfiguracji hello, uruchamiając następujące polecenia hello:

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![Plik konfiguracji](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   Istnieją dwa makra w tym pliku mogą configurate. Witaj najpierw jest `INTERVAL`, który definiuje hello interwał (w milisekundach) między dwa komunikaty, które wysyłają toocloud. Witaj drugi `SIMULATED_DATA`, czyli wartość logiczną parametru czy toouse symulowane dane czujników, czy nie.

   Jeśli użytkownik **nie ma czujnik hello**Ustaw hello `SIMULATED_DATA` wartość zbyt`1` toomake hello przykładowej aplikacji tworzenia i używania danych czujnika symulowane.

1. Zapisz i zamknij naciskając formantu O > Enter > Control X.

### <a name="build-and-run-hello-sample-application"></a>Tworzenie i uruchamianie hello przykładowej aplikacji

1. Tworzenie aplikacji przykładowej hello, uruchamiając następujące polecenie hello:

   ```bash
   cmake . && make
   ```
   ![Dane wyjściowe kompilacji](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. Uruchom aplikację przykładową hello, uruchamiając następujące polecenie hello:

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   Upewnij się, możesz kopiowania i wklejania ciąg połączenia urządzenia hello w apostrofy hello.


Powinien pojawić się następujące hello output, że pokazuje hello wiadomości powitania i danych czujnika, które są wysyłane tooyour Centrum IoT.

![Dane wyjściowe - wysyłane z Centrum IoT tooyour Pi malina dane czujników](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a>Następne kroki

Uruchomiono przykładowych danych czujnika toocollect aplikacji i wysyłać je tooyour Centrum IoT. wiadomości powitania toosee Twojego Pi malina został wysłany tooyour IoT hub lub wysyłania wiadomości tooyour Pi malina za pomocą interfejsu wiersza polecenia, zobacz hello [Zarządzaj chmury urządzenia wiadomości z Centrum iothub explorer samouczek](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
