---
title: "Connect Arduino (C) tooAzure IoT — Lekcja 1: Konfigurowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Konfigurowanie sieci Wi-Fi Adafruit piór M0 dla pierwszego użycia."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino Konfigurowanie, Połącz arduino toopc, arduino Instalatora, arduino tablicy"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a>Konfigurowanie urządzenia
## <a name="what-you-will-do"></a>Będzie wykonywać
Skonfiguruj tablicy Adafruit piór M0 sieci Wi-Fi Arduino dla pierwszego użycia przez łączenie tablicy hello, jego uruchomienia. Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).

## <a name="what-you-need"></a>Co jest potrzebne
toocomplete tej operacji, należy hello następujące części dla Twojego startowy Adafruit piór M0 sieci Wi-Fi:

* Witaj tablicy Adafruit piór M0 sieci Wi-Fi
* TooType Micro B kabla A USB

![zestaw][kit]

Wymagane są również:

* Komputer z systemem Windows, Mac lub Linux.
* Połączenia bezprzewodowego dla Twojego tooconnect tablicy Arduino do.
* Internet połączenia toodownload narzędzie konfiguracji.

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:

* Jak tooassemble Arduino tablicy, a power go dla następującego hello lekcje.
* Jak tooadd uprawnienia Ubuntu portu szeregowego.

## <a name="connect-your-arduino-board-tooyour-computer"></a>Połącz komputer tooyour Arduino tablicy

1. Podłącz kabel USB micro hello do portu USB micro najwyższego hello.

   ![Górny micro portu USB][top-micro-usb-port]

2. Plug hello drugiej, kabel USB do komputera.

   ![Komputer USB][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a>Dodaj uprawnienia portu szeregowego na Ubuntu

Jeśli używasz systemu Windows lub macOS można pominąć tę sekcję. Ubuntu należy hello następujące kroki toomake się, że hello normalne linux użytkownik ma toooperate uprawnienia hello na port USB hello Arduino tablicy.

1. Teraz jako zwykłego użytkownika z terminalu:

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   Otrzymasz wyglądać mniej więcej tak:

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   Witaj, "0" może być inną liczbę lub może być zwrócony wiele wpisów. W hello potrzebujemy pierwsze dane przypadków hello jest `uucp`, hello drugi jest `dialout`, który jest właścicielem grupy hello hello pliku.

2. Dodaj grupę toohello toohello użytkowników:

   ```bash
   sudo usermod -a -G group-name username
   ```

   Gdzie `group-name` dane hello w pierwszym krokiem hello i `username` to nazwa użytkownika systemu linux.

3. Konieczne będzie toolog Wyloguj się i zaloguj ponownie dla tego efektu tootake zmiany i hello ukończenia instalacji.

## <a name="summary"></a>Podsumowanie
W tym artykule, kiedy znasz już jak tooconfigure Arduino tablicy. następne zadanie Hello jest tooinstall hello niezbędne narzędzia i oprogramowania w ramach przygotowań do uruchomienia na tablicy Arduino przykładowej aplikacji.

![Sprzęt jest gotowy][hardware-is-ready]

## <a name="next-steps"></a>Następne kroki
[Pobierz narzędzia hello][get-the-tools]
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md