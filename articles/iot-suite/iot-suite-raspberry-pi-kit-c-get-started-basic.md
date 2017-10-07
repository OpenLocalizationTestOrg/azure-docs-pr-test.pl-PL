---
title: "aaaConnect tooAzure Pi malina pakiet IoT z rzeczywistą czujników za pomocą C | Dokumentacja firmy Microsoft"
description: "Użyj hello Microsoft Azure IoT Starter Kit dla hello malina Pi 3 i pakiet IoT Azure. Użyj C tooconnect Twojego toohello Pi malina zdalne monitorowanie rozwiązania, wysyłania danych telemetrycznych z czujników chmury toohello i odpowiadać toomethods wywoływane z pulpitu nawigacyjnego rozwiązania hello."
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
ms.openlocfilehash: 7dac55ae5fde4c6f8e3ea6a7debf9a6822dc07ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a>Połącz z toohello malina Pi 3 zdalne monitorowanie rozwiązania i wysyłania danych telemetrycznych z czujnika rzeczywistych za pomocą C

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Ten samouczek pokazuje, jak toouse hello Microsoft Azure IoT Starter Kit dla toodevelop malina Pi 3 czytnik temperatury i wilgotności, który może komunikować się z chmurą hello. samouczku Hello:

- Raspbian systemu operacyjnego, język programowania hello C i hello zestawu SDK usługi Microsoft Azure IoT dla C tooimplement urządzenia próbki.
- monitorowania zdalnego pakiet IoT Hello wstępnie skonfigurowane rozwiązanie jako hello oparte na chmurze zaplecza.

## <a name="overview"></a>Omówienie

W tym samouczku można wykonać hello następujące kroki:

- Wdróż wystąpienie wstępnie skonfigurowane rozwiązanie tooyour subskrypcji platformy Azure hello zdalnego monitorowania. Ten krok automatycznie wdraża i konfiguruje wiele usług platformy Azure.
- Konfigurowanie sieci toocommunicate czujników i urządzeń do komputera i hello zdalne monitorowanie rozwiązania.
- Zaktualizuj hello próbki urządzenia kod tooconnect toohello zdalnego rozwiązanie monitorowania i wysłać dane telemetryczne, które można wyświetlić na pulpicie nawigacyjnym rozwiązania hello.

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Witaj zdalnego monitorowania przepisów rozwiązania zbiór usług platformy Azure w ramach subskrypcji platformy Azure. wdrożenie Hello odzwierciedla architektury przedsiębiorstwa prawdziwe. tooavoid opłat niepotrzebnych wykorzystania platformy Azure, usunąć wystąpienie usługi hello wstępnie skonfigurowane rozwiązanie azureiotsuite.com po zakończeniu z nim. Jeśli należy ponownie hello wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć. Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a>Pobierz i skonfiguruj hello próbki

Można teraz pobrać i skonfigurować aplikację klienta monitorowania zdalnego hello na Twoje Pi malina.

### <a name="clone-hello-repositories"></a>Repozytoria hello w klonowania

Jeśli jeszcze tego nie zrobiono, hello w klonowania wymagane hello repozytoriów, uruchamiając następujące polecenia w terminalu na Twoje Pi:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-hello-device-connection-string"></a>Zaktualizuj parametry połączenia urządzenia hello

Otwórz hello pliku źródłowego próbki w hello **nano** edytora za pomocą następującego polecenia hello:

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
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
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

Teraz możesz uruchomić program przykładowy hello na powitania malina Pi. Wprowadź polecenie hello:

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

Witaj następujące przykładowe dane wyjściowe jest przykład danych wyjściowych hello, dostępne w wierszu polecenia hello na powitania Pi malina:

![Dane wyjściowe z aplikacji malinowe Pi][img-raspberry-output]

Naciśnij klawisz **Ctrl-C** tooexit hello program w dowolnym momencie.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a>Następne kroki

Odwiedź hello [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
