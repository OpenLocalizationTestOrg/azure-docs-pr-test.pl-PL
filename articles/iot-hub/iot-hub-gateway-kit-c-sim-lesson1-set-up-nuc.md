---
title: "Symulowane urządzenie & Azure IoT bramy - Lekcja 1: Konfigurowanie NUC | Dokumentacja firmy Microsoft"
description: "Ustawienie toowork Intel NUC jako bramy IoT między czujników i informacji z czujnika toocollect Centrum IoT Azure i wysyłać je tooIoT koncentratora."
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: iot bramy intel nuc nuc komputera, DE3815TYKE
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Konfigurowanie Intel NUC jako brama IoT

## <a name="what-you-will-do"></a>Będzie wykonywać

- Ustawienie Intel NUC jako bramę IoT.
- Zainstaluj pakiet Azure IoT krawędzi hello na Intel NUC.
- Uruchom przykładową aplikację "hello_world" na funkcjonalność bramy hello tooverify Intel NUC.
Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się

W tej lekcji dowiesz się:

- Jak tooconnect Intel NUC z urządzenia peryferyjne.
- Jak pakietów hello wymagane tooinstall i aktualizacji przy użyciu Intel NUC hello inteligentne Menedżera pakietów.
- Jak toorun hello "hello_world" Przykładowe funkcjonalność bramy hello tooverify aplikacji.

## <a name="what-you-need"></a>Co jest potrzebne

- Intel NUC Kit DE3815TYKE z hello pakiet oprogramowania bramy IoT firmy Intel (Linux rzeki knie * 7.0.0.13) preinstalowany.
- Kabla Ethernet.
- Klawiatury.
- Kabel HDMI lub VGA.
- Monitor portu HDMI lub VGA.

![Zestaw bramy](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>Intel NUC Uzyskuj dostęp do urządzeń peryferyjnych hello

Obraz powitania poniżej przedstawiono przykładowy NUC firmy Intel, który jest połączony z różnych urządzeń peryferyjnych:

1. Klawiatura tooa połączonych.
2. Połączone monitor toohello kabel VGA lub kabla HDMI.
3. Połączone tooa ich z przewodową siecią przez kabla Ethernet.
4. Zasilacz toohello połączonych za pomocą kabla zasilania.

![Tooperipherals NUC Intel połączone](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Połącz system Intel NUC toohello z komputera hosta za pośrednictwem protokołu Secure Shell (SSH)

W tym miejscu należy klawiatury i monitora tooget hello adres IP urządzenia NUC. Jeśli znasz już hello IP adresu, możesz pominąć toostep 3 w tej sekcji.

1. Włącz NUC firmy Intel, naciskając przycisk zasilania hello i dziennika w systemie hello.

   Hello domyślna nazwa użytkownika i hasło są `root`.

2. Uzyskaj adres IP hello NUC uruchamiając hello `ifconfig` polecenia. Ten krok jest wykonywana na powitania NUC urządzenia.

   Oto przykład danych wyjściowych polecenia hello.

   ![dane wyjściowe ifconfig przedstawiający NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   W tym przykładzie hello wartość, która wykonuje `inet addr:` jest adresem IP hello potrzebne, planując tooconnect zdalnie z tooIntel komputera hosta NUC.

3. Użyj jednej z hello poniższych klientów SSH z tooIntel tooconnect NUC z hosta maszyny.

   - [PuTTY](http://www.putty.org/) dla systemu Windows.
   - Witaj w kompilacji SSH klient Ubuntu lub macOS.

   Jest bardziej wydajny i produktywności toooperate na Intel NUC z komputera-hosta. Potrzebujesz adresu IP hello hello, nazwę użytkownika i hasło tooconnect hello NUC przy użyciu klienta SSH. Oto klienta SSH Użyj przykład hello na macOS.
   ![Klient SSH systemem macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Zainstaluj pakiet Azure IoT krawędzi hello

Pakiet Azure IoT krawędzi Hello zawiera hello wstępnie skompilowanych plików binarnych hello zestawu SDK i jego zależności. Te pliki binarne są Azure IoT krawędzi, hello Azure IoT SDK i narzędzia odpowiednie hello. Pakiet HELLO zawiera również "hello_world" przykładowej aplikacji, która jest funkcjonalność bramy hello toovalidate używane. Krawędź IoT jest hello główną część hello bramy. Witaj tooinstall pakiet, wykonaj następujące kroki:

1. Dodaj hello IoT chmury repozytorium, uruchamiając następujące polecenia w oknie terminalu hello:

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   Witaj `rpm` polecenie importuje hello klucza obr. / min. Witaj `smart channel` polecenie dodaje hello rpm kanału toohello inteligentne Menedżera pakietów. Przed rozpoczęciem powitalne `smart update` polecenia, zobacz dane wyjściowe podobne poniżej.

   ![obr. / min i dane wyjściowe polecenia inteligentne kanału](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. Instalacja pakietu hello, uruchamiając następujące polecenie hello:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`jest nazwą hello hello pakietu. Witaj `smart install` polecenia jest używane tooinstall hello pakietu.

   Po zainstalowaniu pakietu hello Intel NUC jest oczekiwany toowork jako brama.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Uruchom hello Azure IoT krawędzi "hello_world" przykładowej aplikacji

Przejdź do zbyt`azureiotgatewaysdk/samples` i uruchom hello próbki "hello_world" przykładowej aplikacji. Ta przykładowa aplikacja tworzy bramę z hello `hello_world.json` pliku i używa podstawowych składników hello Azure IoT krawędzi architektura toolog pliku tooa wiadomość hello world hello co 5 sekund.

Hello próbki "hello_world" przykładową aplikację można uruchomić, uruchamiając następujące polecenie hello:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

Witaj przykładowej aplikacji daje następujące hello wyniki, jeśli hello funkcjonalność bramy działa prawidłowo:

![dane wyjściowe aplikacji](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Podsumowanie

Gratulacje! Po zakończeniu konfigurowania Intel NUC jako brama. Teraz wszystko jest gotowe toomove na toohello dalej tooset lekcji komputera hosta utworzyć Centrum Azure IoT i zarejestrować urządzenia logicznego centrum Azure IoT.

## <a name="next-steps"></a>Następne kroki
[Przygotuj komputer hosta, a następnie Centrum Azure IoT](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
