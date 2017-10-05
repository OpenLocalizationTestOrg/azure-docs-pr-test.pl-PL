---
title: "Pi malinowe do chmury (Node.js) - Połącz Pi malina z Centrum IoT Azure | Dokumentacja firmy Microsoft"
description: "Pi malina nawiązać połączenia z Centrum IoT Azure pi malina do wysyłania danych do chmury platformy Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "pi Azure iot malinowe, Centrum iot malinowe pi, pi malinowe wysyłania danych do chmury, malinowe pi do chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.openlocfilehash: 956ed5ab0ed38ddebd978b35eb54bc96567f0d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-nodejs"></a>Pi malinowe nawiązać połączenia z Centrum IoT Azure (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

W tym samouczku Rozpocznij od uczenia podstawy pracy z Pi malina, który działa Raspbian. Następnie Dowiedz się jak bezproblemowo połączyć z urządzenia do chmury przy użyciu [Centrum IoT Azure](iot-hub-what-is-iot-hub.md). Dla przykładów Windows 10 IoT Core, przejdź do [Centrum deweloperów systemu Windows](http://www.windowsondevices.com/).

Nie masz jeszcze zestawu? Spróbuj [emulatora malina Pi 3](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/). Lub kupowanie nowej kit [tutaj](https://azure.microsoft.com/develop/iot/starter-kits).

## <a name="what-you-do"></a>Co zrobić

* Instalator malinowe Pi.
* Tworzenie Centrum IoT.
* Zarejestruj urządzenie pi w Centrum IoT.
* Uruchom przykładową aplikację na Pi do wysyłania danych czujnika do Centrum IoT.

Pi malina nawiązać połączenia z Centrum IoT utworzony. Następnie uruchom przykładową aplikację na Pi do zbierania danych temperatury i wilgotności z czujnika BME280. Ponadto użytkownik wysyła dane czujników do Centrum IoT.

## <a name="what-you-learn"></a>Omawiane zagadnienia

* Sposób tworzenia Centrum Azure IoT i uzyskać nowy ciąg połączenia urządzenia.
* Jak nawiązać połączenia z czujnika BME280 Pi.
* Jak zbierać dane czujników, uruchamiając przykładową aplikację na Pi.
* Jak wysyłać dane czujników do Centrum IoT.

## <a name="what-you-need"></a>Co jest potrzebne

![Co jest potrzebne](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* Malina Pi 2 lub 3 Pi malina tablicy.
* Aktywna subskrypcja platformy Azure. Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.
* Monitor, klawiatura USB i myszy łączący się Pi.
* Mac lub komputer z systemem Windows lub Linux.
* Połączenie internetowe.
* 16 GB lub powyżej karty microSD.
* USB-karty sieciowej lub microSD na kartach SD Nagraj obraz systemu operacyjnego na karcie microSD.
* 5 volt potęgą 2-amp dostarczyć stopy 6 micro kabel USB.

Opcjonalne są następujące elementy:

* Złożony Adafruit BME280 temperatury, wykorzystania i wilgotności czujnika.
* Breadboard.
* 6 F/M zworek przewodów.
* Rozproszona LED 10 mm.

  > [!NOTE] 
  Te elementy są opcjonalne, ponieważ dane czujników symulowane obsługi próbki kodu.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a>Konfiguracja malinowe Pi

### <a name="install-the-raspbian-operating-system-for-pi"></a>Instalowanie systemu operacyjnego Raspbian pi

Przygotuj karty microSD instalacji obrazu Raspbian.

1. Pobierz Raspbian.
   1. [Pobierz Joasia Raspbian z pikseli](https://www.raspberrypi.org/downloads/raspbian/) (pliku .zip).
   1. Wyodrębnij obrazu Raspbian do folderu na komputerze.
1. Zainstaluj Raspbian karty microSD.
   1. [Pobierz i zainstaluj narzędzie palnika karty Etcher SD](https://etcher.io/).
   1. Uruchom Etcher i wybierz obraz Raspbian, który został wyodrębniony w kroku 1.
   1. Wybierz dysk karty microSD. Należy pamiętać, że Etcher może już wybrane poprawnego dysku.
   1. Kliknij przycisk Flash instalowanie Raspbian karty microSD.
   1. Karta microSD należy usunąć z komputera po zakończeniu instalacji. Jest bezpiecznie usunąć karta microSD bezpośrednio, ponieważ Etcher automatycznie wysuwa lub odinstalowuje karty microSD po zakończeniu.
   1. Włóż kartę microSD do Pi.

### <a name="enable-ssh-and-i2c"></a>Włącz SSH i I2C

1. Pi nawiązać monitora, klawiatury i myszy, uruchom Pi, a następnie zaloguj Raspbian przy użyciu `pi` jako nazwy użytkownika i `raspberry` jako hasło.
1. Kliknij ikonę malinowe > **preferencje** > **malina Pi konfiguracji**.

   ![Menu Preferencje Raspbian](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. Na **interfejsów** ustaw **I2C** i **SSH** do **włączyć**, a następnie kliknij przycisk **OK**. Jeśli nie masz fizycznych czujników i chcesz użyć danych czujnika symulowane, ten krok jest opcjonalny.

   ![Włącz I2C i SSH na malinowe Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
Aby włączyć SSH i I2C, można znaleźć więcej dokumentacji na [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) i [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).

### <a name="connect-the-sensor-to-pi"></a>Połącz z czujnika do Pi

Użyj przewodów breadboard i zworek LED i nawiązywać BME280 Pi w następujący sposób. Jeśli nie masz czujnika, Pomiń tę sekcję.

![Pi malina i czujnik połączenia](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

Czujnik BME280 może zbierać dane temperatury i wilgotności. I LED będzie blink w przypadku braku komunikacji między urządzeniem i chmurą. 

Czujnik numery PIN można użyć następujących połączeń:

| Uruchom (czujnik & LED)     | Końcowy (tablica)            | Kolor kabel   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin: 5 GB/S)             | 3, 3V PWR (Pin 1)       | Białe kabel   |
| GND (Pin 7 GB/S)             | GND (Pin 6)            | Brązowy kabel   |
| SCK (Pin 8 GB/S)             | I2C1 SDA (Pin 3)       | Kabel pomarańczowy  |
| SDI (Pin 10 GB/S)            | I2C1 SCL (Pin 5)       | Czerwony kabel     |
| VDD LED (Pin 18F)        | Interfejs GPIO 24 (Pin 18)       | Białe kabel   |
| GND LED (Pin 17F)        | GND (Pin 20)           | Czarne kabel   |

Kliknij, aby wyświetlić [malina Pi 2 i 3 mapowania kodu Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) użytkownikowi.

Po pomyślnie nawiązano połączenie BME280 Twojego Pi malina, należy go jak poniżej obrazu.

![Pi połączonych i BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a>Połączenie z siecią Pi

Włącz Pi przy użyciu micro kabla USB i zasilania. Łączenie Pi sieci przewodowej lub wykonaj przy użyciu kabla Ethernet [instrukcji Foundation Pi malina](https://www.raspberrypi.org/learning/software-guide/wifi/) do nawiązania połączenia z siecią bezprzewodową Pi. Po Twoje Pi została pomyślnie podłączona do sieci, należy pamiętać o [adres IP Twojego Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).

![Podłączony do sieci przewodowej](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> Upewnij się, że Pi jest podłączony do sieci z komputera. Na przykład jeśli komputer jest połączony z siecią bezprzewodową, gdy Pi jest połączony z siecią przewodową, może nie być wyświetlana w danych wyjściowych devdisco adres IP.

## <a name="run-a-sample-application-on-pi"></a>Uruchom przykładową aplikację na Pi

### <a name="clone-sample-application-and-install-the-prerequisite-packages"></a>Sklonuj przykładową aplikację i zainstalować wstępnie wymagane pakiety

1. Aby nawiązać połączenie z Pi malina, użyj jednej z następujących klientów SSH z komputera hosta.
    - [PuTTY](http://www.putty.org/) dla systemu Windows. Należy adres IP Twojego Pi połączenia go za pomocą protokołu SSH.
    - Wbudowane SSH klient Ubuntu lub macOS. Być może należy uruchomić `ssh pi@<ip address of pi>` nawiązać Pi za pośrednictwem protokołu SSH.

   > [!NOTE] 
   Domyślna nazwa użytkownika to `pi` , a hasło to `raspberry`.

1. Zainstaluj z Pi Node.js i NPM.
   
   Najpierw należy sprawdzić wersji środowiska Node.js przy użyciu następującego polecenia. 
   
   ```bash
   node -v
   ```

   Jeśli wersja jest starsza niż 4.x lub nie nie Node.js na Pi następnie uruchom następujące polecenie, aby zainstalować lub zaktualizować Node.js.

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. Klonowanie przykładowej aplikacji, uruchamiając następujące polecenie:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. Za pomocą następującego polecenia, należy zainstalować wszystkie pakiety. Zawiera urządzenia Azure IoT SDK, czujnik BME280 biblioteki i Biblioteka dołączenie Pi.

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   Może upłynąć kilka minut na zakończenie tego denpening procesu instalacji na połączenie sieciowe.

### <a name="configure-the-sample-application"></a>Konfigurowanie przykładowej aplikacji

1. Otwórz plik konfiguracji, uruchamiając następujące polecenia:

   ```bash
   nano config.json
   ```

   ![Plik konfiguracji](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   Istnieją dwa elementy w tym pliku mogą configurate. Pierwsza z nich jest `interval`, który definiuje odstęp czasu między dwa komunikaty, które wysyłają do chmury. Drugi `simulatedData`, która jest wartość logiczna, czy należy użyć danych czujnika symulowane lub nie.

   Jeśli użytkownik **nie ma czujnika**, ustaw `simulatedData` do wartości `true` dokonanie przykładowej aplikacji, tworzenia i używania danych czujnika symulowane.

1. Zapisz i zamknij naciskając formantu O > Enter > Control X.

### <a name="run-the-sample-application"></a>Uruchom przykładową aplikację

1. Uruchom przykładową aplikację, uruchamiając następujące polecenie:

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Upewnij się, możesz kopiowania i wklejania ciąg połączenia urządzenia w pojedynczy cudzysłów.


Powinny zostać wyświetlone następujące dane wyjściowe, który zawiera dane czujników i komunikaty, które są wysyłane do Centrum IoT.

![Dane wyjściowe — dane czujników wysłanych z Pi malina Centrum IoT](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a>Następne kroki

Uruchomiono przykładowej aplikacji do zbierania danych czujników i wysyłania go do Centrum IoT.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]