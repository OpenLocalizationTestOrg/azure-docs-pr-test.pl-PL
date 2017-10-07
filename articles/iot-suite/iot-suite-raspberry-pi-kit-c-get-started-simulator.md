---
title: "aaaConnect tooAzure Pi malina pakiet IoT za pomocą C z symulowanego telemetrii | Dokumentacja firmy Microsoft"
description: "Użyj hello Microsoft Azure IoT Starter Kit dla hello malina Pi 3 i pakiet IoT Azure. Użyj C tooconnect Twojego toohello Pi malina zdalne monitorowanie rozwiązania, wysłać symulowanych telemetrii toohello chmury i odpowiadać toomethods wywoływane z pulpitu nawigacyjnego rozwiązania hello."
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
ms.openlocfilehash: 3c4fa43b381385d1a7896cada34aa3aa0b8e5fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-c"></a>Połącz z toohello malina Pi 3 zdalne monitorowanie rozwiązania i wysłać symulowanych dane telemetryczne za pomocą C

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Ten samouczek pokazuje, jak hello toouse malina Pi 3 toosimulate temperatury i wilgotności danych toosend toohello chmury. samouczku Hello:

- Raspbian systemu operacyjnego, język programowania hello C i hello zestawu SDK usługi Microsoft Azure IoT dla C tooimplement urządzenia próbki.
- monitorowania zdalnego pakiet IoT Hello wstępnie skonfigurowane rozwiązanie jako hello oparte na chmurze zaplecza.

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Witaj zdalnego monitorowania przepisów rozwiązania zbiór usług platformy Azure w ramach subskrypcji platformy Azure. wdrożenie Hello odzwierciedla architektury przedsiębiorstwa prawdziwe. tooavoid opłat niepotrzebnych wykorzystania platformy Azure, usunąć wystąpienie usługi hello wstępnie skonfigurowane rozwiązanie azureiotsuite.com po zakończeniu z nim. Jeśli należy ponownie hello wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć. Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a>Pobierz i skonfiguruj hello próbki

Można teraz pobrać i skonfigurować aplikację klienta monitorowania zdalnego hello na Twoje Pi malina.

### <a name="clone-hello-repositories"></a>Repozytoria hello w klonowania

Jeśli jeszcze tego nie zrobiono, hello w klonowania wymagane hello repozytoriów, uruchamiając następujące polecenia w terminalu na Twoje Pi:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Zaktualizuj parametry połączenia urządzenia hello

Otwórz hello pliku źródłowego próbki w hello **nano** edytora za pomocą następującego polecenia hello:

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/remote_monitoring/remote_monitoring.c
```

Znajdź hello następujące wiersze:

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

Zastąp symbole zastępcze hello hello urządzenia i Centrum IoT informacji utworzony i zapisany pod hello na początku tego samouczka. Zapisz zmiany (**Ctrl-O**, **Enter**) i zamknij Edytor hello (**Ctrl-X**).

## <a name="build-hello-sample"></a>Przykład Witaj kompilacji

Instalowanie wymagań wstępnych pakietów hello hello zestawu SDK usługi Microsoft Azure IoT urządzenia dla języka C, uruchamiając następujące polecenia w terminalu na powitania Pi malina hello:

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

Teraz można tworzyć hello zaktualizowane przykładowe rozwiązanie na powitania Pi malina:

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
```

Teraz możesz uruchomić program przykładowy hello na powitania malina Pi. Wprowadź polecenie hello:

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

Witaj następujące przykładowe dane wyjściowe jest przykład danych wyjściowych hello, dostępne w wierszu polecenia hello na powitania Pi malina:

![Dane wyjściowe z aplikacji malinowe Pi][img-raspberry-output]

Naciśnij klawisz **Ctrl-C** tooexit hello program w dowolnym momencie.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a>Następne kroki

Odwiedź hello [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-simulator/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
