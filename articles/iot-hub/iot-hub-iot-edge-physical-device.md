---
title: "aaaUse fizyczne urządzenia Azure IoT krawędzi | Dokumentacja firmy Microsoft"
description: "Jak toouse Texas Instruments w Sensor tag urządzenia toosend danych tooan Centrum IoT przez bramę krawędzi IoT uruchamianie na urządzeniu malina Pi 3. bramy Hello jest utworzony przy użyciu usługi Azure IoT krawędzi."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a>Użyj Azure IoT krawędź Pi malina tooIoT wiadomości urządzenia do chmury tooforward Centrum

W tym przewodniku hello [próbki niski energii Bluetooth] [ lnk-ble-samplecode] przedstawiono toouse [Azure IoT krawędzi] [ lnk-sdk] do:

* Przekazuj tooIoT telemetrii urządzenia do chmury Centrum z urządzenia fizycznego.
* Polecenia trasy z urządzenia fizycznego tooa Centrum IoT.

Przewodnik składa się z następujących elementów:

* **Architektura**: ważne informacje architektury o hello Bluetooth niski energii próbki.
* **Tworzenie i uruchamianie**: hello kroki wymagane toobuild i przykładowa hello wykonywania.

## <a name="architecture"></a>Architektura

wskazówki Hello pokazuje, jak toobuild i uruchom bramę brzegową IoT 3 Pi malina z systemem Raspbian Linux. Brama Hello jest utworzony przy użyciu IoT krawędzi. Witaj w przykładzie użyto danych temperatury toocollect urządzenia Texas Instruments Sensor tag Bluetooth małej energii (cz).

Po uruchomieniu hello brama brzegowa IoT go:

* Łączy tooa urządzeń Sensor tag przy użyciu hello energii małej Bluetooth (cz) protokołu.
* Łączy tooIoT Centrum przy użyciu protokołu hello HTTP.
* Przekazuje dane telemetryczne z tooIoT urządzeń Sensor tag hello koncentratora.
* Kieruje poleceń z urządzeń Sensor tag toohello Centrum IoT.

Brama Hello zawiera następujące moduły krawędzi IoT hello:

* A *modułu cz* który interfejsy z cz urządzenia tooreceive temperatury danych z urządzenia hello i wysyłania poleceń toohello urządzenia.
* A *modułu toodevice chmury cz* konwertujący JSON wiadomości wysyłane z Centrum IoT w instrukcji cz hello *modułu cz*.
* A *modułu rejestratora* który rejestruje wszystkie bramy wiadomości tooa pliku lokalnego.
* *Moduł mapowania tożsamości* który tłumaczy adresy MAC cz urządzenia i tożsamości urządzenia Azure IoT Hub.
* *Modułu Centrum IoT* który przekazuje Centrum IoT tooan danych telemetrycznych i odbiera polecenia urządzenia z Centrum IoT.
* A *cz drukarki moduł* interpretuje dane telemetryczne z hello cz urządzenia i drukowanie sformatowanych danych toohello konsoli tooenable Rozwiązywanie problemów i debugowania.

### <a name="how-data-flows-through-hello-gateway"></a>Jak dane przepływają przez bramę hello

powitania po diagram blokowy przedstawia potoku przepływu danych przekazywania telemetrii hello:

![Potok bramy przekazywania telemetrii](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

Hello kroki, które przyjmuje elementu telemetrii podróży z tooIoT urządzenia cz Centrum są:

1. urządzenie cz Hello generuje próbki temperatury i wysyła je przez moduł cz toohello Bluetooth hello bramy.
1. Moduł cz Hello odbiera próbki hello i publikuje ją brokera toohello wraz z hello adres MAC urządzenia hello.
1. Moduł mapowania tożsamości Hello przejmuje ten komunikat i używa wewnętrznej tabeli tootranslate hello adres MAC urządzenia hello do tożsamości urządzenia IoT Hub. Centrum IoT urządzenia tożsamości składa się z Identyfikatorem urządzenia i klucz urządzenia.
1. Moduł mapowania tożsamości Hello publikuje nowy komunikat zawierający hello temperatury przykładowych danych, hello adres MAC urządzenia hello, identyfikator urządzenia hello i hello klucza urządzenia.
1. Hello modułu Centrum IoT odbiera ten nowy komunikat (generowane przez moduł mapowania tożsamości hello) i publikuje ją tooIoT koncentratora.
1. Moduł rejestratora Hello rejestruje wszystkie komunikaty z pliku lokalnego tooa hello brokera.

powitania po diagram blokowy przedstawia potoku przepływu danych hello urządzenia polecenie:

![Urządzenia polecenie bramy potoku](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. Centrum IoT modułu okresowo sonduje Hello hello Centrum IoT nowe wiadomości polecenia.
1. Hello modułu Centrum IoT odebrania nowego komunikatu polecenie powoduje ona publikowanie go toohello brokera.
1. Moduł mapowania tożsamości Hello przejmuje wiadomości powitania polecenia i używa wewnętrznej tabeli tootranslate hello adres MAC urządzenia tooa identyfikator urządzenia Centrum IoT. Go następnie publikuje nowy komunikat zawierający adres MAC urządzenia docelowego hello hello w hello właściwości mapy wiadomości powitania.
1. Witaj cz chmury do urządzenia moduł przejmuje ten komunikat i tłumaczy go na powitania prawidłowego cz instrukcji hello cz modułu. Go następnie publikuje nowy komunikat.
1. Moduł cz Hello przejmuje ten komunikat i wykonuje instrukcję we/wy hello komunikując się z urządzeniem cz hello.
1. Moduł rejestratora Hello rejestruje wszystkie komunikaty z hello brokera tooa dysku pliku.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka należy aktywną subskrypcją platformy Azure.

> [!NOTE]
> Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk-free-trial].

Należy klient SSH na Twojej tooenable komputerów możesz tooremotely dostępu hello wiersza polecenia na powitania malina Pi.

- System Windows nie zawiera klienta SSH. Firma Microsoft zaleca używanie [PuTTY](http://www.putty.org/).
- Większość dystrybucje systemu Linux i Mac OS obejmują narzędzia wiersza polecenia SSH hello. Aby uzyskać więcej informacji, zobacz [SSH za pomocą systemu Linux lub Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).

## <a name="prepare-your-hardware"></a>Przygotowanie sprzętu

Ten samouczek zakłada się, czy używasz [Texas Instruments w Sensor tag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) urządzenie podłączone tooa malina Pi 3 systemem Raspbian.

### <a name="install-raspbian"></a>Zainstaluj Raspbian

Możesz użyć dowolnej z hello następujące opcje tooinstall Raspbian na urządzeniu malina Pi 3.

* tooinstall hello najnowszą wersję Raspbian, użyj hello [NOOBS] [ lnk-noobs] graficznego interfejsu użytkownika.
* Ręcznie [Pobierz] [ lnk-raspbian] i zapisywać najnowsze obraz powitania karty SD tooan systemu operacyjnego Raspbian hello.

### <a name="sign-in-and-access-hello-terminal"></a>Zaloguj się i uzyskać dostęp hello terminali

Masz dwie opcje tooaccess terminali środowiska użytkownika Pi malina:

* Jeśli klawiatura i monitorowanie połączonych tooyour Pi malina, możesz użyć hello Raspbian GUI tooaccess okno terminalu.

* Dostęp z wiersza polecenia hello na Twoje Pi malina przy użyciu protokołu SSH z komputera stacjonarnego.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Okno terminalu w hello graficznego interfejsu użytkownika

username są Hello domyślne poświadczenia dla Raspbian **pi** i hasło **malina**. Na pasku zadań hello w hello graficznego interfejsu użytkownika, możesz uruchomić hello **Terminal** narzędzie za pomocą ikony hello, która wygląda jak monitora.

#### <a name="sign-in-with-ssh"></a>Zaloguj się przy użyciu protokołu SSH

Można użyć SSH dla wiersza polecenia dostępu tooyour malina Pi. Artykuł Hello [SSH (Secure Shell)] [ lnk-pi-ssh] w tym artykule opisano sposób tooconfigure SSH na Twoje Pi malina i w jaki sposób tooconnect z [Windows] [ lnk-ssh-windows] lub [Systemu operacyjnego Linux & Mac][lnk-ssh-linux].

Zaloguj się przy użyciu nazwy użytkownika **pi** i hasło **malina**.

### <a name="install-bluez-537"></a>Zainstaluj BlueZ 5.37

Moduły cz Hello komunikować toohello Bluetooth sprzętu za pośrednictwem hello BlueZ stosu. Poprawnie wymagana wersja 5.37 BlueZ dla hello toowork modułów. Tych instrukcji upewnij się, że jest zainstalowana prawidłowa wersja BlueZ hello.

1. Zatrzymaj hello bieżącego demon bluetooth:

    ```sh
    sudo systemctl stop bluetooth
    ```

1. Zainstaluj zależności BlueZ hello:

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. Pobierz kod źródłowy BlueZ hello z bluez.org:

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. Rozpakuj hello kodu źródłowego:

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. Zmień katalogi toohello nowo utworzony folder:

    ```sh
    cd bluez-5.37
    ```

1. Skonfiguruj toobe kodu BlueZ hello wbudowane:

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. Tworzenie BlueZ:

    ```sh
    make
    ```

1. Zainstaluj BlueZ po zakończeniu kompilowania:

    ```sh
    sudo make install
    ```

1. Zmień konfigurację usługi systemd Bluetooth, wskazuje toohello Nowy demon bluetooth w pliku hello `/lib/systemd/system/bluetooth.service`. Zastąp wiersza "ExecStart" hello hello następującego tekstu:

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a>Włącz urządzeń Sensor tag toohello łączności z urządzenia malina Pi 3

Przed uruchomionych hello próbki należy tooverify czy Twoje malina Pi 3 można połączyć toohello urządzeń Sensor tag.

1. Upewnij się, hello `rfkill` zainstalowano narzędzie:

    ```sh
    sudo apt-get install rfkill
    ```

1. Odblokowany bluetooth na powitania malina Pi 3 i sprawdź, czy numer wersji hello **5.37**:

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. tooenter hello interakcyjne bluetooth powłoki, uruchom usługę bluetooth hello i wykonać hello **bluetoothctl** polecenia:

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Wprowadź polecenie hello **włączania zasilania** toopower zapasowej hello bluetooth kontrolera. polecenie Hello zwraca dane wyjściowe podobne toohello poniżej:

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. W powłoce interakcyjne bluetooth hello, wprowadź polecenie hello **na skanowania** tooscan dla urządzenia bluetooth. polecenie Hello zwraca dane wyjściowe podobne toohello poniżej:

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. Urządzeń Sensor tag hello stał się wykrywalny przez naciśnięcie przycisku małych hello (powitalne powinien flash LED zielony). Witaj malina Pi 3 powinien odnajdywanie urządzeń Sensor tag hello:

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    W tym przykładzie widać, że hello adres MAC hello Sensor tag urządzenie jest **A0:E6:F8:B5:F6:00**.

1. Wyłącz skanowanie wprowadzając hello **skanowania poza** polecenia:

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. Podłącz urządzenie Sensor tag tooyour przy użyciu adresu MAC, wprowadzając **połączyć \<adres MAC\>**. następujące przykładowe dane wyjściowe Hello jest skracana dla jasności:

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > Możesz wyświetlić listę właściwości GATT hello urządzenia hello ponownie, używając hello **listę atrybutów** polecenia.

1. Teraz możesz odłączyć od hello urządzenia przy użyciu hello **rozłączyć** polecenia, a następnie Zamknij z powłoki bluetooth hello przy użyciu hello **Zamknij** polecenia:

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

Możesz teraz gotowy toorun hello cz IoT krawędzi próbki na Twoje malina Pi 3.

## <a name="run-hello-iot-edge-ble-sample"></a>Uruchom hello cz krawędzi IoT próbki

toorun hello cz krawędzi IoT próbki, należy toocomplete trzech zadań:

* Skonfiguruj dwa przykładowe urządzenia w Centrum IoT.
* Tworzenie IoT Edge na urządzeniu malina Pi 3.
* Konfigurowania i uruchamiania przykładowych cz hello na urządzeniu malina Pi 3.

W czasie hello zapisu krawędzi IoT obsługuje modułów cz tylko w bramy z systemem Linux.

### <a name="configure-two-sample-devices-in-your-iot-hub"></a>Skonfiguruj dwa przykładowe urządzenia w Centrum IoT

* [Tworzenie Centrum IoT] [ lnk-create-hub] w Twojej subskrypcji platformy Azure, potrzebna hello nazwa Twojej toocomplete Centrum tego przewodnika. Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.
* Dodaj urządzenia o nazwie **SensorTag_01** tooyour Centrum IoT i zanotuj jego identyfikator i urządzenia klucza. Można użyć hello [explorer urządzenie lub Centrum iothub explorer] [ lnk-explorer-tools] narzędzi tooadd tym Centrum IoT toohello urządzeń utworzone w poprzednim kroku hello i tooretrieve jego klucza. Podczas konfigurowania bramy hello mapowania urządzeń Sensor tag toohello tego urządzenia.

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a>Tworzenie Azure IoT krawędzi w Twojej malinowe Pi 3

Zainstaluj zależności Edge IoT Azure:

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

Użyj następujących hello polecenia tooclone krawędzi IoT i wszystkie jego modułów podrzędnych tooyour katalogu macierzystego:

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

Jeśli masz pełną kopię hello krawędzi IoT repozytorium na Twoje malina Pi 3 można tworzyć za pomocą hello następujące polecenia z folderu hello, który zawiera hello zestawu SDK:

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a>Konfigurowanie i uruchamianie przykładowych cz hello na Twoje malina Pi 3

toobootstrap i wykonywania hello próbki, należy skonfigurować każdy moduł IoT krawędzi, który uczestniczy w hello bramy. Tej konfiguracji znajduje się w pliku JSON, a następnie należy skonfigurować pięć uczestniczących modułach IoT krawędzi. Brak przykładowy plik JSON w repozytorium hello o nazwie **bramy\_sample.json** których można używać jako hello punkt początkowy dla tworzenia pliku konfiguracji. Ten plik jest hello **przykłady/ble_gateway/src** folderu w lokalnej kopii hello krawędzi IoT repozytorium.

Witaj poniższych sekcjach opisano sposób tooedit tej konfiguracji pliku dla przykładu cz hello i założono tego repozytorium krawędzi IoT hello znajduje się w hello **/home/pi/iot-edge /** folderu na Twoje malina Pi 3. Jeśli repozytorium hello znajduje się w innym miejscu, odpowiednio hello ścieżki.

#### <a name="logger-configuration"></a>Konfiguracja rejestratora

Zakładając, że hello repozytorium bramy znajduje się w hello **/home/pi/iot-edge /** folderu, skonfigurować moduł rejestratora hello w następujący sposób:

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a>Konfiguracja modułu cz

Przykładowa konfiguracja Hello hello cz urządzenia zakłada urządzenia Texas Instruments w Sensor tag. Wszystkie standardowe cz urządzenie może działać jako GATT peryferyjnych powinny działać, ale może być konieczne tooupdate hello GATT cech identyfikatorów i danych. Dodaj hello adres MAC urządzenia Sensor tag:

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

Jeśli nie używasz urządzeń Sensor tag, przejrzyj hello dokumentacji dla Twojej cz toodetermine urządzenia, czy potrzebujesz tooupdate hello GATT cech identyfikatorów i wartości danych.

#### <a name="iot-hub-module"></a>Moduł Centrum IoT

Dodaj nazwę hello Centrum IoT. Wartość sufiksu Hello jest zwykle **azure devices.net**:

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a>Konfiguracja modułu mapowania tożsamości

Dodaj adres MAC hello Sensor tag urządzenia i identyfikator urządzenia hello i klucza hello **SensorTag_01** urządzenie dodane tooyour Centrum IoT:

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a>Konfiguracja modułu cz drukarki

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a>Konfiguracja modułu BLEC2D

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a>Konfiguracja routingu

Witaj następującej konfiguracji zapewnia następujące hello routingu między modułami krawędzi IoT:

* Witaj **rejestratora** modułu odbiera i rejestruje wszystkie komunikaty.
* Witaj **Sensor tag** moduł powoduje wysyłanie wiadomości powitania tooboth **mapowania** i **drukarki cz** modułów.
* Witaj **mapowania** moduł powoduje wysyłanie wiadomości toohello **Centrum IoTHub** toobe modułu przesłane tooyour Centrum IoT.
* Witaj **Centrum IoTHub** moduł powoduje wysyłanie wiadomości kopii toohello **mapowania** modułu.
* Witaj **mapowania** moduł powoduje wysyłanie wiadomości toohello **BLEC2D** modułu.
* Witaj **BLEC2D** moduł powoduje wysyłanie wiadomości kopii toohello **Sensor Tag** modułu.

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

Przykładowe hello toorun, przebieg hello ścieżki toohello plik JSON konfiguracji jako toohello parametru **cz\_bramy** binarnego. Witaj poniższego polecenia założono używasz hello **gateway_sample.json** pliku konfiguracji. Wykonaj to polecenie z hello **krawędzi iot** folderu na powitania Pi malina:

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

Może być konieczne toopress hello małych znajdującego się na toomake urządzeń Sensor tag hello wykrywalny go przed uruchomieniem hello próbki.

Po uruchomieniu hello przykładowe, można użyć hello [explorer urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) lub hello [explorer Centrum iothub](https://github.com/Azure/iothub-explorer) narzędzie toomonitor hello wiadomości powitania brama brzegowa IoT przekazuje z urządzeń Sensor tag hello. Na przykład za pomocą Eksploratora Centrum iothub można monitorować za pomocą następującego polecenia hello wiadomości urządzenia do chmury:

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a>Wysyłanie komunikatów z chmury do urządzeń

Moduł cz Hello obsługuje również wysyłanie poleceń z Centrum IoT toohello urządzenia. Można użyć hello [explorer urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) lub hello [explorer Centrum iothub](https://github.com/Azure/iothub-explorer) wiadomości JSON toosend narzędzie module bramy cz hello przekazuje toohello cz urządzenia.

Jeśli korzystasz z urządzenia Texas Instruments w Sensor tag hello, można włączyć LED hello czerwony, zielony LED lub Brzęczyk przez wysyłanie poleceń z Centrum IoT. Przed wysłaniem poleceń z Centrum IoT należy najpierw wysłać hello następujące dwa komunikaty JSON w kolejności. Następnie możesz wysłać dowolne tooturn polecenia hello na powitania świateł lub Brzęczyk.

1. Resetuj wszystkie LED i brzęczyk hello (wyłączone):

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. Skonfiguruj we/wy jako "remote":

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

Teraz możesz wysłać dowolne powitania po tooturn polecenia świateł hello lub Brzęczyk na urządzeniu Sensor tag hello:

* Włącz LED hello czerwony:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* Włącz LED hello zielony:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* Włącz Brzęczyk hello:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a>Następne kroki

Toogain większą wiedzę krawędzi IoT i wypróbować niektóre przykłady kodu, odwiedź stronę hello następujące samouczki deweloperów i zasoby:

* [Krawędź IoT Azure][lnk-sdk]

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Przewodnik dewelopera Centrum IoT][lnk-devguide]

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
