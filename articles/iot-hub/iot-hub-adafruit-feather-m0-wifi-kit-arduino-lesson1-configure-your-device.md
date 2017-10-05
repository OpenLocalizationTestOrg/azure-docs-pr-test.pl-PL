---
title: "Connect Arduino (C) do Azure IoT — Lekcja 1: Konfigurowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Konfigurowanie sieci Wi-Fi Adafruit piór M0 dla pierwszego użycia."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino ustawienie nawiązać arduino komputerów, arduino Instalatora, arduino tablicy"
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
ms.openlocfilehash: 9e319292e5d30dea7e45857e435825861aad1c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a>Konfigurowanie urządzenia
## <a name="what-you-will-do"></a>Będzie wykonywać
Skonfiguruj tablicy Adafruit piór M0 sieci Wi-Fi Arduino dla pierwszego użycia przez łączenie tablicy, jego uruchomienia. Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).

## <a name="what-you-need"></a>Co jest potrzebne
Aby wykonać tę operację, potrzebne następujące części dla Twojego startowy Adafruit piór M0 sieci Wi-Fi:

* Tablica Adafruit piór M0 sieci Wi-Fi
* B Micro do kabla USB A typu

![zestaw][kit]

Wymagane są również:

* Komputer z systemem Windows, Mac lub Linux.
* Połączenia bezprzewodowego dla tablicy Arduino do nawiązania połączenia.
* Połączenia internetowego na pobieranie narzędzia do konfiguracji.

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:

* Jak utworzyć tablicy Arduino i włączenie go dla następujących — lekcje.
* Jak dodawać uprawnienia portu szeregowego na Ubuntu.

## <a name="connect-your-arduino-board-to-your-computer"></a>Łączenie się z komputerem tablicy Arduino

1. Podłącz kabel USB micro do górnej micro portu USB.

   ![Górny micro portu USB][top-micro-usb-port]

2. Podłącz drugi koniec kabla USB do komputera.

   ![Komputer USB][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a>Dodaj uprawnienia portu szeregowego na Ubuntu

Jeśli używasz systemu Windows lub macOS można pominąć tę sekcję. Ubuntu należy następujące kroki, aby upewnij się, że użytkownik normalne linux ma uprawnienia do działania na port USB Arduino tablicy.

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

   "0" może być inny numer, lub może być zwrócony wiele wpisów. W pierwszym przypadku danych potrzebne jest `uucp`, w ciągu sekundy jest `dialout`, który jest właścicielem grupy pliku.

2. Dodaj użytkownika do grupy:

   ```bash
   sudo usermod -a -G group-name username
   ```

   Gdzie `group-name` danych znaleziono w pierwszym kroku i `username` to nazwa użytkownika systemu linux.

3. Konieczne będzie rejestrować Wyloguj się i zaloguj ponownie ta zmiana została uwzględniona i ukończyć instalację.

## <a name="summary"></a>Podsumowanie
W tym artykule kiedy znasz już sposobu konfigurowania Arduino tablicy. Następne zadanie jest Zainstaluj niezbędne narzędzia i oprogramowania w ramach przygotowań do uruchomienia na tablicy Arduino przykładowej aplikacji.

![Sprzęt jest gotowy][hardware-is-ready]

## <a name="next-steps"></a>Następne kroki
[Pobierz narzędzia][get-the-tools]
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md