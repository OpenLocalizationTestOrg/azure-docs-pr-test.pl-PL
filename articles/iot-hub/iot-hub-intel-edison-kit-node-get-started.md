---
title: "aaaIntel Edison toocloud (Node.js) - Połącz Edison Intel tooAzure Centrum IoT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup i połącz Intel Edison tooAzure Centrum IoT platformy Intel Edison toosend danych toohello chmury Azure w tym samouczku."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Usługa Azure iot intel edison, intel edison Centrum iot, intel edison wysyłania danych toocloud, intel edison toocloud"
ms.assetid: a7c9cf2d-c102-41b0-aa45-41285c6877eb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/15/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfc3387efc532b4b83f0626a9cf61d12c2952af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-nodejs"></a>Połącz tooAzure Intel Edison Centrum IoT (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

W tym samouczku Rozpocznij od uczenia hello podstawowe informacje dotyczące pracy z Intel Edison. Następnie dowiesz się, jak połączyć tooseamlessly chmury toohello urządzeń przy użyciu [Centrum IoT Azure](iot-hub-what-is-iot-hub.md).

Nie masz jeszcze zestawu? Uruchom [tutaj](https://azure.microsoft.com/develop/iot/starter-kits)

## <a name="what-you-do"></a>Co zrobić

* Konfiguracja Intel Edison i i Grove modułów.
* Tworzenie Centrum IoT.
* Zarejestruj urządzenie dla Edison w Centrum IoT.
* Uruchom przykładową aplikację w Centrum IoT tooyour danych czujnika Edison toosend.

Połącz Centrum IoT tooan Edison firmy Intel, który utworzono. Następnie możesz uruchomić przykładową aplikację na Edison toocollect temperatury i wilgotności danych z czujnika temperatury Grove. Ponadto możesz wysłać Centrum IoT tooyour danych czujnika hello.

## <a name="what-you-learn"></a>Omawiane zagadnienia

* Jak toocreate Centrum Azure IoT i uzyskać nowy ciąg połączenia urządzenia.
* Jak tooconnect Edison z czujnika temperatury Grove.
* Jak toocollect dane czujników, uruchamiając na Edison przykładowej aplikacji.
* Jak Centrum IoT tooyour danych czujnika toosend.

## <a name="what-you-need"></a>Co jest potrzebne

![Co jest potrzebne](media/iot-hub-intel-edison-kit-node-get-started/0_kit.png)

* Witaj Intel Edison tablicy
* Karty rozszerzeń Arduino
* Aktywna subskrypcja platformy Azure. Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.
* Mac lub komputer z systemem Windows lub Linux.
* Połączenie internetowe.
* TooType Micro B kabla A USB
* Zasilacz prądu (DC). Zasilacza powinny być sklasyfikowane w następujący sposób:
  - 7-15V KONTROLERA DOMENY
  - Co najmniej 1500mA
  - numer pin center/wewnętrzny Hello powinna być bieguna dodatnie hello hello zasilania

Witaj, następujące elementy są opcjonalne:

* Grove podstawowej tarczy V2
* Grove - czujnik temperatury
* Grove kabel
* Paski rozdzielacza lub śruby zawarte w pakiecie hello, w tym cztery zestawy śruby i tworzywa odstępników i dwie śruby toofasten hello modułu toohello rozszerzenia tablicy.

> [!NOTE] 
Te elementy są opcjonalne, ponieważ obsługa przykładowy kod hello symulowane danych czujnika.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a>Instalator Edison Intel

### <a name="assemble-your-board"></a>Złóż tablicy

Ta sekcja zawiera kroki tooattach Intel® Edison modułu tooyour rozszerzenia tablicy.

1. Umieść hello Intel® Edison modułu w ramach konspektu hello białe na tablicy rozszerzenia, wyrównywanie hello luk w hello module z śruby hello na powitania rozszerzenia tablicy.

2. Naciśnij modułu hello poniżej słowa hello `What will you make?` dopóki uważasz, że bardzo proste.

   ![Złóż tablicy 2](media/iot-hub-intel-edison-kit-node-get-started/1_assemble_board2.jpg)

3. Użyj karty rozszerzeń toohello hello dwa szesnastkowych poziomie NTS (zawarte w pakiecie hello) toosecure hello modułu.

   ![Złóż tablicy 3](media/iot-hub-intel-edison-kit-node-get-started/2_assemble_board3.jpg)

4. Wstaw śruby w jednej z czterech luk rogu hello na powitania rozszerzenia tablicy. Skręcenie i zwiększyć jedną hello białe plastikowe odstępników na powitania gwintowanym.

   ![Złóż tablicy 4](media/iot-hub-intel-edison-kit-node-get-started/3_assemble_board4.jpg)

5. Powtórz te czynności dla hello innych odstępników trzy rogu.

   ![Złóż tablicy 5](media/iot-hub-intel-edison-kit-node-get-started/4_assemble_board5.jpg)

Teraz budowy tablicy.

   ![złożony tablicy](media/iot-hub-intel-edison-kit-node-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a>Połącz hello tarczy Base Grove i hello czujnik temperatury

1. Umieść hello Grove Base tarczy na tooyour tablicy. Upewnij się, że wszystkie numery PIN ściśle są podłączone do tablicy.
   
   ![Podstawowy tarczy Grove](media/iot-hub-intel-edison-kit-node-get-started/6_grove_base_sheild.jpg)

2. Czujnik temperatury Użyj Grove kabel tooconnect Grove na powitania Grove Base tarczy **A0** portu.

   ![Połącz czujnik tootemperature](media/iot-hub-intel-edison-kit-node-get-started/7_temperature_sensor.jpg)

   ![Edison i czujnik połączenia](media/iot-hub-intel-edison-kit-node-get-started/16_edion_sensor.png)

Teraz z czujnika jest gotowa.

### <a name="power-up-edison"></a>Włącz Edison

1. Dołącz hello zasilania.

   ![Podłącz zasilacz](media/iot-hub-intel-edison-kit-node-get-started/8_plug_power.jpg)

2. Zielona LED (oznaczony DS1 na powitania karty rozszerzeń Arduino *) powinien podświetlony i pozostać podświetlone.

3. Poczekaj na jedną minutę na powitania tablicy toofinish rozruch.

   > [!NOTE]
   > Jeśli nie masz zasilacz kontrolera domeny, można nadal zasilania hello tablicy za pośrednictwem portu USB. Zobacz `Connect Edison tooyour computer` sekcji, aby uzyskać szczegółowe informacje. Włączanie tablicy w ten sposób może spowodować nieprzewidywalne zachowanie z tablicy, szczególnie w przypadku, gdy przy użyciu sieci Wi-Fi lub zwiększają motors.

### <a name="connect-edison-tooyour-computer"></a>Podłącz komputer tooyour Edison

1. Przełącz dół mikroprzełącznika hello kierunku Witaj dwie micro portów USB, dzięki czemu Edison jest w trybie urządzenia. Różnice między trybu urządzenia ani hosta, odwołanie [tutaj](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).

   ![Przełącz mikroprzełącznika hello w dół](media/iot-hub-intel-edison-kit-node-get-started/9_toggle_down_microswitch.jpg)

2. Podłącz kabel USB micro hello do portu USB micro najwyższego hello.

   ![Górny micro portu USB](media/iot-hub-intel-edison-kit-node-get-started/10_top_usbport.jpg)

3. Plug hello drugiej, kabel USB do komputera.

   ![Komputer USB](media/iot-hub-intel-edison-kit-node-get-started/11_computer_usb.jpg)

4. Będzie wiadomo, że tablicy jest w pełni zainicjowany, gdy komputer instaluje nowy dysk (podobne jak w przypadku Wstawianie karta SD do komputera).

## <a name="download-and-run-hello-configuration-tool"></a>Pobierz i uruchom narzędzie konfiguracji hello
Pobierz najnowsze narzędzia konfiguracji hello z [to łącze](https://software.intel.com/en-us/iot/hardware/edison/downloads) kategorii hello `Installers` nagłówka. Wykonaj hello narzędzia i postępuj zgodnie z jego na ekranie instrukcjami, klikając przycisk Dalej, w razie potrzeby

### <a name="flash-firmware"></a>Oprogramowanie układowe Flash
1. Na powitania `Set up options` kliknij `Flash Firmware`.
2. Wybierz hello tooflash obrazu na tablicy, wykonując jedną z następujących hello:
   - toodownload i flash tablicy o hello najnowszego oprogramowania układowego obraz dostępne z firmy Intel, wybierz `Download hello latest image version xxxx`.
   - Wybierz tablicy z obrazem, który został zapisany już na komputerze, tooflash `Select hello local image`. Przeglądaj tooand hello wybierz obraz ma tooflash tooyour tablicy.
3. Narzędzie Instalatora Hello podejmie tooflash tablicy. cały proces miga Hello może trwać too10 minut.

### <a name="set-password"></a>Ustaw hasło
1. Na powitania `Set up options` kliknij `Enable Security`.
2. Można ustawić niestandardową nazwę tablicy Intel® Edison. Jest to opcjonalne.
3. Wpisz hasło do tablicy, a następnie kliknij przycisk `Set password`.
4. Oznacz hello hasła, które jest później używany w dół.

### <a name="connect-wi-fi"></a>Połączenia sieci Wi-Fi
1. Na powitania `Set up options` kliknij `Connect Wi-Fi`. Poczekaj zapasowej minutę tooone jako użytkownika skanowania komputera dostępnych sieci Wi-Fi.
2. Z hello `Detected Networks` listy rozwijanej wybierz sieci.
3. Z hello `Security` listy rozwijanej, wybierz hello sieci typu zabezpieczeń.
4. Udostępnić informacje logowania i hasło, a następnie kliknij przycisk `Configure Wi-Fi`.
5. Oznacz dół hello adres IP, który jest później używany.

> [!NOTE]
> Upewnij się, że Edison jest połączonych toohello sam sieci jako komputera. Komputer łączy tooyour Edison przy użyciu adresu IP hello.

   ![Połącz czujnik tootemperature](media/iot-hub-intel-edison-kit-node-get-started/12_configuration_tool.png)

Gratulacje! Pomyślnie skonfigurowano Edison.

## <a name="run-a-sample-application-on-intel-edison"></a>Uruchom przykładową aplikację na Intel Edison

### <a name="prepare-hello-azure-iot-device-sdk"></a>Przygotowanie hello SDK urządzenia IoT Azure

1. Użyj jednej z poniższych klientów SSH z tooyour tooconnect Twojego hosta komputera Intel Edison hello. adres IP Hello jest z narzędzia do konfiguracji hello oraz hasło hello jest hello jedną ustawione w tym narzędziu.
    - [PuTTY](http://www.putty.org/) dla systemu Windows.
    - Witaj wbudowanego klienta SSH Ubuntu lub macOS.

2. Klonowanie hello przykładowej aplikacji tooyour urządzenia klienckiego. 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-intel-edison-client-app
   ```

3. Następnie przejdź toohello repozytorium folder toorun hello następujące polecenia tooinstall wszystkich pakietów, może upłynąć lek zagrażający toocomplete minut.
   
   ```bash
   cd iot-hub-node-intel-edison-client-app
   npm install
   ```


### <a name="configure-and-run-hello-sample-application"></a>Konfigurowanie i uruchamianie hello przykładowej aplikacji

1. Otwórz plik konfiguracji hello, uruchamiając następujące polecenia hello:

   ```bash
   nano config.json
   ```

   ![Plik konfiguracji](media/iot-hub-intel-edison-kit-node-get-started/13_configure_file.png)

   Istnieją dwa makra w tym pliku mogą configurate. Witaj najpierw jest `INTERVAL`, który definiuje dwa komunikaty, które wysyłają toocloud hello interwału. Witaj drugi `simulatedData`, czyli wartość logiczną parametru czy toouse symulowane dane czujników, czy nie.

   Jeśli użytkownik **nie ma czujnik hello**Ustaw hello `simulatedData` wartość zbyt`true` toomake hello przykładowej aplikacji tworzenia i używania danych czujnika symulowane.

1. Zapisz i zamknij naciskając formantu O > Enter > Control X.


1. Uruchom aplikację przykładową hello, uruchamiając następujące polecenie hello:

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Upewnij się, możesz kopiowania i wklejania ciąg połączenia urządzenia hello w apostrofy hello.

Powinien pojawić się następujące hello output, że pokazuje hello wiadomości powitania i danych czujnika, które są wysyłane tooyour Centrum IoT.

![Dane wyjściowe — dane czujników wysyłane z Centrum IoT tooyour Intel Edison](media/iot-hub-intel-edison-kit-node-get-started/15_message_sent.png)

## <a name="next-steps"></a>Następne kroki

Uruchomiono przykładowych danych czujnika toocollect aplikacji i wysyłać je tooyour Centrum IoT.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
