---
title: "Connect Raspberry pi (C) tooAzure IoT — Lekcja 1: Wdrażanie aplikacji | Dokumentacja firmy Microsoft"
description: "Klonowanie hello aplikacji przykładowej C z serwisu GitHub, a system gulp toodeploy tej tablicy tooyour malina Pi 3 aplikacji. Ta przykładowa aplikacja miga tablicy toohello LED połączone hello co dwie sekundy."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "pi malinowe doprowadziły migania, migania doprowadziły z malinowe pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e90c3360c4de1873313db19561c781eb21dbf1d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Tworzenie i wdrażanie aplikacji migania hello
## <a name="what-you-will-do"></a>Będzie wykonywać
Klonowanie hello przykładowej C aplikacji z usługi GitHub i użyj hello gulp narzędzie toodeploy hello przykładowej aplikacji tooRaspberry Pi 3. Witaj przykładowej aplikacji miga tablicy toohello LED połączone hello co dwie sekundy. Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:

* Jak toouse hello `device-discover-cli` tooretrieve narzędzie sieci informacji na temat Pi.
* Jak toodeploy i wykonywania hello przykładowej aplikacji na Pi.
* Jak toodeploy i debugowania aplikacji uruchamiany zdalnie na Pi.

## <a name="what-you-need"></a>Co jest potrzebne
Użytkownik pomyślnie ukończona hello następujące operacje:

* [Konfigurowanie urządzenia](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [Pobierz narzędzia hello](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a>Uzyskaj hello adresu IP i hosta nazwy pi
Otwórz wiersz polecenia w systemie Windows lub terminal macOS lub Ubuntu, a następnie uruchom następujące polecenie hello:

```bash
devdisco list --eth
```

Powinny pojawić się dane wyjściowe podobne toohello następujące czynności:

![Odnajdywanie urządzeń](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

Zwróć uwagę na powitania `IP address` i `hostname` pi. Należy w dalszej części tego artykułu.

> [!NOTE]
> Upewnij się, że Pi jest połączonych toohello sam sieci jako komputera. Na przykład, jeśli komputer jest połączony tooa sieci bezprzewodowej podczas Pi jest połączonych tooa ich z przewodową siecią, może nie być wyświetlana hello IP adres hello devdisco w danych wyjściowych.

## <a name="open-hello-sample-application"></a>Otwórz hello przykładowej aplikacji
Witaj tooopen przykładowej aplikacji, wykonaj następujące kroki:

1. Klonuj repozytorium przykładowej hello z serwisu GitHub, uruchamiając następujące polecenie hello:
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. Otwórz hello przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia hello:
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Struktura repozytorium](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

Witaj `main.c` pliku w hello `app` podfolder to plik klucza źródła hello, który zawiera hello kodu toocontrol hello LED.

### <a name="install-application-dependencies"></a>Zainstaluj zależności aplikacji
Zainstaluj hello bibliotek i inne moduły potrzebnych dla aplikacji przykładowej hello, uruchamiając następujące polecenie hello:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Skonfiguruj połączenie z urządzeniem hello
tooconfigure hello połączenie z urządzeniem, wykonaj następujące kroki:

1. Generowanie pliku konfiguracji urządzenia hello, uruchamiając następujące polecenie hello:
   
   ```bash
   gulp init
   ```
   
   plik konfiguracji Hello `config-raspberrypi.json` zawiera poświadczenia użytkownika hello używasz toolog tooPi. przeciek hello tooavoid poświadczeń użytkownika hello plik konfiguracji jest generowany w podfolderze hello `.iot-hub-getting-started` hello folderu macierzystego na tym komputerze.

2. Otwórz plik konfiguracji urządzenia hello w programie Visual Studio Code, uruchamiając następujące polecenie hello:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. Zastąp symbol zastępczy hello `[device hostname or IP address]` hello adres IP lub nazwa hosta hello uzyskano wcześniej w "Uzyskaj hello adresu IP i hosta nazwy pi."
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> Klucz SSH można użyć zamiast nazwy użytkownika i hasła podczas łączenia tooRaspberry Pi. W celu toodo to będzie miał użyciu klucza hello toogenerate **ssh-keygen** i **pi ssh kopiowania id @\<adres urządzenia\>**.
>
> W systemie Windows te polecenia są dostępne w **Git Bash**.
>
> Na MacOS należy toorun **brew zainstalować ssh kopiowania id**.
>
> Po pomyślnym przekazaniu klucza toohello hello Pi malina, Zastąp **device_password** z **device_key_path** właściwości w **config raspberrypi.json**.
>
> Wiersze zaktualizowane powinien wyglądać jak poniżej:
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

Gratulacje! Pomyślnie utworzono hello pierwszy przykładowej aplikacji Pi.

## <a name="deploy-and-run-hello-sample-application"></a>Wdrażanie i uruchamianie hello przykładowej aplikacji
### <a name="install-hello-azure-iot-hub-sdk-on-pi"></a>Zainstaluj zestaw SDK usługi Azure IoT Hub hello na Pi
Zainstaluj zestaw SDK usługi Azure IoT Hub hello na Pi, uruchamiając następujące polecenie hello:

```bash
gulp install-tools
```

To zadanie może potrwać kilka minut toocomplete hello zostanie uruchomiony po raz pierwszy.

### <a name="deploy-and-run-hello-sample-app"></a>Wdrażanie i uruchamianie hello przykładowej aplikacji
Wdrażanie i uruchamianie aplikacji przykładowej hello, uruchamiając następujące polecenie hello:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Weryfikowanie działania aplikacji hello
Witaj przykładowej aplikacji kończy się automatycznie po hello LED miga do 20 razy. Jeśli nie widzisz migający hello LED, zobacz hello [przewodnik rozwiązywania problemów](iot-hub-raspberry-pi-kit-c-troubleshooting.md) dla rozwiązania toocommon problemów.
![Migający LED](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)

## <a name="summary"></a>Podsumowanie
Zainstalowaniu hello wymagane narzędzia toowork z Pi i przykładowej aplikacji tooPi tooblink hello LED wdrożone. Można teraz tworzenie, wdrażanie i uruchom inną aplikację przykładową, która łączy Pi tooAzure toosend Centrum IoT i odbierania wiadomości.

## <a name="next-steps"></a>Następne kroki
[Pobierz narzędzia Azure](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

