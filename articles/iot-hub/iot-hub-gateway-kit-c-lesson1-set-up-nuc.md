---
title: "Urządzeń Sensor tag & Azure IoT bramy - Lekcja 1: Konfigurowanie Intel NUC | Dokumentacja firmy Microsoft"
description: "Ustawienie toowork Intel NUC jako bramy IoT między czujników i informacji z czujnika toocollect Centrum IoT Azure i wysyłać je tooIoT koncentratora."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: iot bramy intel nuc nuc komputera, DE3815TYKE
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Konfigurowanie Intel NUC jako brama IoT
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a>Będzie wykonywać

- Ustawienie Intel NUC jako bramę IoT.
- Zainstaluj pakiet Azure IoT krawędzi hello na powitania Intel NUC.
- Uruchom przykładową aplikację "hello_world" na powitania funkcjonalność bramy hello tooverify Intel NUC.

  > Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się

W tej lekcji dowiesz się:

- Jak tooconnect Intel NUC z urządzenia peryferyjne.
- Jak pakietów hello wymagane tooinstall i aktualizacji przy użyciu Intel NUC hello inteligentne Menedżera pakietów.
- Jak toorun hello "hello_world" Przykładowe funkcjonalność bramy hello tooverify aplikacji.

## <a name="what-you-need"></a>Co jest potrzebne

- Intel NUC Kit DE3815TYKE z hello pakiet oprogramowania bramy IoT firmy Intel (Linux rzeki knie * 7.0.0.13) preinstalowany. [Kliknij tutaj toopurchase Grove IoT komercyjnych bramy zestawu](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).
- Kabla Ethernet.
- Klawiatury.
- Kabel HDMI lub VGA.
- Monitor portu HDMI lub VGA.
- Opcjonalnie: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)

![Zestaw bramy](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>Intel NUC Uzyskuj dostęp do urządzeń peryferyjnych hello

Obraz powitania poniżej przedstawiono przykładowy NUC firmy Intel, który jest połączony z różnych urządzeń peryferyjnych:

1. Klawiatura tooa połączonych.
2. Połączone tooa monitor za pomocą kabla VGA lub kabla HDMI.
3. Połączone tooa przewodowej sieci za pomocą kabla Ethernet.
4. Zasilacz tooa połączonych za pomocą kabla zasilania.

![Tooperipherals NUC Intel połączone](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Połącz system Intel NUC toohello z komputera hosta za pośrednictwem protokołu Secure Shell (SSH)

Konieczne będzie, klawiatury i monitora adresu IP hello tooget urządzenia Intel NUC. Jeśli znasz już hello IP adresu, możesz pominąć wyprzedzeniem toostep 3 w tej sekcji.

1. Włącz hello Intel NUC, naciskając przycisk zasilania hello, a następnie zaloguj.

   Hello domyślna nazwa użytkownika i hasło są `root`.

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. Pobierz adres IP hello hello Intel NUC, uruchamiając hello `ifconfig` na powitania Intel NUC urządzenia.

   Oto przykład danych wyjściowych polecenia hello.

   ![dane wyjściowe ifconfig przedstawiający Intel NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   W tym przykładzie hello wartość, która wykonuje `inet addr:` jest adresem IP hello potrzebne przy połączeniu toohello Intel NUC z komputera-hosta.

3. Użyj jednej z hello poniższych klientów SSH z tooIntel tooconnect NUC Twojego hosta komputera.

    - [PuTTY](http://www.putty.org/) dla systemu Windows.
    - Witaj wbudowanego klienta SSH Ubuntu lub macOS.

   Jest bardziej wydajny i produktywności toooperate NUC Intel z komputera-hosta. Będzie konieczne hello Intel NUC adres IP użytkownika tooit tooconnect nazwy i hasła przy użyciu klienta SSH. Oto przykład, które używa klienta SSH w macOS.
   ![Klient SSH systemem macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Zainstaluj pakiet Azure IoT krawędzi hello

Pakiet Azure IoT krawędzi Hello zawiera wstępnie skompilowanych plików binarnych hello krawędzi IoT i jego zależności. Te pliki binarne są Azure IoT krawędzi, hello Azure IoT SDK i narzędzia odpowiednie hello. Witaj pakietu zawiera także "hello_world" Przykładowa aplikacja jest funkcjonalność bramy hello toovalidate używane. Krawędź IoT jest hello główną część hello bramy. 

Wykonaj te kroki tooinstall hello pakietu.

1. Dodaj hello repozytorium chmury IoT, uruchamiając następujące polecenia w oknie terminalu hello:

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > Wprowadź "y", gdy monit too'Include ten kanał? "
   
   Jeśli zostanie wyświetlony `import read failed(-1)` błąd, hello Użyj następującego polecenia tooresolve hello problemu:
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   Witaj `rpm` polecenie importuje hello klucza obr. / min. Witaj `smart channel` polecenie dodaje hello rpm kanału toohello inteligentne Menedżera pakietów. Przed rozpoczęciem powitalne `smart update` polecenia, zostanie wyświetlony wyjścia, takich jak poniżej.

   ![obr. / min i dane wyjściowe polecenia inteligentne kanału](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. Wykonanie polecenia update inteligentne hello:

   ```bash
   smart update
   ```

3. Zainstaluj pakiet Azure IoT bramy hello, uruchamiając następujące polecenie hello:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`jest nazwą hello hello pakietu. Witaj `smart install` polecenia jest używane tooinstall hello pakietu.

    > Witaj uruchom następujące polecenie, jeśli zostanie wyświetlony ten błąd: "klucz publiczny nie jest dostępna"

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > Ponowny rozruch hello NUC firmy Intel, jeśli zostanie wyświetlony ten błąd: "nie zawiera util-linux deweloperów"

   Po zainstalowaniu pakietu hello Intel NUC jest gotowy toofunction jako brama.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Uruchom hello Azure IoT krawędzi "hello_world" przykładowej aplikacji

następujące Przykładowa aplikacja Hello tworzy bramę z `hello_world.json` pliku i używa podstawowych składników hello Azure IoT krawędzi architektura toolog pliku tooa wiadomość hello world (log.txt) co 5 sekund.

Przykładowa aplikacja hello Hello World można uruchomić, wykonując następujące polecenia hello:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

Zezwala aplikacji Hello World hello Uruchom kilka minut, a następnie naciśnij hello Enter klucza toostop go.
![dane wyjściowe aplikacji](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

> Możesz zignorować wszelkie błędy "handle(NULL) nieprawidłowy argument", które są wyświetlane po naciśnięciu przycisku Enter.

Możesz sprawdzić, że brama hello zostało wykonane pomyślnie, otwierając plik log.txt hello, która jest teraz w folderze hello_world ![log.txt widok katalogu](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)

Otwórz za pomocą następującego polecenia hello log.txt:

```bash
vim log.txt
```

Zostanie wtedy wyświetlone hello zawartość log.txt, który zostanie zapisany formatu JSON, hello rejestrowania komunikatów, które zostały napisane co 5 sekund, przez moduł Hello World bramy hello.
![Widok katalogu log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)

Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Podsumowanie

Gratulacje! Po zakończeniu konfigurowania Intel NUC jako brama. Teraz możesz już toomove na toohello dalej tooset lekcji komputera hosta tworzenia Centrum IoT Azure i rejestrowanie urządzenia logicznego centrum IoT Azure.

## <a name="next-steps"></a>Następne kroki
[Użyj IoT bramy tooconnect tooAzure urządzenia IoT Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

