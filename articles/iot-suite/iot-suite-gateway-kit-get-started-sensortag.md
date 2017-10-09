---
title: "aaaConnect tooAzure bramy pakiet IoT przy użyciu NUC Intel | Dokumentacja firmy Microsoft"
description: "Użyj hello IoT Microsoft komercyjnych Kit bramy i hello zdalnego wstępnie skonfigurowane rozwiązanie monitorowania. Użyj hello Azure IoT krawędzi bramy tooenable zdalne monitorowanie rozwiązania toohello tooconnect urządzeń Sensor tag, wysyłania danych telemetrycznych toohello chmury, a odpowiadać toomethods wywoływane z pulpitu nawigacyjnego rozwiązania hello."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 6f98ee3c1e2311a8644da9d72d40e671e7cbcf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a>Połącz Twoje toohello bramy Azure IoT krawędzi zdalne monitorowanie wstępnie skonfigurowane rozwiązanie i wysłać dane telemetryczne z Sensor tag

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

Ten samouczek pokazuje, jak toouse Azure IoT krawędzi danych temperatury i wilgotności toosend z Sensor tag toohello zdalnego monitorowania urządzenia wstępnie skonfigurowane rozwiązanie. Witaj Sensor tag łączy toohello Intel NUC bramy przy użyciu funkcji Bluetooth. samouczku Hello:

- Azure IoT krawędzi tooimplement bramy próbki.
- monitorowania zdalnego pakiet IoT Hello wstępnie skonfigurowane rozwiązanie jako hello oparte na chmurze zaplecza.

## <a name="overview"></a>Omówienie

W tym samouczku można wykonać hello następujące kroki:

- Wdróż wystąpienie wstępnie skonfigurowane rozwiązanie tooyour subskrypcji platformy Azure hello zdalnego monitorowania. Ten krok automatycznie wdraża i konfiguruje wiele usług platformy Azure.
- Konfigurowanie toocommunicate urządzenia bramy NUC firmy Intel, tak do komputera i hello zdalnego rozwiązanie monitorowania.
- Konfigurowanie telemetrii tooreceive Intel NUC bramy z urządzeń Sensor tag i wysłać go toohello zdalny pulpit nawigacyjny monitorowania.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[Texas Instruments Sensor tag cz][lnk-sensortag]. W tym samouczku pobiera dane telemetryczne z urządzeń Sensor tag hello w przez sieć Bluetooth.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Witaj zdalnego monitorowania przepisów rozwiązania zbiór usług platformy Azure w ramach subskrypcji platformy Azure. wdrożenie Hello odzwierciedla architektury przedsiębiorstwa prawdziwe. tooavoid opłat niepotrzebnych wykorzystania platformy Azure, usunąć wystąpienie usługi hello wstępnie skonfigurowane rozwiązanie azureiotsuite.com po zakończeniu z nim. Jeśli należy ponownie hello wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć. Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a>Konfiguracja połączenia Bluetooth

Konfigurować funkcję Bluetooth na powitania Intel NUC tooenable hello Sensor tag urządzenia tooconnect i wysyłania danych telemetrycznych.

### <a name="find-hello-mac-address-of-hello-sensortag"></a>Znajdź adres MAC hello hello Sensor tag

1. W powłoce hello na powitania Intel NUC Uruchom hello następujące usługi Bluetooth hello toounblock polecenia:

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. Hello uruchom następujące polecenia usługa Bluetooth hello toostart na powitania NUC firmy Intel, a wprowadź hello Bluetooth powłoki:

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Uruchom następujące polecenie toopower na kontrolerze Bluetooth hello hello:

    ```bash
    power on
    ```

    Jeśli kontroler hello jest włączona, zostanie wyświetlony komunikat z **Zmienianie zasilania w zakończyło się pomyślnie**.

1. Uruchom powitania po tooscan polecenia dla w pobliżu urządzenia Bluetooth:

    ```bash
    scan on
    ```

1. Naciśnij przycisk zasilania hello znajdującego się na powitania Sensor tag toomake wykrywalny go. miga LED Hello zielony.

1. Po wyświetleniu komunikatu w powłoce hello tego kontrolera hello wykrył hello Sensor tag, zanotuj hello adres MAC urządzenia hello. wygląda Hello adres MAC **A0:E6:F8:B5:F6:00**. Należy adres MAC hello później w samouczku hello podczas konfigurowania bramy hello.

1. Uruchom hello następujące polecenia tooturn Wyłącz Bluetooth skanowania:

    ```bash
    scan off
    ```

1. Uruchom następujące polecenie tooverify, że możesz połączyć urządzeń Sensor tag toohello hello:

    ```bash
    connect <SensorTag MAC address>
    ```

    Jeśli łączysz się pomyślnie, powłoka hello pokazuje wiadomość hello **połączenie przebiegło pomyślnie** i wyświetla informacje o urządzeniu Sensor tag hello. Jeśli nie można połączyć, sprawdź powitalne Sensor tag jest nadal włączony.

1. Teraz można odłączyć od hello Sensor tag i zakończyć hello Bluetooth powłoki, uruchamiając następujące polecenia hello:

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a>Utworzenie niestandardowego modułu krawędzi IoT hello

Teraz można tworzyć hello niestandardowych krawędzi IoT moduł, który umożliwia hello bramy toosend wiadomości toohello zdalnego rozwiązanie monitorowania. Aby uzyskać więcej informacji dotyczących konfigurowania bramy i moduły krawędzi IoT, zobacz [pojęcia dotyczące usługi Azure IoT krawędzi][lnk-gateway-concepts].

Pobierz kod źródłowy hello hello niestandardowe moduły krawędzi IoT z serwisu GitHub, za pomocą następującego polecenia hello:

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

Utworzenie niestandardowego modułu krawędzi IoT hello, za pomocą następującego polecenia hello:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

skrypt kompilacji Hello umieszcza niestandardowego modułu krawędzi IoT hello libsensor2remotemonitoring.so w folderze kompilacji hello.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>Konfigurowanie i uruchamianie hello brama brzegowa IoT

Można teraz skonfigurować hello telemetrii toosend bramy krawędzi IoT z Twojej tooyour urządzeń Sensor tag zdalny pulpit nawigacyjny monitorowania. Aby uzyskać więcej informacji dotyczących konfigurowania bramy i moduły krawędzi IoT, zobacz [pojęcia dotyczące usługi Azure IoT krawędzi][lnk-gateway-concepts].

> [!TIP]
> W tym samouczku użyjesz hello standard `vi` Edytor tekstu na powitania Intel NUC. Jeśli nie używasz `vi` przed, należy wykonać Samouczek wprowadzający, takich jak [Unix — Witaj vi samouczek edytora] [ lnk-vi-tutorial] toofamiliarize sobie z tego edytora. Alternatywnie możesz zainstalować hello użytkownikom większy komfort [nano](https://www.nano-editor.org/) edytora za pomocą polecenia hello `smart install nano -y`.

Otwórz hello przykładowy plik konfiguracyjny w hello **vi** Edytor przy użyciu hello następujące polecenie:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

Znajdź hello następujące wiersze w konfiguracji hello modułu Centrum IoTHub hello:

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

Zastąp symbol zastępczy hello wartości z Centrum IoT informacji utworzony i zapisany pod hello hello start tego samouczka. wartość Hello IoTHubName wygląda jak **yourrmsolution37e08**, i wartość hello IoTSuffix jest zwykle **azure devices.net**.

Znajdź hello następujące wiersze w konfiguracji hello modułu mapowania hello:

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

Zastąp hello **macAddress** symbol zastępczy hello adres MAC z Sensor tag zanotowany wcześniej. Zastąp hello **deviceID** i **deviceKey** symbole zastępcze z identyfikatorów hello i klucze dla urządzeń hello dwa wcześniej utworzony w hello zdalnego rozwiązanie monitorowania.

Znajdź hello następujące wiersze w konfiguracji hello modułu Sensor tag hello:

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

Zastąp hello **urządzenia\_mac\_adres** symbol zastępczy hello adres MAC z Sensor tag zanotowany wcześniej.

Zapisz zmiany.

Teraz możesz uruchomić bramy hello przy użyciu hello następującego polecenia:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

Witaj brama brzegowa IoT rozpoczyna się hello Intel NUC i wysyła dane telemetryczne z hello Sensor tag toohello zdalnego rozwiązanie monitorowania:

![Brama brzegowa IoT wysyła dane telemetryczne z hello Sensor tag][img-telemetry]

Naciśnij klawisz **Ctrl-C** tooexit hello program w dowolnym momencie.

## <a name="view-hello-telemetry"></a>Dane telemetryczne wyświetleń hello

Brama Hello teraz wysyła dane telemetryczne z hello zdalnego rozwiązanie monitorowania Sensor tag urządzenia toohello. Można wyświetlić dane telemetryczne hello na pulpicie nawigacyjnym rozwiązania hello. Można również wysłać polecenia tooyour Sensor tag urządzenia za pośrednictwem bramy hello z pulpitu nawigacyjnego rozwiązania hello.

- Przejdź toohello pulpit nawigacyjny rozwiązania.
- Wybierz hello urządzenia skonfigurowane w hello bramy, która reprezentuje hello Sensor tag w hello **tooView urządzenia** listy rozwijanej.
- Wyświetla Hello telemetrię z urządzeń Sensor tag hello na powitania pulpitu nawigacyjnego.

![Wyświetl dane telemetryczne z urządzeń Sensor tag hello][img-telemetry-display]

> [!WARNING]
> Pozostawienie zdalne monitorowanie działającej na koncie Azure hello są rozliczane na powitania jego uruchomieniu. Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config]. Usuń hello wstępnie skonfigurowane rozwiązanie z konta platformy Azure po zakończeniu korzystania z niego.


## <a name="next-steps"></a>Następne kroki

Odwiedź hello [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started