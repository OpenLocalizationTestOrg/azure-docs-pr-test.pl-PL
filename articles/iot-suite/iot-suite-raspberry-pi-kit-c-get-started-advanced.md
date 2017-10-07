---
title: "Aktualizuje pakiet IoT przy użyciu oprogramowania układowego toosupport C aaaConnect tooAzure Pi malina | Dokumentacja firmy Microsoft"
description: "Użyj hello Microsoft Azure IoT Starter Kit dla hello malina Pi 3 i pakiet IoT Azure. Użyj C tooconnect Twojego toohello Pi malina zdalne monitorowanie rozwiązania, wysyłania danych telemetrycznych z czujników chmury toohello i przeprowadzić aktualizację oprogramowania układowego zdalnego."
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
ms.openlocfilehash: 36d39c6d754ddb025fd3f6b74d7795ed907b754c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a>Połącz z toohello malina Pi 3 zdalne monitorowanie rozwiązania i Włącz aktualizacje oprogramowania układowego zdalnego za pomocą C

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Ten samouczek pokazuje, jak toouse hello Microsoft Azure IoT Starter Kit dla 3 Pi malina do:

* Opracowywanie czytnik temperatury i wilgotności, który może komunikować się z chmurą hello.
* Włącz i wykonywanie aplikacji klienckiej hello tooupdate aktualizacji oprogramowania układowego zdalnego na powitania malina Pi.

samouczku Hello:

* Raspbian systemu operacyjnego, język programowania hello C i hello zestawu SDK usługi Microsoft Azure IoT dla C tooimplement urządzenia próbki.
* monitorowania zdalnego pakiet IoT Hello wstępnie skonfigurowane rozwiązanie jako hello oparte na chmurze zaplecza.

## <a name="overview"></a>Omówienie

W tym samouczku można wykonać hello następujące kroki:

* Wdróż wystąpienie wstępnie skonfigurowane rozwiązanie tooyour subskrypcji platformy Azure hello zdalnego monitorowania. Ten krok automatycznie wdraża i konfiguruje wiele usług platformy Azure.
* Konfigurowanie sieci toocommunicate czujników i urządzeń do komputera i hello zdalne monitorowanie rozwiązania.
* Zaktualizuj hello próbki urządzenia kod tooconnect toohello zdalnego rozwiązanie monitorowania i wysłać dane telemetryczne, które można wyświetlić na pulpicie nawigacyjnym rozwiązania hello.
* Używanie aplikacji klient hello tooupdate kodu hello próbki urządzenia.

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Witaj zdalnego monitorowania przepisów rozwiązania zbiór usług platformy Azure w ramach subskrypcji platformy Azure. wdrożenie Hello odzwierciedla architektury przedsiębiorstwa prawdziwe. tooavoid opłat niepotrzebnych wykorzystania platformy Azure, usunąć wystąpienie usługi hello wstępnie skonfigurowane rozwiązanie azureiotsuite.com po zakończeniu z nim. Jeśli należy ponownie hello wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć. Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a>Pobierz i skonfiguruj hello próbki

Można teraz pobrać i skonfigurować aplikację klienta monitorowania zdalnego hello na Twoje Pi malina.

### <a name="clone-hello-repositories"></a>Repozytoria hello w klonowania

Jeśli jeszcze tego nie zrobiono tego wcześniej, hello w klonowania wymagane hello repozytoriów, uruchamiając następujące polecenia na Twoje Pi:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Zaktualizuj parametry połączenia urządzenia hello

Otwórz hello przykładowy plik konfiguracyjny w hello **nano** Edytor przy użyciu hello następujące polecenie:

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

Zastąp symbole zastępcze hello hello identyfikator i Centrum IoT informacji o urządzeniu utworzony i zapisany pod hello na początku tego samouczka.

Gdy wszystko będzie gotowe, hello zawartość pliku deviceinfo hello powinna wyglądać hello poniższy przykład:

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

Zapisz zmiany (**Ctrl-O**, **Enter**) i zamknij Edytor hello (**Ctrl-X**).

## <a name="build-hello-sample"></a>Przykład Witaj kompilacji

Jeśli nie zostało to jeszcze zrobione, należy zainstalować hello wymagań wstępnych pakietów hello zestawu SDK usługi Microsoft Azure IoT urządzenia dla języka C, uruchamiając następujące polecenia w terminalu na powitania Pi malina hello:

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

Można teraz tworzyć hello przykładowe rozwiązanie na powitania Pi malina:

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

Teraz możesz uruchomić program przykładowy hello na powitania malina Pi. Wprowadź polecenie hello:

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

Witaj następujące przykładowe dane wyjściowe jest przykład danych wyjściowych hello, dostępne w wierszu polecenia hello na powitania Pi malina:

![Dane wyjściowe z aplikacji malinowe Pi][img-raspberry-output]

Naciśnij klawisz **Ctrl-C** tooexit hello program w dowolnym momencie.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. Na pulpicie nawigacyjnym rozwiązania hello, kliknij przycisk **urządzeń** toovisit hello **urządzeń** strony. Wybierz użytkownika Pi malina hello **listę urządzeń**. Następnie wybierz pozycję **metody**:

    ![Lista urządzeń na pulpicie nawigacyjnym][img-list-devices]

1. Na powitania **wywołania metody** wybierz pozycję **InitiateFirmwareUpdate** w hello **metody** listy rozwijanej.

1. W hello **FWPackageURI** wprowadź **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**. Ten plik archiwum zawiera hello implementacji oprogramowania układowego hello w wersji 2.0.

1. Wybierz **InvokeMethod**. Aplikacja Hello na powitania Pi malina wysyła pulpit nawigacyjny potwierdzenia wstecz toohello rozwiązania. Następnie uruchamia proces aktualizacji oprogramowania układowego hello pobierając hello nowej wersji oprogramowania układowego hello:

    ![Pokaż historię — metoda][img-method-history]

## <a name="observe-hello-firmware-update-process"></a>Obserwowanie procesu aktualizacji oprogramowania układowego hello

Można obserwować procesu aktualizacji oprogramowania układowego hello podczas jego działania na urządzeniu hello i wyświetlając hello zgłosił właściwości na pulpicie nawigacyjnym rozwiązania hello:

1. Można wyświetlić postęp hello w proces aktualizacji hello na powitania Pi malina:

    ![Pokaż postęp aktualizacji][img-update-progress]

    > [!NOTE]
    > Witaj zdalnego monitorowania ponownych uruchomień aplikacji dyskretnie po zakończeniu aktualizacji hello. Użyj polecenia hello `ps -ef` tooverify jest uruchomiona. Proces hello tooterminate, należy użyć hello `kill` polecenia o identyfikatorze hello.

1. Można wyświetlić stan hello hello aktualizacji oprogramowania układowego, zgłoszonych przez urządzenia hello, w portalu rozwiązania hello. Witaj Poniższy zrzut ekranu przedstawia stan hello i czas trwania każdego etapu procesu aktualizacji hello i nowa wersja oprogramowania układowego hello:

    ![Pokaż stan zadania][img-job-status]

    Jeśli Przejdź wstecz toohello pulpitu nawigacyjnego, możesz sprawdzić, czy urządzenie hello nadal wysyła dane telemetryczne po aktualizacji oprogramowania układowego hello.

> [!WARNING]
> Pozostawienie zdalne monitorowanie działającej na koncie Azure hello są rozliczane na powitania jego uruchomieniu. Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config]. Usuń hello wstępnie skonfigurowane rozwiązanie z konta platformy Azure po zakończeniu korzystania z niego.

## <a name="next-steps"></a>Następne kroki

Odwiedź hello [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md