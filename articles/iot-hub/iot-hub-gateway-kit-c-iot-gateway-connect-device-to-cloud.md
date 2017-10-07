---
title: "aaaUse tooconnect bramy IoT tooAzure urządzenia IoT Hub | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse NUC Intel jako tooconnect bramy IoT Sensor tag analizy czasowej i tooAzure danych czujnika wysyłania Centrum IoT w hello chmury."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Brama iot połączyć toocloud urządzenia"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a>Użyj IoT bramy tooconnect rzeczy toohello cloud - tooAzure Sensor tag Centrum IoT

> [!NOTE]
> Przed rozpoczęciem tego samouczka, upewnij się, przeprowadzisz [Konfigurowanie NUC Intel jako brama IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md). W [Konfigurowanie NUC Intel jako brama IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), konfigurowanie urządzenia Intel NUC hello jako bramę IoT.

## <a name="what-you-will-learn"></a>Co dowiesz się

Dowiesz się, jak toouse tooconnect bramy IoT tooAzure Sensor Texas Instruments tag (CC2650STK) Centrum IoT. Brama IoT Hello wysyła temperatury i wilgotności dane zbierane z hello Sensor tag tooAzure Centrum IoT.

## <a name="what-you-will-do"></a>Będzie wykonywać

- Tworzenie Centrum IoT.
- Zarejestruj urządzenie w Centrum IoT hello hello Sensor tag.
- Włącz hello połączenie między bramą IoT hello i hello Sensor tag.
- Uruchom cz przykładowej aplikacji toosend Sensor tag danych tooyour Centrum IoT.

## <a name="what-you-need"></a>Co jest potrzebne

- Samouczek [Konfigurowanie NUC Intel jako brama IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) zakończone, w której skonfigurowaniu NUC Intel jako brama IoT.
- * Aktywna subskrypcja platformy Azure. Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.
- Klient SSH, który jest uruchamiany na komputerze hosta. PuTTY jest zalecane w systemie Windows. Linux i macOS już dostarczane za pomocą klienta SSH.
- adres IP Hello i hello nazwy użytkownika i hasła tooaccess hello bramy z powitania klienta SSH.
- Połączenie internetowe.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> Tutaj możesz zarejestrować to nowe urządzenie dla użytkownika Sensor tag

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a>Włącz hello połączenie między bramą IoT hello i hello Sensor tag

W tej sekcji należy wykonać następujące zadania hello:

- Pobierz adres MAC hello hello Sensor tag dla połączenia Bluetooth.
- Inicjowanie połączenia Bluetooth z hello IoT bramy toohello Sensor tag.

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a>Pobierz adres MAC hello hello Sensor tag połączenia Bluetooth

1. Na komputerze hosta hello Uruchom klienta SSH hello i połącz toohello IoT bramy.
1. Odblokuj Bluetooth, uruchamiając następujące polecenie hello:

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. Uruchom usługę Bluetooth hello na powitania IoT bramy, a następnie wprowadź tooconfigure powłoki Bluetooth, hello Bluetooth, uruchamiając następujące polecenia:

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. Włącz hello Bluetooth kontrolera, uruchamiając hello następujące polecenia na powitania powłoki Bluetooth:

   ```bash
   power on
   ```

   ![Włącz hello kontrolera Bluetooth na powitania IoT bramy z bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. Uruchom skanowanie w poszukiwaniu w pobliżu urządzenia Bluetooth, uruchamiając następujące polecenie hello:

   ```bash
   scan on
   ```

   ![Skanowanie w pobliżu urządzenia Bluetooth z bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. Naciśnij klawisz hello parowanie przycisk na powitania Sensor tag. zielony Hello PRZEPROWADZONY na powitania błysków Sensor tag.
1. Na powitania powłoki Bluetooth powinna zostać wyświetlona hello znalezionych Sensor tag. Zanotuj hello adres MAC hello Sensor tag. W tym przykładzie hello hello Sensor tag adresu MAC jest `24:71:89:C0:7F:82`.
1. Wyłącz skanowanie hello, uruchamiając następujące polecenie hello:

   ```bash
   scan off
   ```

   ![Zatrzymuje skanowanie w pobliżu urządzenia Bluetooth z bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a>Inicjowanie połączenia Bluetooth z hello IoT bramy toohello Sensor tag

1. Połącz toohello Sensor tag, uruchamiając następujące polecenie hello:

   ```bash
   connect <MAC address>
   ```

   ![Połącz z bluetoothctl toohello Sensor tag](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. Odłącz od hello Sensor tag, a następnie zakończyć hello Bluetooth powłoki, uruchamiając następujące polecenia hello:

   ```bash
   disconnect
   exit
   ```

   ![Odłącz od hello Sensor tag z bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

Pomyślnie włączono hello połączenie między hello Sensor tag i hello IoT bramy.

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a>Uruchom cz przykładowej aplikacji toosend Sensor tag danych tooyour Centrum IoT

Energii małej Bluetooth (cz) Przykładowa aplikacja Hello są udostępniane przez Azure IoT krawędzi. Witaj przykładowej aplikacji zbiera dane z połączenia cz i Wyślij Centrum IoT tooyou danych hello. toorun hello przykładowej aplikacji, musisz:

1. Skonfiguruj hello przykładowej aplikacji.
1. Uruchom hello Przykładowa aplikacja hello IoT bramy.

### <a name="configure-hello-sample-application"></a>Skonfiguruj hello przykładowej aplikacji

1. Folder przejdź toohello hello przykładowej aplikacji, uruchamiając następujące polecenie hello:

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. Otwórz plik konfiguracji hello, uruchamiając następujące polecenie hello:

   ```bash
   vi ble_gateway.json
   ```

1. W pliku konfiguracyjnym hello Wypełnij hello następujące wartości:

   **IoTHubName**: hello nazwę Centrum IoT.

   **IoTHubSuffix**: Pobierz IoTHubSuffix z hello klucz podstawowy ciąg połączenia urządzenia hello zanotowaną w dół. Upewnij się, możesz pobrać klucz podstawowy hello ciąg połączenia urządzenia hello, nie hello klucz podstawowy parametry połączenia Centrum IoT. klucz podstawowy Hello ciąg połączenia urządzenia hello jest w formacie hello `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.

   **Transport**: hello wartość domyślna to `amqp`. Ta wartość przedstawia hello protokołu podczas transpotation. Może to być `http`, `amqp`, lub `mqtt`.

   **macAddress**: hello adres MAC hello Sensor tag zanotowaną w dół.

   **deviceID**: identyfikator urządzenia hello, który został utworzony w Centrum IoT.

   **deviceKey**: hello klucz podstawowy ciąg połączenia urządzenia hello.

   ![Plik konfiguracji pełną hello hello cz przykładowej aplikacji](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. Naciśnij klawisz `ESC` i typ `:wq` toosave hello pliku.

### <a name="run-hello-sample-application"></a>Uruchom hello przykładowej aplikacji

1. Upewnij się, że powitalne Sensor tag jest włączona.
1. Uruchom następujące polecenie hello:

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>Następne kroki

[Użyj bramy IoT dla transformacji danych czujnika z krawędzią IoT Azure](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
