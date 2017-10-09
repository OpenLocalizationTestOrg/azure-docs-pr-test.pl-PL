---
title: "aaaConnect tooAzure bramy pakiet IoT przy użyciu NUC Intel | Dokumentacja firmy Microsoft"
description: "Użyj hello IoT Microsoft komercyjnych Kit bramy i hello zdalnego wstępnie skonfigurowane rozwiązanie monitorowania. Użyj hello Azure IoT krawędzi bramy tooconnect toohello zdalnego rozwiązanie monitorowania, wysłać symulowanych telemetrii toohello chmury, a odpowiedź toomethods wywoływane z pulpitu nawigacyjnego rozwiązania hello."
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
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 46b545fc21b054191c8f78ace20fc628f839a819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a>Połącz Twoje toohello bramy Azure IoT krawędzi zdalne monitorowanie wstępnie skonfigurowane rozwiązanie i wysłać symulowanych telemetrii

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

Ten samouczek pokazuje, jak toouse Azure IoT krawędzi toosimulate temperatury i wilgotności danych toosend toohello monitorowania zdalnego wstępnie skonfigurowane rozwiązanie. samouczku Hello:

- Azure IoT krawędzi tooimplement bramy próbki.
- monitorowania zdalnego pakiet IoT Hello wstępnie skonfigurowane rozwiązanie jako hello oparte na chmurze zaplecza.

## <a name="overview"></a>Omówienie

W tym samouczku można wykonać hello następujące kroki:

- Wdróż wystąpienie wstępnie skonfigurowane rozwiązanie tooyour subskrypcji platformy Azure hello zdalnego monitorowania. Ten krok automatycznie wdraża i konfiguruje wiele usług platformy Azure.
- Konfigurowanie toocommunicate urządzenia bramy NUC firmy Intel, tak do komputera i hello zdalnego rozwiązanie monitorowania.
- Skonfiguruj hello dane telemetryczne, które można wyświetlić na pulpicie nawigacyjnym rozwiązania hello symulowane toosend bramy IoT krawędzi.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Witaj zdalnego monitorowania przepisów rozwiązania zbiór usług platformy Azure w ramach subskrypcji platformy Azure. wdrożenie Hello odzwierciedla architektury przedsiębiorstwa prawdziwe. tooavoid opłat niepotrzebnych wykorzystania platformy Azure, usunąć wystąpienie usługi hello wstępnie skonfigurowane rozwiązanie azureiotsuite.com po zakończeniu z nim. Jeśli należy ponownie hello wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć. Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

Powtórz poprzednie tooadd kroki hello drugiego urządzenia przy użyciu Identyfikatora urządzenia, takich jak **device02**. Przykładowe Hello wysyła dane z dwóch symulowanego urządzenia zdalnego rozwiązanie monitorowania hello bramy toohello.

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

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
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

skrypt kompilacji Hello umieszcza niestandardowego modułu krawędzi IoT hello libsimulator.so w folderze kompilacji hello.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>Konfigurowanie i uruchamianie hello brama brzegowa IoT

Można teraz skonfigurować hello krawędzi IoT bramy toosend symulowane telemetrii tooyour zdalnego pulpitu nawigacyjnego monitorowania. Aby uzyskać więcej informacji dotyczących konfigurowania bramy i moduły krawędzi IoT, zobacz [pojęcia dotyczące usługi Azure IoT krawędzi][lnk-gateway-concepts].

> [!TIP]
> W tym samouczku użyjesz hello standard `vi` Edytor tekstu na powitania Intel NUC. Jeśli nie używasz `vi` przed, należy wykonać Samouczek wprowadzający, takich jak [Unix — Witaj vi samouczek edytora] [ lnk-vi-tutorial] toofamiliarize sobie z tego edytora. Alternatywnie możesz zainstalować hello użytkownikom większy komfort [nano](https://www.nano-editor.org/) edytora za pomocą polecenia hello `smart install nano -y`.

Otwórz hello przykładowy plik konfiguracyjny w hello **vi** Edytor przy użyciu hello następujące polecenie:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
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
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

Zastąp hello **deviceID** i **deviceKey** symbole zastępcze z identyfikatorów hello i klucze dla urządzeń hello dwa wcześniej utworzony w hello zdalnego rozwiązanie monitorowania.

Zapisz zmiany.

Teraz możesz uruchomić powitalne brama brzegowa IoT przy użyciu hello następującego polecenia:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

Brama Hello rozpoczyna się na powitania Intel NUC i wysyła symulowane telemetrii toohello zdalnego rozwiązanie monitorowania:

![Brama brzegowa IoT generuje symulowane telemetrii][img-simulated telemetry]

Naciśnij klawisz **Ctrl-C** tooexit hello program w dowolnym momencie.

## <a name="view-hello-telemetry"></a>Dane telemetryczne wyświetleń hello

Witaj brama brzegowa IoT teraz wysyła symulowane telemetrii toohello zdalnego rozwiązanie monitorowania. Można wyświetlić dane telemetryczne hello na pulpicie nawigacyjnym rozwiązania hello.

- Przejdź toohello pulpit nawigacyjny rozwiązania.
- Wybierz jedno z urządzeń hello dwa skonfigurowane w hello bramy w hello **tooView urządzenia** listy rozwijanej.
- Wyświetla Hello telemetrię z urządzeń bramy hello na powitania pulpitu nawigacyjnego.

![Wyświetl dane telemetryczne z urządzenia bramy hello symulowane][img-telemetry-display]

> [!WARNING]
> Pozostawienie zdalne monitorowanie działającej na koncie Azure hello są rozliczane na powitania jego uruchomieniu. Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config]. Usuń hello wstępnie skonfigurowane rozwiązanie z konta platformy Azure po zakończeniu korzystania z niego.

## <a name="next-steps"></a>Następne kroki

Odwiedź hello [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started