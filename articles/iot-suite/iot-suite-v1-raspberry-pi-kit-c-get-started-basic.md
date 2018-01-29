---
title: "Pi malina nawiązać połączenie za pomocą C z czujników rzeczywistych pakiet IoT Azure | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Microsoft Azure IoT Starter Kit malinowe pi 3 i pakiet Azure IoT. Użyj C do nawiązania połączenia zdalnego rozwiązanie monitorowania sieci Pi malina wysłać dane telemetryczne z czujników w chmurze i Odpowiedz na metody wywoływane z poziomu pulpitu nawigacyjnego rozwiązania."
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
ms.date: 11/02/2017
ms.author: dobett
ms.openlocfilehash: 635eb9d4e85eaf43dc83f2bd5a0d0f7c32620d98
ms.sourcegitcommit: 295ec94e3332d3e0a8704c1b848913672f7467c8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/06/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a>Twoje malina Pi 3 nawiązać połączenie zdalne rozwiązanie monitorowania i wysyłania danych telemetrycznych z czujnika rzeczywistych za pomocą C

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-selector](../../includes/iot-suite-v1-raspberry-pi-kit-selector.md)]

W tym samouczku przedstawiono sposób Microsoft Azure IoT startowy do malina Pi 3 umożliwia tworzenie czytnik temperatury i wilgotności, który może komunikować się z chmurą. W samouczku:

- Raspbian systemu operacyjnego, język programowania C i Microsoft Azure IoT SDK dla języka C do zaimplementowania urządzenia próbki.
- Pakiet IoT zdalne monitorowanie wstępnie skonfigurowane rozwiązanie jako zaplecza opartej na chmurze.

## <a name="overview"></a>Omówienie

W tym samouczku zostaną wykonane następujące kroki:

- Wdrożenie wystąpienia programu zdalnego wstępnie skonfigurowane rozwiązanie monitorowania do subskrypcji platformy Azure. Ten krok automatycznie wdraża i konfiguruje wiele usług platformy Azure.
- Konfigurowanie czujniki i urządzenia do komunikowania się z komputerem i zdalnego rozwiązanie monitorowania.
- Zaktualizuj przykładowy kod urządzenia do nawiązania połączenia zdalnego rozwiązanie monitorowania i wysłać dane telemetryczne, które można wyświetlić na pulpicie nawigacyjnym rozwiązania.

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-prerequisites](../../includes/iot-suite-v1-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-v1-provision-remote-monitoring](../../includes/iot-suite-v1-provision-remote-monitoring.md)]

> [!WARNING]
> Zdalne rozwiązanie monitorowania udostępnia zestaw usług platformy Azure w ramach subskrypcji platformy Azure. Wdrożenie odzwierciedla architektury przedsiębiorstwa prawdziwe. Aby uniknąć niepotrzebnych wykorzystania platformy Azure, opłat, należy usunąć wystąpienia wstępnie skonfigurowanego rozwiązania na azureiotsuite.com po zakończeniu z nim. Jeśli potrzebujesz ponownie wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć. Aby uzyskać więcej informacji na temat zmniejszenie zużycia podczas wykonywania zdalnego rozwiązanie monitorowania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-solution](../../includes/iot-suite-v1-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-v1-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a>Pobierz i skonfiguruj próbki

Można teraz pobrać i konfigurowania zdalnego monitorowania aplikacji klienckiej na Twoje malina Pi.

### <a name="clone-the-repositories"></a>Klonowanie repozytoria

Jeśli jeszcze tego nie zrobiono, klonowanie wymagane repozytoriów, uruchamiając następujące polecenia w terminalu na Twoje Pi:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-the-device-connection-string"></a>Zaktualizuj parametry połączenia urządzenia

Otwieranie przykładowego pliku źródłowego w **nano** edytora za pomocą następującego polecenia:

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
```

Znajdź następujące wiersze:

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

Zastąp symbole zastępcze urządzenia i Centrum IoT informacji utworzony i zapisany na początku tego samouczka. Zapisz zmiany (**Ctrl-O**, **Enter**) i zamknij Edytor (**Ctrl-X**).

## <a name="build-the-sample"></a>Tworzyć przykładowy kod

Zainstaluj wstępnie wymagane pakiety dla Microsoft Azure IoT urządzenia SDK dla języka C, uruchamiając następujące polecenia w terminalu na Pi malina:

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

Można teraz tworzyć zaktualizowane przykładowe rozwiązanie na Pi malina:

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

Teraz możesz uruchomić program przykładowy na malina Pi. Wprowadź polecenie:

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

Następujące przykładowe dane wyjściowe jest przykład danych wyjściowych, widocznej na Pi malina w wierszu polecenia:

![Dane wyjściowe z aplikacji malinowe Pi][img-raspberry-output]

Naciśnij klawisz **Ctrl-C** aby zamknąć program w dowolnym momencie.

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-v1-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a>Następne kroki

Odwiedź stronę [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.

[img-raspberry-output]: ./media/iot-suite-v1-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
