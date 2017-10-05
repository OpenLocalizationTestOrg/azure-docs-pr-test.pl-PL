---
title: "Symulowane urządzenie & Azure IoT bramy - Lekcja 1: Konfigurowanie NUC | Dokumentacja firmy Microsoft"
description: "Skonfigurować Intel NUC do pracy jako bramy IoT między czujników i Centrum IoT Azure do zbierania informacji z czujnika i wysyłania go do Centrum IoT."
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
ms.openlocfilehash: b87974be9570f7d03fe84ae0a1d1fa7e346ff189
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Konfigurowanie Intel NUC jako brama IoT

## <a name="what-you-will-do"></a>Będzie wykonywać

- Ustawienie Intel NUC jako bramę IoT.
- Zainstaluj pakiet Azure IoT Edge na Intel NUC.
- Uruchom przykładową aplikację "hello_world" na NUC firmy Intel, aby sprawdzić funkcjonalność bramy.
Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się

W tej lekcji dowiesz się:

- Jak nawiązać połączenia z urządzeń peryferyjnych Intel NUC.
- Sposób instalacji i aktualizacji wymaganych pakietów na NUC Intel pomocą inteligentne Menedżera pakietów.
- Jak uruchomić "hello_world" przykładowej aplikacji, aby sprawdzić funkcjonalność bramy.

## <a name="what-you-need"></a>Co jest potrzebne

- Intel NUC Kit DE3815TYKE z pakietem oprogramowania bramy IoT firmy Intel (Linux rzeki knie * 7.0.0.13) preinstalowany.
- Kabla Ethernet.
- Klawiatury.
- Kabel HDMI lub VGA.
- Monitor portu HDMI lub VGA.

![Zestaw bramy](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a>Połącz z urządzeniami peryferyjnymi Intel NUC

Na poniższym obrazie przedstawiono przykładowy NUC firmy Intel, który jest połączony z różnych urządzeń peryferyjnych:

1. Podłączona do klawiatury.
2. Połączenie monitor przez kabel VGA lub kabla HDMI.
3. Połączone z siecią przewodową za kabla Ethernet.
4. Podłączone do źródła zasilania, za pomocą kabla zasilania.

![Połączone dla urządzeń peryferyjnych NUC Intel](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Połączyć się z systemem Intel NUC z komputera hosta za pośrednictwem protokołu Secure Shell (SSH)

W tym miejscu należy klawiatury i monitora, aby uzyskać adres IP urządzenia NUC. Jeśli już znasz adres IP, należy przejść do kroku 3 w tej sekcji.

1. Włącz NUC firmy Intel, naciskając przycisk zasilania i logowania w systemie.

   Domyślna nazwa użytkownika i hasło są `root`.

2. Uzyskaj adres IP NUC uruchamiając `ifconfig` polecenia. Ten krok jest realizowane na urządzeniu NUC.

   Oto przykład danych wyjściowych polecenia.

   ![dane wyjściowe ifconfig przedstawiający NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   W tym przykładzie wartość następujący `inet addr:` to adres IP, do którego należy, jeśli planujesz łączyć się zdalnie z komputera-hosta Intel NUC.

3. Do nawiązania połączenia NUC firmy Intel, użyj jednej z następujących klientów SSH z komputera-hosta.

   - [PuTTY](http://www.putty.org/) dla systemu Windows.
   - Kompilacji w SSH klient Ubuntu lub macOS.

   Jest bardziej wydajny i produktywności do działania na Intel NUC z komputera-hosta. Potrzebujesz adresu IP, nazwę użytkownika i hasło, aby połączyć NUC przy użyciu klienta SSH. Oto przykład użycia SSH klient, na macOS.
   ![Klient SSH systemem macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-the-azure-iot-edge-package"></a>Zainstaluj pakiet Azure IoT krawędzi

Pakiet Azure IoT krawędzi zawiera wstępnie skompilowanych plików binarnych zestawu SDK i jego zależności. Te pliki binarne są Azure IoT krawędzi, zestaw SDK usługi Azure IoT i odpowiednie narzędzia. Pakiet zawiera również "hello_world" przykładowej aplikacji, która służy do sprawdzania poprawności funkcje bramy. Krawędź IoT jest główną część bramy. Aby zainstalować pakiet, wykonaj następujące kroki:

1. Dodaj repozytorium chmury IoT, uruchamiając następujące polecenia w oknie terminala:

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   `rpm` Polecenie importuje klucz obr. / min. `smart channel` Polecenie dodaje kanału obr. / min na inteligentne Menedżera pakietów. Przed uruchomieniem `smart update` polecenia, zobacz dane wyjściowe podobne poniżej.

   ![obr. / min i dane wyjściowe polecenia inteligentne kanału](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. Zainstaluj pakiet, uruchamiając następujące polecenie:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`to nazwa pakietu. `smart install` Polecenie służy do zainstalowania pakietu.

   Po zainstalowaniu pakietu Intel NUC powinien działać jako brama.

## <a name="run-the-azure-iot-edge-helloworld-sample-application"></a>Uruchom przykładową aplikację "hello_world" krawędzi IoT Azure

Przejdź do `azureiotgatewaysdk/samples` i uruchomić przykładowe "hello_world" przykładowej aplikacji. Ta przykładowa aplikacja tworzy bramę z `hello_world.json` pliku i używa podstawowych składników architektury Azure IoT Edge, aby wiadomość hello world w pliku dziennika co 5 sekund.

Przykładowe "hello_world" przykładową aplikację można uruchomić, uruchamiając następujące polecenie:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

Przykładowa aplikacja tworzy następujące dane wyjściowe, jeśli funkcję bramy działa prawidłowo:

![dane wyjściowe aplikacji](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Podsumowanie

Gratulacje! Po zakończeniu konfigurowania Intel NUC jako brama. Teraz możesz przejść do następnej lekcji, aby skonfigurować komputer hosta, tworzenia Centrum Azure IoT i zarejestrować urządzenia logicznego centrum Azure IoT.

## <a name="next-steps"></a>Następne kroki
[Przygotuj komputer hosta, a następnie Centrum Azure IoT](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
